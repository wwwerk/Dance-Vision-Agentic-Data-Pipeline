# Portable Secrets Management with SOPS + age on macOS Big Sur

A self-contained setup for storing encrypted secrets inside project git repositories, with no Homebrew, no cloud KMS, and no PGP keyring — just two static binaries, a tiny age key file, a `.sops.yaml` config, and a pre-commit hook that refuses plaintext secrets.

**How the pieces fit together:**

- **SOPS** encrypts individual values inside YAML, JSON, dotenv, and INI files while leaving key names and structure readable — so diffs stay meaningful and merges mostly work ([getsops.io docs](https://getsops.io/docs/)). Comments are encrypted too.
- **age** provides the encryption keys: a small X25519 identity file you keep on your machine, and a public recipient string that goes in the repo config. SOPS supports age natively as a key source ([getsops.io docs](https://getsops.io/docs/)).
- **The pre-commit hook** validates the staged content of every secrets file — cryptographically, and against a full-encryption policy — before a commit is allowed.

---

## Critical: version compatibility on Big Sur

Before anything else — **the latest releases of both tools will not run on macOS 11 Big Sur.** Both are Go programs, and the Go toolchain that builds a binary determines the minimum macOS it supports. Go 1.24 is the last release that runs on Big Sur; Go 1.25 and later require macOS 12 Monterey ([Go 1.24 release notes](https://go.dev/doc/go1.24#darwin), [Go 1.25 release notes](https://go.dev/doc/go1.25#darwin), [Go wiki: Darwin](https://go.dev/wiki/Darwin)).

I verified the embedded Go build version inside each release's darwin binaries (Go records its toolchain version in every binary) against the [sops releases page](https://github.com/getsops/sops/releases) and [age releases page](https://github.com/FiloSottile/age/releases):

| Tool | Release | Built with | Runs on Big Sur 11? |
|---|---|---|---|
| sops | [v3.13.3](https://github.com/getsops/sops/releases/tag/v3.13.3) (latest) | Go 1.26.5 | No — [needs macOS 12+](https://go.dev/doc/go1.25#darwin) |
| sops | v3.12.x | Go 1.26.0–1.26.1 | No — [needs macOS 12+](https://go.dev/doc/go1.25#darwin) |
| sops | v3.11.0 | Go 1.25.1 | No — [needs macOS 12+](https://go.dev/doc/go1.25#darwin) |
| **sops** | **[v3.10.2](https://github.com/getsops/sops/releases/tag/v3.10.2)** | **Go 1.24.2** | **Yes — use this** |
| age | [v1.3.2](https://github.com/FiloSottile/age/releases/tag/v1.3.2) (latest) | Go 1.27 | No — [needs macOS 13+](https://github.com/golang/wiki/blob/master/MinimumRequirements.md) |
| age | v1.3.0–v1.3.1 | Go 1.25.5 | No — [needs macOS 12+](https://go.dev/doc/go1.25#darwin) |
| **age** | **[v1.2.1](https://github.com/FiloSottile/age/releases/tag/v1.2.1)** | **Go 1.23.4** | **Yes — use this** |

This guide pins **sops v3.10.2** and **age v1.2.1**. If you later upgrade the Mac past Big Sur, upgrade both tools to current versions at the same time — the encrypted files themselves are portable; only the binaries are version-locked to the OS.

---

## Part 1 — Install the binaries (manual download)

Everything installs into `~/.local/bin`, a user-owned directory that needs no admin rights. Big Sur's default shell is zsh, so PATH goes in `~/.zshrc`.

### 1.1 Detect your architecture

```bash
uname -m
```

- `arm64` → Apple Silicon
- `x86_64` → Intel

### 1.2 Install SOPS v3.10.2

```bash
mkdir -p ~/.local/bin && cd "$(mktemp -d)"

ARCH="arm64"        # set to amd64 on Intel
V="3.10.2"

curl -fLO "https://github.com/getsops/sops/releases/download/v${V}/sops-v${V}.darwin.${ARCH}"

# Verify checksum before installing — aborts on mismatch.
# Values from the official sops-v3.10.2.checksums.txt release asset:
EXPECTED="99702df79737162b986641afb8d98251acb16a52e6cab556a6b6f57c608c059a"   # arm64
# EXPECTED="dece9b0131af5ced0f8c278a53c0cf06a4f0d1d70a177c0979f6d111654397ce" # amd64
ACTUAL=$(shasum -a 256 "sops-v${V}.darwin.${ARCH}" | awk '{print $1}')
[ "$ACTUAL" = "$EXPECTED" ] || { echo "checksum mismatch — aborting" >&2; exit 1; }

chmod +x "sops-v${V}.darwin.${ARCH}"
mv "sops-v${V}.darwin.${ARCH}" ~/.local/bin/sops
```

### 1.3 Install age v1.2.1

```bash
cd "$(mktemp -d)"

ARCH="arm64"        # amd64 on Intel
V="1.2.1"

curl -fLO "https://github.com/FiloSottile/age/releases/download/v${V}/age-v${V}-darwin-${ARCH}.tar.gz"

# Verify checksum before extracting — aborts on mismatch.
EXPECTED="cf79875bd5970dc2dac60c87fa50cee1ff1f9a41b0eb273f65e174aff37c367a"   # arm64
# EXPECTED="424e1d64438a730626540b2e01e98d132a64214442ca9465b3e82336d12e633e" # amd64
ACTUAL=$(shasum -a 256 "age-v${V}-darwin-${ARCH}.tar.gz" | awk '{print $1}')
[ "$ACTUAL" = "$EXPECTED" ] || { echo "checksum mismatch — aborting" >&2; exit 1; }

tar xzf "age-v${V}-darwin-${ARCH}.tar.gz"
mv age/age age/age-keygen ~/.local/bin/
```

The hashes above were computed from the official release downloads at the time of writing; age also publishes a `.proof` file next to each tarball — a signed checksum-transparency-log entry ([age README](https://github.com/FiloSottile/age)) — if you want independently authenticated provenance beyond the hash comparison.

### 1.4 PATH and verification

Add to `~/.zshrc` (or `~/.bash_profile` if you use bash):

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Then reload and check both tools:

```bash
source ~/.zshrc
sops --version        # expect: sops 3.10.2
age --version         # expect: v1.2.1
age-keygen --version  # expect: v1.2.1
```

### 1.5 Gatekeeper

Binaries downloaded with `curl` in Terminal normally carry no quarantine attribute, so Gatekeeper will not block them — confirm with `xattr -l ~/.local/bin/sops`. If you downloaded through a browser instead, macOS may quarantine the file; remove the attribute for that one file:

```bash
xattr -d com.apple.quarantine ~/.local/bin/sops
```

Do not disable Gatekeeper system-wide (`spctl --master-disable`) to work around this — it is never necessary here.

---

## Part 2 — Generate your age key

The identity file is the one thing that must never enter the repository. Generate it with a restrictive umask so it is created with `600` permissions:

```bash
mkdir -p ~/.config/sops/age
(umask 077 && age-keygen -o ~/.config/sops/age/keys.txt)
```

Output looks like:

```
public key: age1ql3z77g2xzg5q2tq7zlx7xs5hcevl36l8y0cd3yh9fr3mn9c2d5sj95xhq
```

The file itself contains the private `AGE-SECRET-KEY-1...` line; the printed `age1...` string is the matching **public recipient** — that is the only part that belongs in the repo.

Point SOPS at the key explicitly rather than relying on defaults. Add to `~/.zshrc`:

```bash
export SOPS_AGE_KEY_FILE="$HOME/.config/sops/age/keys.txt"
```

**Back the key up now** — into your password manager or encrypted storage. The age identity is the only way to decrypt your files; there is no key escrow, and losing it loses the secrets. Portable here means the repo travels, never the private key.

---

## Part 3 — `.sops.yaml` for the repository

The file policy this guide uses:

| Path | Committed? | Content |
|---|---|---|
| `secrets/*.yaml`, `secrets/*.env` (nested too) | Yes | SOPS-encrypted secrets |
| `.sops.yaml`, `.githooks/` | Yes | Public config + hook |
| `.env` (repo root) | No (gitignored) | Decrypted runtime output |
| `~/.config/sops/age/keys.txt` | Never | Your private identity |

Place `.sops.yaml` in the repository root (the filename must be exactly `.sops.yaml`, not `.sops.yml` — [getsops.io reference](https://getsops.io/docs/reference/)):

```yaml
# .sops.yaml — SOPS creation rules. COMMIT THIS FILE.
# It contains only PUBLIC recipients (like a public key) — never private keys.
# SOPS looks for this file in the repo root and matches rules top-to-bottom;
# the first path_regex that matches a file's path (relative to this file) wins.
#
# encrypted_regex: '.*' forces FULL-VALUE encryption. Without it, SOPS's
# default policy leaves any key ending in "_unencrypted" in the clear —
# the pre-commit hook rejects files without this policy.
creation_rules:
  # Structured YAML secrets: secrets/*.yaml and secrets/*.yml
  - path_regex: '^secrets/.*\.ya?ml$'
    encrypted_regex: '.*'
    age: 'age1REPLACE_WITH_YOUR_PUBLIC_RECIPIENT'

  # dotenv secrets: secrets/*.env (KEY=value files)
  - path_regex: '^secrets/.*\.env$'
    encrypted_regex: '.*'
    age: 'age1REPLACE_WITH_YOUR_PUBLIC_RECIPIENT'
```

Replace `age1REPLACE_WITH_YOUR_PUBLIC_RECIPIENT` with your own printed public key from Part 2.

Three behaviors worth knowing:

- SOPS selects the file format from the path: `.yaml`/`.yml` → YAML, `.env` → dotenv, `.json` → JSON; anything else falls back to binary whole-file encryption ([getsops.io reference](https://getsops.io/docs/reference/)). The dotenv match is a strict `.env` suffix — `app.env` works, `.env.production` does not.
- `encrypted_regex: '.*'` is not cosmetic: by default SOPS leaves values for keys ending in `_unencrypted` in the clear ([getsops.io reference](https://getsops.io/docs/reference/)). The strict regex encrypts every key, and the pre-commit hook enforces it (Part 5).
- Creation rules only affect **encryption**. Decryption uses the metadata stored inside the file itself, so a teammate with a valid key can decrypt anything encrypted to their recipient.

### `.gitignore` for the repo root

```
# runtime plaintext — never commit (root .env only; encrypted secrets live in secrets/)
/.env
*.dec.yaml
*.dec.yml
*.dec.env
```

---

## Part 4 — Daily workflow

**Create a new encrypted secrets file:**

```bash
mkdir -p secrets
$EDITOR secrets/production.yaml        # write plaintext first
sops encrypt -i secrets/production.yaml # encrypt in place — now safe to commit
```

For dotenv files the same command works, because the `.env` suffix selects the dotenv format:

```bash
$EDITOR secrets/production.env
sops encrypt -i secrets/production.env
```

**Edit an encrypted file safely** (decrypts to a temp file, re-encrypts on save — verified working on 3.10.2):

```bash
sops edit secrets/production.yaml
```

**Decrypt to a runtime file the app reads** (stays local, gitignored). Restrict permissions before decryption, so a pre-existing mode-644 `.env` is never written to while world-readable, and a failed decrypt never leaves it more open than it started:

```bash
(
  umask 077
  touch .env &&
  chmod 600 .env &&
  sops decrypt secrets/production.env > .env
)
```

**What goes into git:** the encrypted files and `.sops.yaml`. What never does: the plaintext working copies you might make while editing (use `sops edit` instead), `.env`, and the key file.

---

## Part 5 — The pre-commit hook

The hook lives in the repo as `.githooks/pre-commit` so it is versioned with the project, then activated per clone with `core.hooksPath` (plain `.git/hooks` is not tracked by git, so it would silently miss on fresh clones).

### 5.1 The hook

Save as `.githooks/pre-commit`, then `chmod +x .githooks/pre-commit`:

```bash
#!/usr/bin/env bash
# pre-commit: block plaintext (or tampered) secrets from being committed.
# Install per clone:  git config core.hooksPath .githooks
# Bypass (unsafe):    git commit --no-verify
set -uo pipefail

# Files that must be valid SOPS ciphertext if committed (ERE on index paths).
# Root-anchored to match the .sops.yaml path_regex scope exactly.
PROTECTED_RE='^secrets/.*\.(ya?ml|env)$'
# Files that must never be committed at all.
NEVER_RE='^\.env$|\.dec\.(ya?ml|env)$'

sops_bin="${SOPS_BIN:-sops}"

# Fail closed: without sops nothing can be verified.
if ! command -v "$sops_bin" >/dev/null 2>&1; then
  echo "pre-commit: ERROR: 'sops' not found on PATH (set SOPS_BIN to override)." >&2
  echo "pre-commit: refusing to commit unverified secrets. Install sops, or" >&2
  echo "pre-commit: bypass at your own risk with: git commit --no-verify" >&2
  exit 1
fi

fail=0
workdir=$(mktemp -d "${TMPDIR:-/tmp}/precommit.XXXXXX") || exit 1
trap 'rm -rf "$workdir"' EXIT

# List staged additions/modifications/renames/copies (-z handles spaces;
# deletions are excluded — their content is not being committed).
staged_list="$workdir/staged"
if ! git diff --cached --name-only --diff-filter=ACMR -z > "$staged_list"; then
  echo "pre-commit: ERROR: failed to list staged files — refusing." >&2
  exit 1
fi

while IFS= read -r -d '' file <&4; do
  if [[ "$file" =~ $NEVER_RE ]]; then
    echo "pre-commit: REJECTED: '$file' must never be committed (runtime plaintext)." >&2
    fail=1
    continue
  fi
  if [[ "$file" =~ $PROTECTED_RE ]]; then
    # Validate the STAGED blob, not the working tree copy.
    blob="$workdir/blob"
    if ! git show ":$file" > "$blob" 2>/dev/null; then
      echo "pre-commit: ERROR: could not read staged '$file' — refusing." >&2
      fail=1
      continue
    fi
    case "$file" in
      *.yaml|*.yml) fmt=yaml ;;
      *.env)        fmt=dotenv ;;
      *)            fmt=binary ;;
    esac
    ok=1
    # 1) Must decrypt cleanly — proves valid SOPS metadata and MAC integrity.
    "$sops_bin" decrypt --input-type "$fmt" --output-type "$fmt" "$blob" >/dev/null 2>&1 || ok=0
    # 2) Metadata must declare the full-encryption policy (encrypted_regex: '.*').
    #    Without it, keys are exempted from encryption by default (the
    #    "_unencrypted" suffix rule), leaving values in the clear.
    if [[ "$ok" -eq 1 ]]; then
      case "$fmt" in
        yaml)
          # Metadata is everything after the reserved top-level 'sops:' key.
          sed -n '/^sops:/,$p' "$blob" > "$workdir/meta"
          grep -Eq '^[[:space:]]*encrypted_regex:[[:space:]]*\.\*[[:space:]]*$' "$workdir/meta" || ok=0
          grep -Eq '^[[:space:]]*unencrypted_(suffix|regex):[[:space:]]*[^[:space:]]' "$workdir/meta" && ok=0
          grep -Eq '^[[:space:]]*encrypted_suffix:[[:space:]]*[^[:space:]]' "$workdir/meta" && ok=0
          ;;
        dotenv)
          grep -Eq '^sops_encrypted_regex=\.\*$' "$blob" || ok=0
          grep -Eq '^sops_unencrypted_(suffix|regex)=[^[:space:]]' "$blob" && ok=0
          grep -Eq '^sops_encrypted_suffix=[^[:space:]]' "$blob" && ok=0
          ;;
      esac
    fi
    if [[ "$ok" -ne 1 ]]; then
      echo "pre-commit: REJECTED: '$file' is not fully-encrypted SOPS ciphertext." >&2
      echo "pre-commit: it is plaintext, was edited after encryption (MAC failed)," >&2
      echo "pre-commit: or was encrypted with a policy that leaves values in the clear." >&2
      echo "pre-commit: if it is plaintext, fix with:  sops encrypt -i \"$file\"" >&2
      echo "pre-commit: if it is already encrypted, its policy exempts values from encryption —" >&2
      echo "pre-commit: decrypt it to a temp file and re-encrypt it under this repo's rules." >&2
      fail=1
    fi
  fi
done 4< "$staged_list"

exit $fail
```

### 5.2 Activate it (once per clone)

```bash
git config core.hooksPath .githooks
```

Optionally add a one-line README note so teammates do the same after cloning. If your team standardizes on the [pre-commit framework](https://pre-commit.com) already, keep the same validation logic in a local hook repo entry instead.

### 5.3 How it works — and why it is built this way

- **It inspects the git index, not the working tree.** `git diff --cached --name-only` enumerates what is actually being committed, and `git show ":$file"` retrieves the staged blob. A plaintext file that is staged and then encrypted in the working tree is still rejected — and the reverse (encrypted staged, working copy now plaintext) correctly passes, because only the commit's content matters.
- **Validation is cryptographic, not cosmetic.** It runs `sops decrypt` with output discarded to `/dev/null`. SOPS verifies the file's MAC over the whole tree ([getsops.io reference](https://getsops.io/docs/reference/)), so this simultaneously catches plaintext files (no SOPS metadata), files edited after encryption (MAC failure — e.g. someone spliced a plaintext value into the ciphertext), and files encrypted to a key you do not hold.
- **It enforces the full-encryption policy.** A file can be perfectly MAC-valid and still contain plaintext values, because SOPS records its encryption policy in the file's own metadata — and by default, keys ending in `_unencrypted` are exempted from encryption ([getsops.io reference](https://getsops.io/docs/reference/)). The hook reads that staged metadata and rejects any file that does not declare `encrypted_regex: .*` (or that declares any exemption like `unencrypted_suffix`, `unencrypted_regex`, or `encrypted_suffix`).
- **It fails closed.** If `sops` is missing, if the staged file list cannot be read, or if your key cannot decrypt the file, the commit is rejected. An unverifiable secrets file should not be committed on trust.
- **No hidden dependencies.** Pure bash + git + sops — no Python, jq, or YAML parser needed. It uses only features available in Big Sur's stock bash 3.2. Temp files (which can contain staged plaintext) live in a private temp directory that a trap removes on exit.
- **It never prints decrypted content** — decrypt output goes to `/dev/null`.

### 5.4 Verified behavior

The hook and configuration were exercised end-to-end against an 18-case test matrix using the Linux builds of the same pinned versions (sops 3.10.2, age 1.2.1) — the logic is OS-independent, and Big Sur compatibility of the pinned darwin binaries is established by the toolchain evidence in the compatibility section, not by execution on Big Sur itself:

| Scenario | Result |
|---|---|
| Encrypted `secrets/*.yaml` and `secrets/*.env` staged | Commit allowed |
| Plaintext `secrets/*.yaml` staged | Blocked |
| Plaintext staged, then encrypted in working tree | Blocked (staged blob checked) |
| Encrypted staged, then decrypted in working tree | Allowed (index content is valid) |
| Nested `secrets/sub/app.yaml`, encrypted / plaintext | Allowed / blocked |
| Nested `secrets/sub/app.env`, plaintext | Blocked |
| Plaintext value in a key ending `_unencrypted`, file unencrypted | Blocked |
| MAC-valid file with an `_unencrypted`-exempt plaintext value (YAML and dotenv), encrypted under default rules | Blocked (policy check) |
| Same key encrypted with `encrypted_regex: '.*'` | Allowed, value encrypted |
| File encrypted with selective `encrypted_regex: '^password$'` | Blocked (partial policy) |
| Protected path containing spaces | Handled (`-z` iteration) |
| Unrelated files | Allowed |
| Deleting a protected file | Allowed (deletions carry no content) |
| Plaintext value spliced into encrypted ciphertext | Blocked (MAC failure) |
| File encrypted to a recipient you do not hold | Blocked (fail closed) |
| `sops` not installed | Blocked (fail closed) |
| Root `.env` or `*.dec.yaml` staged | Blocked (never-commit rule) |

### 5.5 Limitations — read this

- Local hooks are a guardrail, not a security boundary. Anyone can bypass with `git commit --no-verify`, and `core.hooksPath` must be set per clone. For real enforcement, run the same validation in CI on every pull request, where it cannot be bypassed — and note that CI must reproduce **both** checks the hook performs: the decryption/MAC validation and the staged-metadata policy check. A decrypt-only CI check is not sufficient — a MAC-valid file can still contain plaintext values exempted by policy, which is exactly the gap the policy check exists to close.

- The hook requires a valid identity for every protected file, so a teammate without the key cannot commit changes to secrets files. That is the fail-closed trade-off; if it is too strict, scope `PROTECTED_RE` more narrowly.
- It does not scan arbitrary files for secret-looking strings (high-entropy blobs, AWS keys in code, etc.) — it enforces the `secrets/` policy only. Pair it with a dedicated secret scanner if you need that.

---

## Part 6 — Portability across machines

The repo travels; each machine needs its own identity (or a restored backup):

```bash
# on a new machine: install the two binaries (Part 1), then either
#  a) restore your backed-up identity file to ~/.config/sops/age/keys.txt, or
#  b) create a new one (Part 2) and share the printed public key with the repo owner
```

To add a teammate's recipient so they can decrypt existing files, add their `age1...` string to `.sops.yaml`, then re-encrypt the data keys (file contents are not re-encrypted, only the per-file data key — fast):

```bash
sops updatekeys secrets/production.yaml
sops updatekeys secrets/production.env
```

To rotate after a key exposure (e.g. a laptop was lost), remove the old recipient from `.sops.yaml`, add a new one, then re-encrypt the data keys and rotate the file contents:

```bash
sops updatekeys secrets/production.yaml   # re-encrypt the per-file data key for the new recipients
sops rotate -i secrets/production.yaml     # new data key + re-encrypted contents
```

Understand what each step does and does not revoke. `sops updatekeys` preserves the existing file data key, so a former recipient who already copied it from repository history can still decrypt old revisions. `sops rotate -i` generates a fresh data key, which protects future revisions — but the old data key still decrypts every revision committed before the rotate, and nothing SOPS does changes the underlying credentials themselves. Treat real exposure as: rotate the data keys as above, and rotate the actual secrets (passwords, tokens) everywhere they are used.

---

## Quick reference

```bash
sops encrypt -i secrets/app.yaml      # encrypt in place (new file)
sops edit secrets/app.yaml            # safe edit: decrypt -> editor -> re-encrypt
# runtime decrypt with 600 perms (see Part 4):
#   ( umask 077; touch .env && chmod 600 .env && sops decrypt secrets/app.env > .env )
sops updatekeys secrets/app.yaml       # re-encrypt data key after .sops.yaml change
sops rotate -i secrets/app.yaml        # fresh data key + re-encrypted contents
git config core.hooksPath .githooks   # activate hook (once per clone)
```

## Sources

- [SOPS documentation — getsops.io](https://getsops.io/docs/)
- [SOPS configuration reference (.sops.yaml, formats) — getsops.io](https://getsops.io/docs/reference/)
- [SOPS releases — GitHub](https://github.com/getsops/sops/releases)
- [age releases — GitHub](https://github.com/FiloSottile/age/releases)
- [age project README (installation, verification) — GitHub](https://github.com/FiloSottile/age)
- [Go 1.24 release notes (last release to run on Big Sur) — go.dev](https://go.dev/doc/go1.24#darwin)
- [Go 1.25 release notes (requires macOS 12) — go.dev](https://go.dev/doc/go1.25#darwin)
- [Go wiki: Darwin platform support — go.dev](https://go.dev/wiki/Darwin)
- [Go wiki: Minimum requirements — GitHub](https://github.com/golang/wiki/blob/master/MinimumRequirements.md)

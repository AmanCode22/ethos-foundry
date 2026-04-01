# Ethos Foundry

Hard Traits registry for Ethos.

Use Forge to install native C/C++/Rust extensions. Hosted on Cloudflare Pages.

## Quick use

Search:
```bash
forge foundry search math
```

Install:
```bash
forge foundry get mymath
```

List what you have:
```bash
forge list native
```

Then in Ethos:
```
bring in mymath.
set result to run mymath.add with 10, 5.
say result.
```

## How this works

1. You write a Hard Trait using one of the template repos (C, C++, or Rust).
2. The template has GitHub Actions that build binaries for Linux, macOS, Windows, and Termux automatically.
3. You tag a release → binaries go to GitHub Releases.
4. A GitHub Action automatically opens a PR to this repo with your `manifest.json`.
5. I review it. If it looks good, I merge it. Done.

## Adding your trait

**Step 1 — Fork a template**

Pick your language:
- C: https://github.com/AmanCode22/ethos-trait-c (maintained by me)
- C++: https://github.com/AmanCode22/ethos-trait-cpp (maintained by me)
- Rust: https://github.com/AmanCode22/ethos-trait-rust (maintained by me)

If you wanna contribute by making api for other languages then open a issue with the repo link containing the api similar to above and I would put them here!

These repos have starter code, build config, and CI workflows. They compile for all platforms automatically when you tag a release.

**Step 2 — Build and release**

Write your code. Push. Tag a release like `v1.0.0`. The workflows build binaries and upload them to GitHub Releases automatically.

**Step 3 — PR opens automatically**

The template's GitHub Action detects your new release and opens a PR to this repo with your `manifest.json`. You don't need to do anything.

**Step 4 — Review and merge**

I review the PR personally. If it passes, I merge it. Your trait goes live on Foundry.

## Updating your trait

When you release a new version:

1. Update your trait repo and tag a new release (e.g., `v2.0.0`).
2. The CI builds new binaries and uploads them.
3. A new PR opens automatically to this repo with the updated `manifest.json`.
4. I review and merge. Users get the latest version when they run `forge foundry get`.

You don't need to do anything extra. Just tag a release.

## manifest.json fields

Required:
- `name` — must match your folder name exactly
- `version` — semver like `1.0.0` or `0.5.0-beta`
- `description` — one line about what it does
- `author` — your name or handle
- `repository` — link to your trait's source repo
- `license` — MIT, Apache-2.0, etc.
- `platforms` — object with one entry per OS you support
- `platforms.<os>.url` — direct link to the binary on GitHub Releases
- `platforms.<os>.checksum` — `sha256:<hash>` of that binary
- `functions` — list of functions Ethos can call
- `functions.<name>.return` — return type (see supported types below)
- `functions.<name>.args` — list of argument types

Optional:
- `tags` — keywords like `["math", "crypto"]` for search
- `verified` — leave `false`; I set it to `true` after I review your code

Supported types for `return` and `args`:
```
char, unsigned char, wchar_t
short, unsigned short
int, unsigned int
long, unsigned long
long long, unsigned long long
int8_t, uint8_t, int16_t, uint16_t
float, double, long double
char *, wchar_t *, void *
pointer_to_int, size_t, ssize_t
bool, void
```

## Rules

- Folder name must equal `manifest.name`
- No binaries in this repo — use GitHub Releases
- All URLs must be public
- Checksums are mandatory (SHA256)

## Platforms

Forge picks the right binary automatically:

| Tag | OS | Arch | Extension |
|-----|----|------|-----------|
| linux-x86_64 | Linux | x86_64 | .so |
| linux-aarch64 | Linux | ARM64 | .so |
| macos-arm64 | macOS | Apple Silicon | .dylib |
| macos-x86_64 | macOS | Intel | .dylib |
| windows-x86_64 | Windows | x86_64 | .dll |
| termux-aarch64 | Android/Termux | ARM64 | .so |
| termux-armv7 | Android/Termux | ARMv7 | .so |

## Links

- Ethos docs: https://github.com/AmanCode22/ethos-lang/blob/main/DOCS.md
- Forge: https://github.com/AmanCode22/forge
- C template: https://github.com/AmanCode22/ethos-trait-c
- C++ template: https://github.com/AmanCode22/ethos-trait-cpp
- Rust template: https://github.com/AmanCode22/ethos-trait-rust
- Building Ethos: https://github.com/AmanCode22/ethos-lang/blob/main/BUILDING.md

## License

MIT. Free to use, free to contribute.

---

Built by Aman (Class 9, India). Solo project. I review every PR myself. Questions? Open an issue.

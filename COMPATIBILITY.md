# Compatibility matrix

Which [`signetry-core`](https://github.com/Signetry/core) version each
integration supports. Every integration pins a **minimum** `signetry-core` and is
tested against it. The kernel follows [SemVer](https://semver.org/); until `1.0.0`
the public API may change between minor versions.

## signetry-core public API

| signetry-core | Highlights |
|---|---|
| **0.4.0** (latest) | CLI DX: `signetry init` scaffolder + `signetry completion` (bash/zsh/fish) · `install.sh` one-liner + Homebrew tap · Capabilities & Proof docs. |
| **0.3.0** | Capability graph (contract v2: tool/bash/MCP/skill allowlists) · plan binding (`PlanCapabilitySet`) · masked verifier (hijack signal) · G1/G2/G3 proof gates (`signetry gates`) · canonical PR-comment renderer (`signetry comment`) · Admitted Extension + ASBOM (`signetry admit-extension`). |
| **0.2.x** | Real-time guard (`signetry guard`) for editor hooks · SLSA/in-toto provenance · Merkle transparency log · passport + emergency brake. |
| **0.1.x** | Initial admission pipeline: contract, trust boundary, checks, verifier, earned authority, Ed25519 receipt, CLI + MCP server. |

## Integration → signetry-core

| Integration | Requires signetry-core | Notes |
|---|---|---|
| **signetry-action** | `>= 0.3.0` | Renders the PR comment via `signetry comment`; installs bubblewrap for the `sandboxed` tier. Was `>= 0.1.3`. |
| **signetry-reviewer** | none (stdlib) | Advisory reviewer; deterministic core has no signetry-core dependency. It *cross-verifies* the required check but does not import signetry-core. |
| **signetry-eval** | `>= 0.3.0` | Needs the capability graph, plan binding, masked verifier, gates, and `admit_extension`. |
| **signetry-plugins** | `>= 0.2.0` | Uses `signetry guard` for the editor PreToolUse hook. Superseded by the per-agent repos. |
| **signetry-claude-code** | `>= 0.3.0` | Split from signetry-plugins. PreToolUse guard + MCP + `/signetry:admit`. |
| **signetry-cursor** | `>= 0.3.0` | Split from signetry-plugins. MCP server + project rule. |
| **signetry-codex** | `>= 0.3.0` | Split from signetry-plugins. MCP server + lifecycle-hook guard. |
| **signetry-precommit** | `>= 0.3.0` | Split from signetry-plugins. Universal git / pre-commit guard. |
| **signetry** (hosted) | tracks `main` / latest | Converging on consuming `signetry-core` directly (no forked governance). |
| **signetry-github-app** (planned) | `>= 0.2.0` | — |
| **signetry-claude-code / -cursor / -codex / -precommit** (planned) | `>= 0.2.0` | Split from signetry-plugins; each pins independently. |

## Rule

An integration must **pin** its `signetry-core` dependency to a source tag
(`signetry-core @ git+https://github.com/Signetry/core@vX.Y.Z` — signetry-core is
source-available and not on PyPI) and never vendor or fork governance logic. If a
surface needs a new capability, it lands in `signetry-core` first, is released (a git
tag), then the integration bumps its pin here.

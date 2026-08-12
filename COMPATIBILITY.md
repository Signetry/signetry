# Compatibility matrix

Which [`umbra-core`](https://github.com/Signetry/core) version each
integration supports. Every integration pins a **minimum** `umbra-core` and is
tested against it. The kernel follows [SemVer](https://semver.org/); until `1.0.0`
the public API may change between minor versions.

## umbra-core public API

| umbra-core | Highlights |
|---|---|
| **0.4.0** (latest) | CLI DX: `umbra init` scaffolder + `umbra completion` (bash/zsh/fish) · `install.sh` one-liner + Homebrew tap · Capabilities & Proof docs. |
| **0.3.0** | Capability graph (contract v2: tool/bash/MCP/skill allowlists) · plan binding (`PlanCapabilitySet`) · masked verifier (hijack signal) · G1/G2/G3 proof gates (`umbra gates`) · canonical PR-comment renderer (`umbra comment`) · Admitted Extension + ASBOM (`umbra admit-extension`). |
| **0.2.x** | Real-time guard (`umbra guard`) for editor hooks · SLSA/in-toto provenance · Merkle transparency log · passport + emergency brake. |
| **0.1.x** | Initial admission pipeline: contract, trust boundary, checks, verifier, earned authority, Ed25519 receipt, CLI + MCP server. |

## Integration → umbra-core

| Integration | Requires umbra-core | Notes |
|---|---|---|
| **umbra-action** | `>= 0.3.0` | Renders the PR comment via `umbra comment`; installs bubblewrap for the `sandboxed` tier. Was `>= 0.1.3`. |
| **umbra-reviewer** | none (stdlib) | Advisory reviewer; deterministic core has no umbra-core dependency. It *cross-verifies* the required check but does not import umbra-core. |
| **umbra-eval** | `>= 0.3.0` | Needs the capability graph, plan binding, masked verifier, gates, and `admit_extension`. |
| **umbra-plugins** | `>= 0.2.0` | Uses `umbra guard` for the editor PreToolUse hook. Superseded by the per-agent repos. |
| **umbra-claude-code** | `>= 0.3.0` | Split from umbra-plugins. PreToolUse guard + MCP + `/umbra:admit`. |
| **umbra-cursor** | `>= 0.3.0` | Split from umbra-plugins. MCP server + project rule. |
| **umbra-codex** | `>= 0.3.0` | Split from umbra-plugins. MCP server + lifecycle-hook guard. |
| **umbra-precommit** | `>= 0.3.0` | Split from umbra-plugins. Universal git / pre-commit guard. |
| **umbra** (hosted) | tracks `main` / latest | Converging on consuming `umbra-core` directly (no forked governance). |
| **umbra-github-app** (planned) | `>= 0.2.0` | — |
| **umbra-claude-code / -cursor / -codex / -precommit** (planned) | `>= 0.2.0` | Split from umbra-plugins; each pins independently. |

## Rule

An integration must **pin** its `umbra-core` dependency to a source tag
(`umbra-core @ git+https://github.com/Signetry/core@vX.Y.Z` — umbra-core is
source-available and not on PyPI) and never vendor or fork governance logic. If a
surface needs a new capability, it lands in `umbra-core` first, is released (a git
tag), then the integration bumps its pin here.

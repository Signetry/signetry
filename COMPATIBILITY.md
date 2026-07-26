# Compatibility matrix

Which [`umbra-core`](https://github.com/bkd-dotcom/umbra-core) version each
integration supports. Every integration pins a **minimum** `umbra-core` and is
tested against it. The kernel follows [SemVer](https://semver.org/); until `1.0.0`
the public API may change between minor versions.

## umbra-core public API

| umbra-core | Highlights |
|---|---|
| **0.3.x** (next) | Capability graph (contract v2: tool/bash/MCP/skill allowlists) · plan binding (`PlanCapabilitySet`) · masked verifier (hijack signal) · G1/G2/G3 proof gates (`umbra gates`) · canonical PR-comment renderer (`umbra comment`) · Admitted Extension + ASBOM (`umbra admit-extension`). |
| **0.2.x** | Real-time guard (`umbra guard`) for editor hooks · SLSA/in-toto provenance · Merkle transparency log · passport + emergency brake. |
| **0.1.x** | Initial admission pipeline: contract, trust boundary, checks, verifier, earned authority, Ed25519 receipt, CLI + MCP server. |

## Integration → umbra-core

| Integration | Requires umbra-core | Notes |
|---|---|---|
| **umbra-action** | `>= 0.3.0` | Renders the PR comment via `umbra comment`; installs bubblewrap for the `sandboxed` tier. Was `>= 0.1.3`. |
| **umbra-eval** | `>= 0.3.0` | Needs the capability graph, plan binding, masked verifier, gates, and `admit_extension`. |
| **umbra-plugins** | `>= 0.2.0` | Uses `umbra guard` for the editor PreToolUse hook. |
| **umbra** (hosted) | tracks `main` / latest | Converging on consuming `umbra-core` directly (no forked governance). |
| **umbra-github-app** (planned) | `>= 0.2.0` | — |
| **umbra-claude-code / -cursor / -codex / -precommit** (planned) | `>= 0.2.0` | Split from umbra-plugins; each pins independently. |

## Rule

An integration must **pin** its `umbra-core` dependency (`umbra-core>=X.Y.Z`) and
never vendor or fork governance logic. If a surface needs a new capability, it
lands in `umbra-core` first, is released, then the integration bumps its pin here.

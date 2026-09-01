# Compatibility matrix

Which [`signetry-core`](https://github.com/Signetry/core) version each integration
supports. Every integration declares a **minimum** `signetry-core` and **pins** an exact
source tag; both columns are below, because they answer different questions — the
minimum tells you what a capability needs, the pin tells you what you actually get when
you install today. The kernel follows [SemVer](https://semver.org/); until `1.0.0` the
public API may change between minor versions.

## signetry-core public API

| signetry-core | Highlights |
|---|---|
| **0.8.0** (latest) | Receipt format published as an independently testable spec (`docs/RECEIPT_SPEC.md` + `tests/conformance/`, Apache-2.0) · `check_invariants()` and a `signetry verify` that fails on a non-conforming receipt · **policy registry** (`signetry policies`, `signetry init --policy <id>`) · placeholder provenance reported as `placeholder`, not as ownership · open core: kernel moves to BUSL-1.1, converting to Apache-2.0 on 2030-08-31. |
| **0.7.0** | Detection breadth: Kotlin scanned at all (it was absent from the extension map) · Go SSRF, Go/Java path traversal, PHP XXE · `AiderExecutor` · SSRF precision fixes. |
| **0.6.0** | Renamed to Signetry: `signetry` CLI, `signetry_core` package, `SIGNETRY_*` env, `.signetry/` config. |
| **0.5.1**–**0.5.4** | Source-available distribution (removed from PyPI; installed from a git tag) · Codex sandbox fixes on CI runners. |
| **0.5.0** | Detection engine + governed fix fusion (SAST over 7 languages, SARIF, cross-file taint) — `signetry scan`, `--fix`. |
| **0.4.0** | CLI DX: `signetry init` scaffolder + `signetry completion` (bash/zsh/fish) · `install.sh` one-liner + Homebrew tap · Capabilities & Proof docs. |
| **0.3.0** | Capability graph (contract v2: tool/bash/MCP/skill allowlists) · plan binding (`PlanCapabilitySet`) · masked verifier (hijack signal) · G1/G2/G3 proof gates (`signetry gates`) · canonical PR-comment renderer (`signetry comment`) · Admitted Extension + ASBOM (`signetry admit-extension`). |
| **0.2.x** | Real-time guard (`signetry guard`) for editor hooks · SLSA/in-toto provenance · Merkle transparency log · passport + emergency brake. |
| **0.1.x** | Initial admission pipeline: contract, trust boundary, checks, verifier, earned authority, Ed25519 receipt, CLI + MCP server. |

## Integration → signetry-core

As of the 2026-09-01 release train, every integration is pinned to the same kernel tag.
A row whose pin lags is a row to fix, which is the point of showing it.

| Integration | Released | Minimum | Pins | Notes |
|---|---|---|---|---|
| **action** | `v0.5.0` (`@v1`) | `>= 0.3.0` | `core@v0.8.0` | Renders the PR comment via `signetry comment`; installs bubblewrap for the `sandboxed` tier. `@v1` is the moving major tag and points here. |
| **reviewer** | `v0.3.0` (`@v1`) | none (stdlib) | — | Advisory reviewer; has no `signetry-core` dependency. It *cross-verifies* the required check without importing the kernel. |
| **eval** | `v0.3.0` | `>= 0.3.0` | `core@v0.8.0` | Needs the capability graph, plan binding, masked verifier, gates and `admit_extension`. Publishes the governance leaderboard, re-measured on release. |
| **plugins** | `v0.3.0` | `>= 0.2.0` | `core@v0.8.0` | The multi-editor bundle (Claude Code, Codex, Cursor, universal guard). Kept alongside the per-agent repos, not superseded by them. |
| **claude-code** | `v0.4.0` | `>= 0.3.0` | `core@v0.8.0` | PreToolUse guard + MCP + `/signetry:admit`. |
| **cursor** | `v0.4.0` | `>= 0.3.0` | `core@v0.8.0` | MCP server + project rule. |
| **codex** | `v0.4.0` | `>= 0.3.0` | `core@v0.8.0` | MCP server + lifecycle-hook guard. |
| **precommit** | `v0.4.0` | `>= 0.3.0` | `core@v0.8.0` | Universal git / pre-commit guard. Use `rev: v0.4.0` in `.pre-commit-config.yaml`. |
| **github-app** | `v0.2.0` | — | — | The App manifest and setup runbook. Comment-only; carries no policy logic — the hosted service governs. |
| **signetry** (hosted) | docs | tracks latest | `core@v0.8.0` | Consumes `signetry-core` directly (no forked governance). |

## Rule

An integration must **pin** its `signetry-core` dependency to a source tag
(`signetry-core @ git+https://github.com/Signetry/core@vX.Y.Z` — signetry-core is
source-available and not on PyPI) and never vendor or fork governance logic. If a
surface needs a new capability, it lands in `signetry-core` first, is released (a git
tag), then the integration bumps its pin here.

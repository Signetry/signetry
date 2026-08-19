# Integrations catalog

Every Signetry surface is its own repository under the Signetry umbrella. All of them
depend on pinned [`signetry-core`](https://github.com/Signetry/core) and never
reimplement governance — they emit or display the same **Admission Decision Pack**.

## Status legend

- **stable** — released, versioned, safe to depend on
- **beta** — usable, API may still shift
- **planned** — designed in the architecture, not yet built

## Catalog

| Repo | Role | Depends on | Status |
|---|---|---|---|
| [**signetry-core**](https://github.com/Signetry/core) | The kernel — the only place governance logic lives: policy, guard, admit, dual verifier, plan binding, G1/G2/G3 gates, passport, receipt, SLSA/transparency, extension admission, CLI, MCP server. Plus a **layered SAST detection engine** (`signetry scan`, 7 languages, cross-file taint, SARIF) and **governed fix fusion** (`signetry scan --fix`, bring-your-own-key, never merges). | — | **stable** |
| [**signetry**](https://github.com/Signetry/core) (hosted) | Production hosted platform / org console at [signetry.github.io](https://signetry.github.io). | signetry-core | **beta** |
| [**signetry-action**](https://github.com/Signetry/action) | GitHub Action + Marketplace required check; posts the canonical PR comment and uploads the signed receipt. | signetry-core | **stable** |
| [**signetry-reviewer**](https://github.com/Signetry/reviewer) | Advisory PR reviewer — finds architecture + security issues, cross-verifies against deterministic gates, recommends safe/needs-human/block. Never merges on its own judgement; optional guarded auto-merge. | — (stdlib) | **beta** |
| [**signetry-plugins**](https://github.com/Signetry/plugins) | Original editor/agent plugins monorepo. Superseded by the per-agent repos below; kept for existing installs. | signetry-core | **beta** |
| [**signetry-github-app**](https://github.com/Signetry/github-app) | GitHub App (PR comments, webhooks) via a short-lived installation token. Manifest + setup; served by the hosted `signetry`. | signetry-core | **beta** |
| [**signetry-claude-code**](https://github.com/Signetry/claude-code) | Claude Code plugin: PreToolUse guard + MCP server + `/signetry:admit` skill. | signetry-core | **beta** |
| [**signetry-cursor**](https://github.com/Signetry/cursor) | Cursor integration: MCP server + project rule. | signetry-core | **beta** |
| [**signetry-codex**](https://github.com/Signetry/codex) | Codex integration: MCP server + lifecycle-hook guard. | signetry-core | **beta** |
| **signetry-copilot** | Copilot / coding-agent integration. | signetry-core | **planned** |
| **signetry-vscode** | VS Code extension. | signetry-core | **planned** |
| [**signetry-precommit**](https://github.com/Signetry/precommit) | Universal git / pre-commit hooks. | signetry-core | **beta** |
| [**signetry-eval**](https://github.com/Signetry/eval) | Public adversarial eval suite — measures ASR + utility-under-defense (IPI, skill/MCP poisoning, MINJA) against the real `signetry-core` pipeline. Also runs the **head-to-head detection benchmark**: a 52-case, 7-language public corpus where `signetry-core` scores **100% recall / 0 false positives** vs a top LLM scanner (Claude Opus 4.8) at 90% — deterministic, offline, free. | signetry-core | **beta** |
| [**homebrew-signetry**](https://github.com/Signetry/homebrew-signetry) | Homebrew tap for the `signetry` CLI (`brew install Signetry/signetry/signetry`). | signetry-core (via PyPI) | **beta** |
| **signetry-demo-repo** | Public demo / judge fixtures. | — | **planned** |

## Integration repo contract

Every child repo must:

1. Live under the Signetry GitHub Org.
2. Be listed here and in [COMPATIBILITY.md](COMPATIBILITY.md).
3. Depend on **pinned** `signetry-core` — never reimplement policy.
4. Emit or display the `AdmissionDecisionPack` (same schema / UX templates).
5. Fail **closed** on admit; a soft guard may fail open only with a loud `INACTIVE`.
6. Never auto-merge.
7. Own its README, `SECURITY.md`, versioning, and CI; link back to this umbrella.

## Which one do I want?

- **Gate every agent PR in CI** → [signetry-action](https://github.com/Signetry/action)
- **Scan a repo for vulnerabilities (7 languages, SARIF) and govern the fix** → [signetry-core](https://github.com/Signetry/core) (`signetry scan .` · `signetry scan . --fix`)
- **Govern an agent inside my editor** → [signetry-plugins](https://github.com/Signetry/plugins)
- **A hosted dashboard for my org** → [signetry](https://signetry.github.io)
- **Embed governance in my own tool / script / hook** → [signetry-core](https://github.com/Signetry/core) (`pip install "signetry-core @ git+https://github.com/Signetry/core@v0.7.0"` — source-available, not on PyPI)

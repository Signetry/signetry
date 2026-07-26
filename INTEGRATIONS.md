# Integrations catalog

Every Umbra surface is its own repository under the Umbra umbrella. All of them
depend on pinned [`umbra-core`](https://github.com/bkd-dotcom/umbra-core) and never
reimplement governance — they emit or display the same **Admission Decision Pack**.

## Status legend

- **stable** — released, versioned, safe to depend on
- **beta** — usable, API may still shift
- **planned** — designed in the architecture, not yet built

## Catalog

| Repo | Role | Depends on | Status |
|---|---|---|---|
| [**umbra-core**](https://github.com/bkd-dotcom/umbra-core) | The kernel — the only place governance logic lives: policy, guard, admit, dual verifier, plan binding, G1/G2/G3 gates, passport, receipt, SLSA/transparency, extension admission, CLI, MCP server. | — | **stable** |
| [**umbra**](https://github.com/bkd-dotcom/umbra) (hosted) | Production hosted platform / org console at [umbra.engineer](https://umbra.engineer). | umbra-core | **beta** |
| [**umbra-action**](https://github.com/bkd-dotcom/umbra-action) | GitHub Action + Marketplace required check; posts the canonical PR comment and uploads the signed receipt. | umbra-core | **stable** |
| [**umbra-plugins**](https://github.com/bkd-dotcom/umbra-plugins) | Editor/agent plugins (Claude Code, Cursor, Codex, universal git hook). Being split into per-agent repos below. | umbra-core | **beta** |
| **umbra-github-app** | GitHub App (PR comments, webhooks) via a short-lived installation token. | umbra-core | **planned** |
| **umbra-claude-code** | Claude Code plugin (split from umbra-plugins). | umbra-core | **planned** |
| **umbra-cursor** | Cursor integration (split from umbra-plugins). | umbra-core | **planned** |
| **umbra-codex** | Codex integration (split from umbra-plugins). | umbra-core | **planned** |
| **umbra-copilot** | Copilot / coding-agent integration. | umbra-core | **planned** |
| **umbra-vscode** | VS Code extension. | umbra-core | **planned** |
| **umbra-precommit** | Universal git / pre-commit hooks (split from umbra-plugins). | umbra-core | **planned** |
| **umbra-eval** | Public adversarial eval suite (optional extract from `umbra-core/evals`). | umbra-core | **planned** |
| **umbra-demo-repo** | Public demo / judge fixtures. | — | **planned** |

## Integration repo contract

Every child repo must:

1. Live under the Umbra GitHub Org.
2. Be listed here and in [COMPATIBILITY.md](COMPATIBILITY.md).
3. Depend on **pinned** `umbra-core` — never reimplement policy.
4. Emit or display the `AdmissionDecisionPack` (same schema / UX templates).
5. Fail **closed** on admit; a soft guard may fail open only with a loud `INACTIVE`.
6. Never auto-merge.
7. Own its README, `SECURITY.md`, versioning, and CI; link back to this umbrella.

## Which one do I want?

- **Gate every agent PR in CI** → [umbra-action](https://github.com/bkd-dotcom/umbra-action)
- **Govern an agent inside my editor** → [umbra-plugins](https://github.com/bkd-dotcom/umbra-plugins)
- **A hosted dashboard for my org** → [umbra](https://umbra.engineer)
- **Embed governance in my own tool / script / hook** → [umbra-core](https://github.com/bkd-dotcom/umbra-core) (`pip install umbra-core`)

# Umbra Platform Architecture

> **Canonical source of truth:** the full architecture document lives at
> [`bkd-dotcom/umbra` → `docs/ARCHITECTURE.md`](https://github.com/bkd-dotcom/umbra/blob/main/docs/ARCHITECTURE.md)
> during the current transition. This page is the umbrella's overview and links
> into it; when the platform stabilizes, the canonical document is promoted here
> as the permanent home.

This overview summarizes the design so the umbrella is self-contained; the linked
document is authoritative wherever they differ.

## Positioning (locked)

**Umbra is the platform. Models/agents are pluggable executors.** It competes with
standards and control planes (admission, attestations, required checks, org
policy) — not with Claude Code / Codex as coding products. Any executor may
*propose* a change; only Umbra may *admit* authority and seal a receipt. The hard
guarantee is at the repository (required check + passport); editor guards are
defense-in-depth.

## The planes

| Plane | Job | Where it lives |
|---|---|---|
| **Policy** | Capability graph: paths, diff budget, required checks, and (v2) tool / bash / MCP / skill allowlists. Fail-closed; policy only restricts. | `umbra-core` (`contract.py`) |
| **Enforcement** | Three choke points — soft guard (editor hook), hard `umbra admit` (CLI/MCP/API), hardest `umbra-action` required check. Plus **plan binding** (CaMeL/DRIFT): a `PlanCapabilitySet` frozen from mission + contract before the executor runs; deviations cap authority. | `umbra-core`, `umbra-action`, plugins |
| **Verification** | The writer never self-approves. A deterministic path (contract, secrets, checks) **and** an independent masked re-check (MELON) that raises a *hijack signal* when a change does what an injection surface pushed for. | `umbra-core` (`verifier.py`) |
| **Authority** | Earned, revocable, run-bound ladder: `L0 observe` / `L1 analyze` / `L2 branch-PR`. Passport binds repo + receipt hash + base commit + executor/config hash + expiry, with an emergency brake. `auto_merge` always false. | `umbra-core` (`passport.py`) |
| **Proof** | **G1** capability integrity · **G2** behavioral authenticity · **G3** interaction auditability. Ed25519 receipt → in-toto/SLSA export → Merkle transparency log. | `umbra-core` (`receipt.py`, `gates.py`, `provenance.py`, `transparency.py`) |
| **Supply chain** | **Admitted Extension**: fingerprint a skill/MCP extension's bytes, quarantine its docs/tool descriptions before ingest, admit/deny against the allowlist, emit a CycloneDX ASBOM. | `umbra-core` (`extension.py`) |
| **Product UI** | A production hosted console (sign-in, multi-repo, admission detail, passports, brake, receipts/audit) rendering the same Admission Decision Pack. | `umbra` (hosted) |

## The result: Admission Decision Pack

One canonical result type across every surface:

```
AdmissionDecisionPack {
  verdict, authority_level, reasons[],
  contract, trust_boundary, checks, verifier,
  plan_capability_set, plan_adherence,
  diff?, receipt, gates (G1/G2/G3), ledger, auto_merge: false
}
```

The CLI prints a human summary; the API/MCP returns the full pack; the Action maps
a subset to outputs + a PR comment (rendered by `umbra comment` in the kernel, so
no surface can invent a stronger claim than the receipt); the hosted UI renders the
same pack.

## Target pipeline (single path, all executors)

```
load CapabilityContract (.umbra/admission.yaml v2)
  → bind PlanCapabilitySet from mission (CaMeL/DRIFT)
  → quarantine untrusted repo text + skill/MCP docs on disk
  → required checks on BASE (isolated worktree)
  → Executor.propose inside a disposable checkout
  → evaluate changeset vs contract (deterministic)
  → required checks on CHANGED tree (sandbox preflight; fail closed)
  → dual verifier (deterministic + masked/independent → hijack signal)
  → grant earned authority L0/L1/L2 (capped on deviation/hijack)
  → seal G1–G3 receipt (Ed25519; provenance + transparency log)
  → passport upsert / brake-aware PR gate
```

## Non-goals

- A first-party coding model to beat Claude/Codex
- Auto-merge at any authority level
- Editor hooks as the hard security boundary
- LLM-as-judge injection detectors as the primary control
- Governance logic forked outside `umbra-core`
- All integrations stuffed into one plugins monorepo
- Orphan repos outside the org / not listed in this umbrella

---

For the complete, current design — personas, UX templates, research anchors, and
the "not a demo" hosted-UI checklist — read the
[canonical architecture document](https://github.com/bkd-dotcom/umbra/blob/main/docs/ARCHITECTURE.md).

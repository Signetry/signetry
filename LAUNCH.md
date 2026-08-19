# Signetry — launch & announcement kit

Shareable, honest copy for announcing Signetry. Every claim here is backed by a
reproducible artifact (a benchmark, a signed receipt, a released package) — no
marketing that outruns the evidence.

---

## Ready-to-post blurbs (copy-paste)

**X / Twitter (≤280 chars)**
> Coding agents can open PRs now. Who decides how much authority each change earned?
>
> Signetry: an admission pipeline that governs any agent's PR and seals the verdict in an Ed25519 receipt. Deterministic SAST too (7 langs, 0-FP).
>
> https://signetry.github.io

**X — alt, seal angle**
> A signet is the seal that authenticates a document. Signetry seals a *verified code change* — earned authority, in a signed receipt. auto_merge is always false; a human merges. Source-available. https://signetry.github.io

**Show HN — title**
> Show HN: Signetry – govern any coding agent's PR and prove it with a signed receipt

**Show HN — first comment**
> Coding agents (Claude Code, Codex, Cursor, Copilot) change repos now, and they read attacker-reachable text (READMEs, issues) that can steer them. I wanted the *merge decision* to be accountable, not vibes.
>
> Signetry runs every change through one deterministic pipeline: executable contract → on-disk quarantine of untrusted text → required checks → an independent verifier the patch-writer can't bypass → earned authority (observe / analyze / branch-PR) → an Ed25519-signed receipt that maps to in-toto/SLSA provenance. Make it a required check and nothing merges without a receipt. `auto_merge` is always false.
>
> It also ships a deterministic, offline SAST engine (`signetry scan`, 7 languages, cross-file taint, SARIF). On a public 52-case benchmark it's 100% recall at 0 false positives.
>
> Source-available (All Rights Reserved), install from source, govern PRs via a GitHub Action. Feedback welcome — especially on the threat model.
>
> Site: https://signetry.github.io · Code: https://github.com/Signetry

**LinkedIn**
> Coding agents can change your repository. The missing piece isn't detection — it's a governed, provable *decision* about how much authority a given change earned.
>
> Signetry is a change-control plane for coding agents: an executable contract, prompt-injection quarantine, an independent verifier, earned authority, and an Ed25519-signed receipt for every decision. Deterministic SAST included (7 languages, 0 false positives on a public benchmark). A human always merges.
>
> Source-available and contributor-friendly under a CLA. → https://signetry.github.io

---

## One-liner

> **Signetry is a change-control plane for coding agents.** It finds vulnerabilities,
> lets an agent draft the fix under a governed admission pipeline, and proves every
> decision with a signed receipt — branch-only, never merged.

## Short post (Show HN / LinkedIn / blog intro)

Coding agents can now change your repository. Signetry is the layer that decides how
much authority a change has *earned* — and proves it.

- **Detect.** `signetry scan` is a deterministic, offline SAST engine across 7
  languages (Python, JavaScript, Go, Java, Ruby, PHP, C#) with cross-file taint and
  SARIF output. On a public 52-case benchmark it hits **100% recall at 0 false
  positives** — matching/leading a top LLM scanner (Claude Opus 4.8 at 90%) while
  staying free and reproducible.
- **Fix, governed.** `signetry scan --fix` hands a finding to a live agent (Codex /
  Claude Code / any adapter, bring-your-own-key), runs the draft through a contract
  → prompt-injection quarantine → required checks → independent verifier, and grants
  only the authority the run earned (L0/L1/L2). L2 opens a **branch-only PR** with an
  Ed25519-signed receipt. `auto_merge` is always false — a human merges.
- **Why it's different.** Detection is table stakes. The moat is the governance:
  earned, revocable authority; on-disk injection quarantine; a verifier the
  patch-writer can't bypass; and a receipt an auditor verifies offline. No scanner
  attempts that.

**Source-available** (All Rights Reserved — *not* open source), on the GitHub
Marketplace. Read it, evaluate it, and contribute under a CLA — the owner retains all
rights, contributors are credited. 10 tagged good-first-issues.

## Reproduce the headline claim

```bash
# source-available; installed from the source repo (not PyPI)
pip install "signetry-core @ git+https://github.com/Signetry/core@v0.7.0"
git clone https://github.com/Signetry/eval && pip install -e signetry-eval
signetry-eval corpus --markdown    # the 52-case, 7-language head-to-head table
signetry scan .                    # scan any repo, offline & free
```

## Links

- **Overview / start here:** https://github.com/Signetry/signetry
- **Kernel (`signetry-core`, source-available):** https://github.com/Signetry/core
- **Benchmark (`signetry-eval`):** https://github.com/Signetry/eval
- **GitHub Action:** https://github.com/marketplace/actions/signetry-admission
- **Contribute — good first issues:**
  https://github.com/Signetry/signetry/issues/10
- **Discuss:** https://github.com/Signetry/signetry/discussions

## Talking to contributors

**Source-available, contribute under a CLA.** The project is All Rights Reserved;
contributors are **credited** (CONTRIBUTORS.md, release notes) but gain no ownership
or right to use/sell it. A bot asks for a one-line CLA signature on the first PR.

The three flagship repos accept real code:

- **signetry-core** — add a detection rule or an executor adapter (highest value).
- **signetry-eval** — add a corpus test case (lowest barrier; each is self-contained).
- **signetry-reviewer** — add a deterministic PR-diff check.

Each has `CONTRIBUTING.md`, `CLA.md`, and `CODE_OF_CONDUCT.md`. Ground rules:
governance stays in `signetry-core`; SAFE cases must stay 0-FP; every change ships with
a test and passes CI; contributions are under the CLA (credited, ownership assigned
to the owner).

## Honesty notes (say these — they build trust)

- Prompt injection is *mitigated*, not solved: bounded + quarantined + dual-verified
  + receipted.
- The optional Semgrep layer can add false positives (its generic rules miss some
  sanitizers); the deterministic engine is 0-FP on the corpus, which is why Semgrep
  is opt-in and non-gating.
- A dev-key receipt proves nothing to a third party (flagged `key_ephemeral`); set a
  production `SIGNETRY_SIGNING_KEY` and pin its public key.
- `auto_merge` is false at every level. Signetry is the governance layer between the
  agent and the human — not a replacement for code review.
- **Source-available, not open source.** The code is public to read and contribute
  to, but it's All Rights Reserved — don't call it "open source." Contributions are
  credited and accepted under a CLA; the owner retains all rights.

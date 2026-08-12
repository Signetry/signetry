# Umbra — launch & announcement kit

Shareable, honest copy for announcing Umbra. Every claim here is backed by a
reproducible artifact (a benchmark, a signed receipt, a released package) — no
marketing that outruns the evidence.

---

## One-liner

> **Umbra is a change-control plane for coding agents.** It finds vulnerabilities,
> lets an agent draft the fix under a governed admission pipeline, and proves every
> decision with a signed receipt — branch-only, never merged.

## Short post (Show HN / LinkedIn / blog intro)

Coding agents can now change your repository. Umbra is the layer that decides how
much authority a change has *earned* — and proves it.

- **Detect.** `umbra scan` is a deterministic, offline SAST engine across 7
  languages (Python, JavaScript, Go, Java, Ruby, PHP, C#) with cross-file taint and
  SARIF output. On a public 52-case benchmark it hits **100% recall at 0 false
  positives** — matching/leading a top LLM scanner (Claude Opus 4.8 at 90%) while
  staying free and reproducible.
- **Fix, governed.** `umbra scan --fix` hands a finding to a live agent (Codex /
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
pip install "umbra-core @ git+https://github.com/Signetry/core@v0.5.4"
git clone https://github.com/Signetry/eval && pip install -e umbra-eval
umbra-eval corpus --markdown    # the 52-case, 7-language head-to-head table
umbra scan .                    # scan any repo, offline & free
```

## Links

- **Overview / start here:** https://github.com/Signetry/signetry
- **Kernel (`umbra-core`, source-available):** https://github.com/Signetry/core
- **Benchmark (`umbra-eval`):** https://github.com/Signetry/eval
- **GitHub Action:** https://github.com/marketplace/actions/umbra-admission
- **Contribute — good first issues:**
  https://github.com/Signetry/signetry/issues/10
- **Discuss:** https://github.com/Signetry/signetry/discussions

## Talking to contributors

**Source-available, contribute under a CLA.** The project is All Rights Reserved;
contributors are **credited** (CONTRIBUTORS.md, release notes) but gain no ownership
or right to use/sell it. A bot asks for a one-line CLA signature on the first PR.

The three flagship repos accept real code:

- **umbra-core** — add a detection rule or an executor adapter (highest value).
- **umbra-eval** — add a corpus test case (lowest barrier; each is self-contained).
- **umbra-reviewer** — add a deterministic PR-diff check.

Each has `CONTRIBUTING.md`, `CLA.md`, and `CODE_OF_CONDUCT.md`. Ground rules:
governance stays in `umbra-core`; SAFE cases must stay 0-FP; every change ships with
a test and passes CI; contributions are under the CLA (credited, ownership assigned
to the owner).

## Honesty notes (say these — they build trust)

- Prompt injection is *mitigated*, not solved: bounded + quarantined + dual-verified
  + receipted.
- The optional Semgrep layer can add false positives (its generic rules miss some
  sanitizers); the deterministic engine is 0-FP on the corpus, which is why Semgrep
  is opt-in and non-gating.
- A dev-key receipt proves nothing to a third party (flagged `key_ephemeral`); set a
  production `UMBRA_SIGNING_KEY` and pin its public key.
- `auto_merge` is false at every level. Umbra is the governance layer between the
  agent and the human — not a replacement for code review.
- **Source-available, not open source.** The code is public to read and contribute
  to, but it's All Rights Reserved — don't call it "open source." Contributions are
  credited and accepted under a CLA; the owner retains all rights.

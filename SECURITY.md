# Security policy

This is the **umbrella** repository: documentation, architecture notes, and the
compatibility matrix. It contains no governance logic. Vulnerabilities in the pipeline
itself — contract evaluation, the guard, the verifier, receipt issuance and
verification — belong against [`Signetry/core`](https://github.com/Signetry/core).

## Reporting

Use **GitHub private vulnerability reporting** on the affected repository:

- Engine, receipts, verifier → [report to `core`](https://github.com/Signetry/core/security/advisories/new)
- CI integration → [report to `action`](https://github.com/Signetry/action/security/advisories/new)
- Anything else, or you are unsure → [report here](https://github.com/Signetry/signetry/security/advisories/new)

Please do **not** open a public issue for an unpatched vulnerability. If you do not get
an acknowledgement within 7 days, open a public issue saying only that you sent a
private report and got no reply — no details.

## What is in scope

- A change that earns authority it should not (contract bypass, path escape, a check
  reported as passing when it did not run).
- A receipt that verifies when it should not: a signature forged, a payload altered
  without detection, or a gate reporting `pass` on absent evidence.
- A receipt that fails to verify when it should — a spec or implementation mismatch is
  also a security bug, because it destroys the audit trail.
- Privilege escalation in the GitHub Action or App beyond `branch_pr_only`.

## What is not in scope

- The deliberate SQL injection in
  [`autofix-demo`](https://github.com/Signetry/autofix-demo) — it is the test fixture.
- The soft, in-editor guard failing open. It is defense-in-depth and says so: it may
  fail open, but only with a loud `INACTIVE` signal. The hard boundary is the required
  check on the pull request plus the signed receipt.
- Findings that require an attacker to already control the repository's Actions
  secrets or branch protection.

## Standing guarantees

- `auto_merge` is always `false`, and it is a **signed field inside every receipt** —
  so "Signetry never merges on its own judgement" is checkable, not promised.
- A gate never reports `pass` on missing evidence. Absent evidence is `unproven`.
- Receipts verify **offline**, against a pinned public key. Verification never requires
  contacting us, and never requires trusting the tool that issued the receipt. See the
  [receipt specification](https://github.com/Signetry/core/blob/main/docs/RECEIPT_SPEC.md).

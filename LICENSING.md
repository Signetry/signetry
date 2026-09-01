# Licensing

Signetry is **open core**. The line is drawn on purpose, and it is drawn in the same
place for every release:

> **Everything you integrate with is Apache-2.0. The engine is source-available and
> converts to Apache-2.0 on 2030-08-31.**

Every public repository in the organization is covered by the table below. If you find
a public Signetry repository with no `LICENSE` file, that is a bug — please open an
issue.

## What that means per repository

| Repository | License | Why |
|---|---|---|
| [`core`](https://github.com/Signetry/core) | **BUSL-1.1** → Apache-2.0 on 2030-08-31 | The admission engine and receipt issuer. Source-available: read it, run it, fork it, patch it. The only prohibition is reselling it as a competing hosted governance service. |
| [`eval`](https://github.com/Signetry/eval) | **Apache-2.0** | The adversarial benchmark. A benchmark nobody can freely run, audit and reproduce is worthless, so this one has no strings at all. |
| [`action`](https://github.com/Signetry/action) | **Apache-2.0** | CI integration. |
| [`plugins`](https://github.com/Signetry/plugins) | **Apache-2.0** | Editor and agent plugins. |
| [`codex`](https://github.com/Signetry/codex) | **Apache-2.0** | OpenAI Codex adapter. |
| [`claude-code`](https://github.com/Signetry/claude-code) | **Apache-2.0** | Claude Code adapter. |
| [`cursor`](https://github.com/Signetry/cursor) | **Apache-2.0** | Cursor adapter. |
| [`precommit`](https://github.com/Signetry/precommit) | **Apache-2.0** | Editor-agnostic git/CI guard. |
| [`github-app`](https://github.com/Signetry/github-app) | **Apache-2.0** | GitHub App manifest and setup. |
| [`autofix-demo`](https://github.com/Signetry/autofix-demo) | **Apache-2.0** | Deliberately vulnerable demo target. |
| [`signetry`](https://github.com/Signetry/signetry) | **Apache-2.0** | This umbrella: docs, architecture, compatibility matrix. |
| [`reviewer`](https://github.com/Signetry/reviewer) | **Apache-2.0** | The advisory PR reviewer installed by the CI workflows. Advisory only — it never merges and never gates. |
| [`homebrew-signetry`](https://github.com/Signetry/homebrew-signetry) | **Apache-2.0** | Homebrew tap formulae. |
| [`signetry.github.io`](https://github.com/Signetry/signetry.github.io) | **Apache-2.0** | The documentation site. |
| [`.github`](https://github.com/Signetry/.github) | **Apache-2.0** | Org profile and shared community-health defaults. |

## Why not Apache-2.0 everywhere?

Because a one-person project that gives away its engine to cloud vendors does not stay
a project for long. BUSL-1.1 keeps `core` readable, runnable, forkable and patchable by
everyone who actually uses it, and stops exactly one thing: a paid competing service
built on it.

The Change Date is not decoration. On **2030-08-31**, `core` becomes Apache-2.0 —
irrevocably, by the terms of the license already published in the repository. Every
release carries its own four-year clock, so the version you install today is
guaranteed to be Apache-2.0 four years from its publication whatever happens to this
project or its author.

## Does BUSL block me?

Almost certainly not. You are explicitly free to:

- read and audit every line
- run `signetry` in your CI, on your laptop, in your build system
- use it **in production** to govern changes to repositories you or your organization control
- fork it, modify it, and publish your modifications
- build and sell a product that *uses* Signetry, as long as the product is not itself a competing governance service

You need a separate arrangement only if you intend to offer change admission, agent
governance, or receipt issuance/verification to third parties as a paid service. If
you are unsure which side of the line you are on, open an issue and ask — a plain
answer is faster for both of us than a lawyer.

## The receipt format is deliberately unencumbered

The [receipt specification](https://github.com/Signetry/core/blob/main/docs/RECEIPT_SPEC.md)
and its [conformance suite](https://github.com/Signetry/core/tree/main/tests/conformance)
are **Apache-2.0**, and the format is versioned independently of the engine. This is
not a footnote: both are named as explicit exclusions from the BUSL `Licensed Work`
parameter in [`core/LICENSE`](https://github.com/Signetry/core/blob/main/LICENSE), so
they carry no restriction and no Change Date.

A receipt is meant to outlive the tool that issued it: an auditor in 2032 must be able
to verify a receipt written in 2026 without running, trusting, or licensing anything
from us. If you want to write a competing issuer or an independent verifier against
the spec, that is a supported use, not a tolerated one — the conformance vectors are
language-agnostic JSON with published test-key seeds precisely so you can check your
implementation against ours.

## Contributions

Contributions to every repository are accepted under the [CLA](https://github.com/Signetry/core/blob/main/CLA.md).

The CLA exists for one practical reason: open core means code sometimes moves across
the line — a community-built adapter that proves itself may belong in the engine. The
CLA lets that happen without tracking down every past contributor for permission.

Be aware of what it actually does, because this is where CLAs differ: it is a
**copyright assignment**, so the maintainer — not you — ends up owning the copyright in
a merged contribution. To the extent an assignment is not permitted by law, it falls
back to a **non-exclusive** licence, deliberately non-exclusive so that you never lose
the ability to use your own work. What you keep either way is the licence's rights:
your contribution ships under that repository's LICENSE, so you may use, modify and
(on the Apache-2.0 repos) commercialize it on exactly the same terms as anyone else.
If assigning copyright is not acceptable to you, say so on the issue before you start
— a DCO-only path for small fixes is a reasonable thing to ask for, and it is easier to
agree before the code is written than after.

## Trademark

"Signetry" and the Signetry mark are not covered by any of the licences above. Fork
the code freely; do not ship a fork under the Signetry name in a way that suggests it
is this project.

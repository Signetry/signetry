# Contributing to Signetry

This is the **umbrella** repository: the platform overview, architecture notes, the
compatibility matrix, and the licensing map. Most code contributions belong in a child
repository — the engine ([`core`](https://github.com/Signetry/core)), the benchmark
([`eval`](https://github.com/Signetry/eval)), or an adapter — but docs fixes here are
very welcome, and a good first PR is
[adding a detection test case to `eval`](https://github.com/Signetry/eval).

## Licensing

This repository is **[Apache-2.0](LICENSE)**. Signetry as a whole is **open core**: the
entire integration surface is Apache-2.0, while the engine is source-available under
BUSL-1.1 and converts to Apache-2.0 on **2030-08-31**. Which repository is licensed how,
and what each licence lets you do, is set out in [LICENSING.md](LICENSING.md).

Short version: you can use Signetry at work, in production, on your own repositories,
without asking anyone. You need a separate arrangement only to resell the engine as a
competing hosted governance service.

## Signing the CLA (required before merge)

This is enforced by a bot. When you open a pull request, the **CLA Assistant** check
will ask you to sign the [Contributor License Agreement](CLA.md). Reply on the PR
with exactly:

```
I have read the CLA Document and I hereby sign the CLA
```

Your acceptance is recorded in `signatures/cla.json`. A PR **cannot be merged** until
the CLA is signed.

**Why an Apache-2.0 project still asks for a CLA.** Signetry is open core, and the line
between the Apache-2.0 integration surface and the BUSL-1.1 engine is not permanent — an
adapter that proves itself may later belong inside
[`Signetry/core`](https://github.com/Signetry/core). The CLA gives the maintainer the
rights to move code across that line and to relicense it (including to Apache-2.0 when
the engine converts in 2030) without tracking down every past contributor. It assigns
copyright in a merged contribution to the maintainer; it does not reduce the rights the
LICENSE grants you. The details, plainly stated, are in
[LICENSING.md](LICENSING.md#contributions).

## Credit

Contributors are **acknowledged** in [CONTRIBUTORS.md](CONTRIBUTORS.md), the Git
history, and release notes. Attribution is separate from trademark: you may freely and
truthfully say you contributed, but please don't present the project as your own work or
brand, or use the Signetry name to endorse your own products. See the "Recognition of
Contributors" clause in [CLA.md](CLA.md).

## Conduct and security

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md). Please report
vulnerabilities privately rather than in a public issue — see [SECURITY.md](SECURITY.md).

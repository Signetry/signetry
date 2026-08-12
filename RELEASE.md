# Release train

Signetry is not a monorepo — each repository releases independently — but governance
capabilities flow in **one direction**, so releases follow a fixed order.

## The order

```
signetry-core  →  integrations (action / plugins / app)  →  hosted (signetry)
   (kernel)          (pin the new signetry-core)              (deploy)
```

1. **signetry-core** ships first. A new capability (a contract field, a verifier
   path, a gate, an extension check) lands, is tested on Python 3.11/3.12/3.13,
   passes its own `self-admission` check, and is released as a **GitHub Release +
   SemVer git tag** with a `CHANGELOG.md` entry (signetry-core is source-available and
   installed from source — not published to PyPI).
2. **Integrations** bump their pinned `signetry-core` (see
   [COMPATIBILITY.md](COMPATIBILITY.md)) and cut their own tags. An integration
   never ships a capability ahead of the kernel that provides it.
3. **Hosted `signetry`** deploys last, consuming the released `signetry-core` and
   surfacing the new fields in the dashboard.
4. Update [INTEGRATIONS.md](INTEGRATIONS.md) status and
   [COMPATIBILITY.md](COMPATIBILITY.md) pins in this umbrella.

## Versioning

- All repos use [SemVer](https://semver.org/). Until `signetry-core` reaches `1.0.0`,
  minor versions may change the public API — integrations pin a minimum and test.
- Actions publish a **moving major tag** (`@v1`) plus exact tags (`@v0.3.0`).
- Never re-tag a released version; cut a new patch instead.

## Invariants that survive every release

- `auto_merge` is false at every authority level and in every signed receipt.
- The soft guard may fail open **only** with a loud `INACTIVE`; admit fails closed.
- Governance logic lives only in `signetry-core`; no integration forks it.
- A capability is available on a surface only after the `signetry-core` release that
  provides it is published and pinned.

## Checklist (per signetry-core release)

- [ ] `CHANGELOG.md` moved from `Unreleased` to the new version + date
- [ ] `pyproject.toml` version bumped
- [ ] tests green on 3.11 / 3.12 / 3.13; `self-admission` green; ruff clean
- [ ] tag `vX.Y.Z` pushed; PyPI publish
- [ ] COMPATIBILITY.md updated in this umbrella
- [ ] dependent integrations' pins bumped and released

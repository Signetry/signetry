# Install Umbra in a day

The fastest path to a **governed, receipted** agent change: add the GitHub Action,
drop a contract, get your first signed receipt. No hosted account required.

## 1. Add the required check (highest-reach choke point)

Create `.github/workflows/umbra.yml` in your repo:

```yaml
name: Umbra Admission
on:
  pull_request:
permissions:
  contents: read
  pull-requests: write   # to post the verdict comment
jobs:
  admit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0   # umbra needs the base commit
      - uses: bkd-dotcom/umbra-action@v1
        with:
          min-authority: "1"   # fail the check below L1 (tune to 2 to require branch-PR)
```

Every PR now gets an **Admission Decision Pack** comment and a signed receipt
uploaded as a workflow artifact. Add the check to branch protection to block merges
without it.

## 2. Drop an executable contract

Create `.umbra/admission.yaml` to declare what a change may touch:

```yaml
version: 2
task_type: dependency-remediation
allowed_paths:
  - "package.json"
  - "package-lock.json"
  - "src/**"
forbidden_paths:
  - ".github/workflows/**"
  - "**/.env*"
  - "**/*secret*"
max_files_changed: 5
required_checks:
  - "npm test"
# Capability graph (v2, optional — omit any line for no extra restriction):
allowed_tools:   [Read, Edit, Bash]
denied_bash:     ["docker\\s+run", "kubectl"]
allowed_mcp:     ["github:search"]
allowed_skills:  ["web-search"]
# Change-control provenance (surfaced honestly in the receipt):
policy_owner: platform-team
policy_version: "1.0"
```

No file? A conservative default contract applies (dependency-manifest scope, small
diff budget). Capabilities can only **restrict** — they never widen authority.

## 3. (Optional) Govern locally + verify the receipt

```bash
pip install "umbra-core>=0.3.0"

# Govern an agent's change on your machine (exits non-zero below branch-PR):
umbra admit . --mission "bump the vulnerable dependency" --agent claude-code \
  --receipt-out receipt.json

# Verify the signed receipt against a pinned key, offline:
umbra verify receipt.json --public-key "$UMBRA_PUBLIC_KEY"

# Read the proof gates and provenance:
umbra gates receipt.json
umbra provenance receipt.json     # in-toto / SLSA statement
```

## 4. (Optional) Govern your agent's extensions

```bash
# Admit or deny a skill / MCP extension before it loads; emit an ASBOM:
umbra admit-extension ./my-skill --repo .            # applies the contract allowlist
umbra admit-extension ./my-mcp-server --asbom --org acme > asbom.json
```

## 5. (Optional) Editor + hosted

- **Editor guard** (allow/deny before a bad edit runs): see
  [umbra-plugins](https://github.com/bkd-dotcom/umbra-plugins).
- **Hosted dashboard** (multi-repo, passports, brake, receipts/audit):
  [umbra.engineer](https://umbra.engineer).

## What you get

- A required GitHub check that fails below your authority bar.
- A canonical PR comment (verdict, contract, trust boundary, checks, verifier,
  proof gates, receipt hash) — identical wherever Umbra runs.
- An Ed25519-signed receipt you can verify offline, forever.
- `auto_merge` is always false. Umbra governs the agent; a human merges.

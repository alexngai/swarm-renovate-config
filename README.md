# swarm-renovate-config

Shared [Renovate](https://docs.renovatebot.com/) preset for the swarm/openhive
ecosystem. Dependency-update policy — especially the **first-party package
group** — lives here once instead of being copy-pasted (and drifting) across
every repo.

## Usage

In each ecosystem repo, add a `renovate.json5` (or `renovate.json`):

```json5
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>alexngai/swarm-renovate-config"]
}
```

That's the whole per-repo config — all policy is inherited from
[`default.json5`](./default.json5).

## What the preset does

- **First-party group** — ecosystem packages (openhive, swarmcraft,
  macro-agent, opentasks, …) are grouped into one PR with no release-age
  delay, so a fresh publish of any of them propagates to every consumer
  within hours.
- **Dev tooling** — grouped, automerged on green CI for patch/minor.
- **Third-party** — grouped patch/minor, held 3 days so a bad publish can be
  yanked first; majors are isolated and never automerged.
- **`@multi-agent-protocol/sdk`** — Renovate is **disabled** for it. MAP
  versions are bumped by hand across the ecosystem.

## Maintenance

When you add a new package to the ecosystem, add it to the
`matchPackageNames` list in `default.json5` **once** — every repo extending
this preset picks it up automatically.

## Prerequisites

The Renovate GitHub App must be installed on every account that owns
ecosystem repos: `alexngai` (and any other org that hosts one).

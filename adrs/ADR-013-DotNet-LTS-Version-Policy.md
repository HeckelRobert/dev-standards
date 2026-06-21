# ADR-013: .NET LTS Version Policy

## Status

Accepted

---

## Context

Platform standards require **.NET LTS** for server-side code. LTS major versions change over time (e.g. .NET 8, .NET 10). Fixing a specific major version in handbook or project requirements becomes outdated and forces unnecessary handbook churn.

Projects need a consistent rule for requirements, architecture, repository pinning, CI, and hosting alignment.

---

## Decision

### Requirements and architecture documents

- State **“.NET LTS”** or **“current .NET LTS at implementation time”**.
- Do **not** fix a major version (e.g. `net8.0`, `net10.0`) in platform standards or generic templates.

### At implementation (scaffold / first deploy)

1. Confirm the active LTS release from the [official .NET support policy](https://dotnet.microsoft.com/en-us/platform/support/policy).
2. Pin the SDK in repository `global.json`.
3. Set `TargetFramework` to matching `netX.0` in all .NET projects.
4. Align CI agents and container/host runtimes to the same LTS major version.
5. Align Azure App Service (or equivalent) Linux runtime major version with the pinned LTS.

### Upgrades

When a new LTS release ships, upgrading is a **planned project activity** (update pin, runtime, CI, hosting), not an automatic handbook change.

---

## Rationale

- Keeps handbook and requirements durable across LTS cycles.
- Makes version choice explicit at the point of execution.
- Avoids mismatch between docs, repo, and Azure runtime.

---

## Alternatives Considered

### Pin major version in platform standards

Rejected — requires handbook updates every LTS cycle; docs drift from “always latest LTS” intent.

### Always use latest STS

Rejected — platform mandates LTS for production stability.

---

## Consequences

- Project `docs/requirements.md` shall include acceptance criteria for LTS confirmation and pinning (see requirements template).
- `docs/architecture.md` shall document the pinned version after scaffold.
- Operations docs shall record hosting runtime major version.

---

## Review Date

Review when Microsoft publishes a new LTS release or support policy changes.

---

## Related Documents

* `standards/technology-selection.md`
* `standards/solution-scaffolding-standard.md`
* `standards/azure-web-application-guide.md`

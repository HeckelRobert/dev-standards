# ADR-015: Tiered LLM Model Selection

## Status

Accepted

---

## Context

Projects integrate LLMs for extraction, classification, and generation. Capable reasoning models are **expensive and slower**; using one premium model for every call (especially on public flows) is often unnecessary and financially risky.

ADR-006 requires provider abstraction; this ADR adds **model tier** guidance within whichever provider the project selects.

---

## Decision

### Default approach

1. **Classify each LLM use case** by required capability (structured extraction, catalog mapping, long-form generation).
2. **Default to the most cost-effective model** that meets quality bar in QA.
3. **Reserve premium models** for steps that fail quality targets with the default tier.
4. **Configure model deployment names** per environment — not hardcoded in business logic.

### Capability tiers (illustrative only)

| Tier | Capability profile | Typical use |
|------|-------------------|-------------|
| **Economy** | Fast, low cost; strong at structured output | JSON extraction, classification, catalog-constrained mapping |
| **Standard** | Better language quality and instruction following | Generation when economy tier fails QA |
| **Premium / reasoning** | Multi-step reasoning, complex analysis | Escalation only — use sparingly |

Provider-specific model IDs are chosen at implementation from the **current provider catalog**. Do not encode model names in platform standards or business logic.

### Cost practices

- Run **deterministic logic first** (rules, catalogs, validation) to reduce tokens.
- Prefer **one LLM call per user journey** where requirements allow.
- Track **token usage per task type** (metrics); set budget alerts.
- Combine with ADR-014 for public endpoints.

### Quality gate

Before production, validate outputs on representative inputs. Escalate tier only with documented evidence in a **project ADR**, not by default.

---

## Rationale

- Aligns spend with business value.
- Keeps upgrade path without provider change.
- Supports ADR-006 abstraction at model configuration layer.

---

## Alternatives Considered

### Single premium model everywhere

Rejected as default — poor cost/latency profile for structured workloads.

### No LLM; rules only

Valid for some features; insufficient when requirements need format-agnostic document interpretation.

---

## Consequences

- `docs/requirements.md` AI section shall note model strategy and cost limits.
- `docs/architecture.md` shall map use cases to tiers.
- Infrastructure implements the provider abstraction interfaces (ADR-006) with configurable model deployment per task type.

---

## Review Date

Review when tier strategy, provider catalog, or cost profile changes materially.

---

## Related Documents

* adrs/ADR-006-AI-Provider-Abstraction.md
* adrs/ADR-014-Public-AI-Endpoint-Abuse-Protection.md
* `standards/observability-standard.md`

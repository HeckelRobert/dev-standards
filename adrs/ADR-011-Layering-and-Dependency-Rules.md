# ADR-011: Layering and Dependency Rules

## Status

Accepted

---

## Context

The platform prefers vertical slices and business-capability namespaces (ADR-010), not root-level technical layer folders.

Architecture tests reference Presentation, Application, Domain, and Infrastructure concerns.

These concerns must be defined so dependency rules are enforceable and consistent with vertical slice organization.

---

## Decision

Logical layers shall exist as **dependency concerns**, not as the primary folder structure.

### Layer Definitions

**Domain**

* Business entities, value objects, domain rules
* No dependencies on Presentation, Infrastructure, or external SDKs

**Application**

* Commands, queries, handlers, validators, application services
* May depend on Domain abstractions
* Must not depend on Presentation or concrete Infrastructure

**Presentation**

* HTTP endpoints, UI, CLI, worker entry points
* May depend on Application (via dispatcher or contracts)
* Must not contain business rules

**Infrastructure**

* Database access, messaging, external APIs, logging providers, AI provider SDKs
* Implements interfaces defined by Application or Domain
* Must not be referenced by Domain

### Dependency Direction

```
Presentation → Application → Domain
Infrastructure → Application / Domain (via interfaces only)
```

Presentation must not depend directly on Infrastructure implementations. Use dependency injection at the composition root.

---

## Rationale

Benefits:

* Reconciles vertical slice folders with testable layering
* Keeps business logic independent of frameworks and providers
* Enables architecture tests (see testing-standard.md)
* Allows slices to colocate Application and Presentation code while respecting boundaries

---

## Alternatives Considered

### Strict physical layer folders

Advantages

* Obvious dependency direction

Disadvantages

* Conflicts with vertical slice colocation
* Encourages anemic domain and god services

Decision

Rejected as primary structure.

---

### No layers

Advantages

* Maximum simplicity

Disadvantages

* Uncontrolled dependencies
* Presentation and database concerns leak into business logic

Decision

Rejected.

---

## Consequences

Projects shall:

* Enforce layer rules with architecture tests
* Define infrastructure implementations behind interfaces
* Register dependencies in composition roots only
* Colocate slice code within modules while respecting logical layer boundaries

Projects shall not:

* Reference EF Core, HTTP clients, or provider SDKs from Domain
* Call repositories directly from Presentation bypassing Application handlers

---

## Review Date

Review when introducing new entry point types (gRPC, workers, agents) or shared libraries.

---

## Related Documents

* standards/testing-standard.md
* adrs/ADR-009-Modular-Monolith.md
* adrs/ADR-010-Vertical-Slice-Architecture.md

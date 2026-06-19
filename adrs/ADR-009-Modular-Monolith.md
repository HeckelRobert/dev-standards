# ADR-009: Modular Monolith

## Status

Accepted

---

## Context

Heckel Platform solutions must balance simplicity, maintainability, operational burden, and AI-assisted development.

Distributed architectures increase coordination cost and are often adopted without clear requirements.

A default architectural style is required so agents and developers make consistent decisions.

---

## Decision

The **Modular Monolith** shall be the default architecture style for new projects.

A modular monolith is a single deployable application organized into explicit modules with clear boundaries and controlled dependencies.

Microservices and distributed monoliths require documented justification before adoption.

---

## Rationale

Benefits:

* Lower operational complexity than distributed systems
* Simpler local development and debugging
* Easier automated testing
* Clear module boundaries without network boundaries
* Better fit for small teams and consultancies
* Easier for AI systems to navigate a single codebase

---

## Alternatives Considered

### Microservices

Advantages

* Independent scaling and deployment
* Organizational boundaries

Disadvantages

* High operational overhead
* Distributed failure modes
* Often premature for initial delivery

Decision

Rejected as default. Allowed when requirements justify it.

---

### Distributed Monolith

Advantages

* Deployment separation without full microservice decomposition

Disadvantages

* Network coupling without independent module evolution
* Operational cost without full microservice benefits

Decision

Allowed only with documented justification.

---

## Consequences

Projects shall:

* Start as a modular monolith unless requirements prohibit it
* Define modules by business capability
* Enforce module boundaries through architecture tests
* Document scaling triggers that would justify distribution

Projects shall not:

* Adopt microservices by default
* Split services without documented requirements

---

## Review Date

Review when independent scaling, deployment, or organizational boundaries become blocking requirements.

---

## Related Documents

* standards/architecture.md
* adrs/ADR-010-Vertical-Slice-Architecture.md
* adrs/ADR-011-Layering-and-Dependency-Rules.md

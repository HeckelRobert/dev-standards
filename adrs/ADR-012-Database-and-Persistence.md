# ADR-012: Database and Persistence

## Status

Accepted

---

## Context

Applications require durable storage. Customers impose different hosting, compliance, and operational constraints.

A default persistence approach is needed without mandating a single database product for all projects.

---

## Decision

### Default

**Relational database** with **Entity Framework Core** is the default persistence approach for business data.

### Preferred databases (evaluate in order)

1. **SQL Server** — Microsoft-first environments, Azure deployments
2. **PostgreSQL** — cross-platform, open source, strong Azure support
3. **SQLite** — local tools, prototypes, embedded scenarios, tests

### Alternatives (require justification)

* **Cosmos DB** — global distribution, document model, specific scale patterns
* **MongoDB** — document model when relational model is a poor fit
* **File storage** — blobs, documents, large binary assets (Azure Blob or equivalent)

### Repository pattern

Data access shall be abstracted behind interfaces defined in Application or Domain.

Handlers depend on abstractions such as `IInspectionRepository`, not `DbContext`, in Application layer code.

`DbContext` and EF configurations belong in Infrastructure.

### Migrations

Schema changes shall be versioned with EF Core migrations (or equivalent for non-EF stores).

Migrations are applied through controlled deployment processes documented in `docs/operations.md`.

---

## Rationale

Benefits:

* EF Core aligns with .NET-first platform
* Relational models fit most business applications
* SQL Server and PostgreSQL cover majority of customer environments
* Interface-based access preserves testability and replaceability

---

## Alternatives Considered

### Dapper only

Advantages

* Performance, explicit SQL

Disadvantages

* More manual mapping and migration discipline
* Higher boilerplate for typical CRUD features

Decision

Allowed for performance-critical paths with justification.

---

### No ORM

Advantages

* Full SQL control

Disadvantages

* Increased maintenance and migration risk

Decision

Rejected as default.

---

## Consequences

Projects shall:

* Document database choice in architecture.md and project ADRs when non-default
* Keep EF Core types out of Domain
* Use migrations for schema evolution
* Support test databases (SQLite or containers) for integration tests

Projects shall not:

* Expose `DbContext` to Presentation
* Store secrets or connection strings in source control

---

## Review Date

Review when compliance, scale, or multi-region requirements change storage constraints.

---

## Related Documents

* standards/technology-selection.md
* standards/security-standard.md
* adrs/ADR-011-Layering-and-Dependency-Rules.md

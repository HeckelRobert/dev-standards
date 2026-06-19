# ADR-007: Repository-Management-Strategy

## Status

Accepted

---

## Context

Multiple customer projects and future products are expected.

Repositories should remain isolated.

Reusable engineering knowledge should be centralized.

---

## Decision

Each software solution shall reside in its own repository.

The Heckel Platform repository serves as the central engineering handbook.

Projects inherit standards but do not directly depend on this repository.

---

## Rationale

Benefits

Independent lifecycle

Independent permissions

Simpler customer handover

Simpler archival

Supports SaaS and custom projects

---

## Consequences

Changes to engineering standards do not automatically affect existing projects.

Projects decide when to adopt updated standards.

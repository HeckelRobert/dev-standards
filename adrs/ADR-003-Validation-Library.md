# ADR-003: Validation Library

## Status

Accepted

---

## Context

Business applications require validation of commands, requests, and input data.

Validation should remain explicit, maintainable, and testable.

---

## Decision

FluentValidation shall be the preferred validation framework.

---

## Rationale

Benefits

Readable syntax

Strong typing

Easy testability

Works well with Vertical Slice Architecture

Good AI compatibility

---

## Alternatives Considered

### DataAnnotations

Advantages

Built into .NET

Disadvantages

Limited expressiveness

Scattered validation logic

Decision

Rejected

---

### Manual Validation

Advantages

No dependency

Disadvantages

Repetitive code

Decision

Rejected

---

## Consequences

Validators should be located close to the features they validate.

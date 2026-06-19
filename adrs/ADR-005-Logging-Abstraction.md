# ADR-005: Logging-Abstraction

## Status

Accepted

---

## Context

Applications require logging.

Logging providers may change over time.

Business logic should remain independent from providers.

---

## Decision

Business code shall only depend on:

ILogger<T>

Logging implementations are infrastructure concerns.

---

## Rationale

Supports:

Serilog

OpenTelemetry

Application Insights

Seq

Console Logging

---

## Alternatives Considered

### Serilog API

Advantages

Powerful features

Disadvantages

Provider coupling

Decision

Rejected

---

### Static Logger

Advantages

Easy to use

Disadvantages

Hard to test

Hard to replace

Decision

Rejected

---

## Consequences

Provider selection occurs in composition roots.

Business modules remain provider agnostic.

# ADR-001: Object Mapping Library

## Status

Accepted

---

## Context

Many software solutions require transformations between different object models.

Examples include:

* Domain Entities to DTOs
* DTOs to Domain Entities
* Commands to Domain Models
* Queries to Response Objects
* API Models to Application Models

The selected mapping approach should support:

* Maintainability
* Readability
* Performance
* AI-assisted development
* Long-term supportability

---

## Decision

Mapster shall be the preferred object mapping library.

Simple mappings may also be implemented manually.

Reflection-based mapping libraries should be avoided.

---

## Rationale

Mapster provides several advantages.

### Compile-Time Code Generation

Mappings can be generated during compilation.

Benefits:

* Better runtime performance
* Earlier detection of mapping issues
* Easier debugging
* Better compatibility with AOT scenarios

### Explicit Configuration

Mapping configuration remains visible and understandable.

Generated code is easier to inspect than runtime-generated mappings.

This improves maintainability and AI-assisted code understanding.

### Reduced Dependency Risk

Mapster is currently available under the MIT license.

It does not impose commercial licensing restrictions.

This reduces vendor dependency risks.

### Better AI Compatibility

AI systems tend to generate more reliable code when mappings are explicit.

Mapster configuration is generally easier for AI systems to understand and modify than convention-based reflection mapping.

---

## Alternatives Considered

### Manual Mapping

Advantages

* No dependency
* Full control
* Maximum transparency

Disadvantages

* Boilerplate code
* Repetitive implementations
* Increased maintenance effort

Decision

Allowed for very small mappings.

---

### AutoMapper

Advantages

* Mature ecosystem
* Broad adoption

Disadvantages

* Reflection based
* Runtime errors possible
* Harder debugging
* Less transparent behavior
* Potential maintainability concerns

Decision

Rejected.

---

### Custom Mapping Framework

Advantages

* Full control

Disadvantages

* Additional maintenance burden
* Reinvents existing solutions

Decision

Rejected.

---

## Consequences

Projects should use Mapster when object mapping becomes non-trivial.

Manual mapping remains acceptable for simple scenarios.

Developers and AI systems should prefer explicit mappings over convention-based mappings.

Generated mapping code should remain reviewable.

---

## Review Date

Review during major .NET upgrades or when Mapster licensing or maintenance changes.

---

## Related Documents

* standards/coding-standard.md
* standards/technology-selection.md
* standards/architecture.md

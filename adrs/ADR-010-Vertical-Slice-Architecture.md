# ADR-010: Vertical Slice Architecture

## Status

Accepted

---

## Context

Traditional layered organization (Controllers, Services, Repositories) scatters feature logic across technical folders.

Vertical Slice Architecture groups code by feature or use case, improving cohesion and AI navigability.

The platform uses an internal command/query dispatcher (ADR-002) to support this style.

---

## Decision

Features shall be organized as **vertical slices** within business modules.

Each slice typically contains:

* Command or Query definition
* Handler
* Validator (when applicable)
* Mapping (when applicable)
* Endpoint or entry point (presentation concern)

Slices are grouped under business capabilities, not technical layers at the root namespace level.

Example structure:

```
src/
  QualityManagement/
    CreateInspection/
      CreateInspectionCommand.cs
      CreateInspectionHandler.cs
      CreateInspectionValidator.cs
      CreateInspectionEndpoint.cs
```

---

## Rationale

Benefits:

* Feature logic is colocated
* Changes affect fewer folders
* Easier onboarding and code review
* Aligns with FluentValidation placement (ADR-003)
* Aligns with internal dispatcher pattern (ADR-002)
* Improves AI context locality

---

## Alternatives Considered

### Traditional Layered Architecture

Advantages

* Familiar to many developers

Disadvantages

* Feature changes span many directories
* Hidden coupling across layers
* Harder for AI to reason about a single feature

Decision

Rejected as primary organization style.

---

### Clean Architecture folders at root

Advantages

* Strong dependency direction

Disadvantages

* Features split across Domain, Application, Infrastructure
* Conflicts with namespace-by-capability guidance

Decision

Rejected at root level. Dependency rules are enforced via ADR-011, not folder names.

---

## Consequences

Projects should:

* Organize namespaces by business capability
* Keep slice-specific code together
* Use the internal dispatcher for commands and queries
* Place validators adjacent to the features they validate

Projects should not:

* Organize root folders purely as Controllers, Services, Repositories
* Scatter a single feature across unrelated modules

---

## Review Date

Review during major architecture refactors or when module count makes slice discovery difficult.

---

## Related Documents

* standards/coding-standard.md
* adrs/ADR-002-Dispatcher-Pattern.md
* adrs/ADR-011-Layering-and-Dependency-Rules.md

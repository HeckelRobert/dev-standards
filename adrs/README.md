# Architecture Decision Records

This directory contains platform-level architecture decisions for Heckel Platform.

Project repositories maintain their own `adrs/` folder for project-specific decisions.

---

# Naming Convention

```
ADR-NNN-Short-Descriptive-Title.md
```

Examples:

* `ADR-001-Object-Mapping-Library.md`
* `ADR-009-Modular-Monolith.md`

Use sequential numbers within each repository. Platform ADRs in this handbook are numbered independently from project ADRs.

---

# Template

New ADRs shall be created from `ADR-TEMPLATE.md`.

Required sections:

* Status
* Context
* Decision
* Rationale
* Alternatives Considered
* Consequences
* Review Date
* Related Documents

---

# Platform ADR Index

| ADR | Title | Status |
|-----|-------|--------|
| ADR-001 | Object Mapping Library | Accepted |
| ADR-002 | Dispatcher Pattern | Accepted |
| ADR-003 | Validation Library | Accepted |
| ADR-004 | Authentication Strategy | Accepted |
| ADR-005 | Logging Abstraction | Accepted |
| ADR-006 | AI Provider Abstraction | Accepted |
| ADR-007 | Repository Management Strategy | Accepted |
| ADR-008 | Documentation Philosophy | Accepted |
| ADR-009 | Modular Monolith | Accepted |
| ADR-010 | Vertical Slice Architecture | Accepted |
| ADR-011 | Layering and Dependency Rules | Accepted |
| ADR-012 | Database and Persistence | Accepted |

---

# Document Precedence

When documents conflict, apply this order:

1. Customer-approved `docs/requirements.md` in the project repository
2. Project-specific ADRs in the project repository
3. Heckel Platform standards (pinned handbook version)
4. Heckel Platform ADRs in this repository
5. Agent role definitions
6. Tool-specific AI instructions

See `standards/standards-governance.md` for versioning and adoption rules.

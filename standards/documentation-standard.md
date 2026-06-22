# Documentation Standard

## Purpose

Documentation should support:

Humans

AI assistants

Autonomous agents

Future developers

Auditors


---

# Required Documentation

Every project shall contain:

docs/

requirements.md

architecture.md

operations.md

security.md


adrs/


ai/


---

# Requirements

Requirements shall describe:

Business goals

Actors

Constraints

Acceptance criteria


---

# Architecture

Architecture documentation shall describe:

Modules

Dependencies

Interfaces

Technology decisions


---

# Operations

Operations documentation shall describe:

Deployment

Backup

Restore

Monitoring

Troubleshooting


---

# Security

Security documentation shall describe:

Authentication

Authorization

Secrets

Data protection


---

# ADRs

Architecture decisions shall be documented.

Examples:

ADR-001 Authentication

ADR-002 Database Selection

ADR-003 Hosting Model


---

# AI Context

Projects shall provide context for AI systems.

Examples:

project-context.md

module-descriptions.md

coding-guidelines.md

testing-guidelines.md


See `standards/standards-governance.md` for handbook versioning and document precedence.

---

# README (repository root)

Every public or customer-facing repository shall include a root **README.md** in **English**.

### Audience order

1. **Business and workshop users first** — what the product does, benefit, quick start (installer, URL, or app access), short demo path. No SDK or clone instructions in this section.
2. **Developers and presenters second** — build from source, tests, publish/installer, CI. Clearly headed (for example *For developers and presenters*).

Use `templates/README.project.md` as the starting point.

### Language

* Repository documentation (README, `docs/`) defaults to **English** unless a project ADR specifies otherwise.
* UI localization is independent; note in README when the live UI defaults to another language.

---

# Demo and pilot deliverables

When the project includes demonstrations or workshops, follow `standards/demo-data-standard.md`.

Desktop and local client distribution follows `standards/desktop-distribution-standard.md` where applicable (not web browser apps).

---
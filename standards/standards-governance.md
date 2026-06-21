# Standards Governance

## Purpose

This document defines how Heckel Platform standards are versioned, adopted, and applied across project repositories.

---

# Handbook vs Project Repositories

The Heckel Platform repository is the central engineering handbook (ADR-007).

Each software solution lives in its own repository.

Projects inherit standards by reference to a pinned handbook version. They do not submodule or package this repository by default.

---

# Document Precedence

When guidance conflicts, apply this order:

1. Customer-approved `docs/requirements.md` in the project repository
2. Project-specific ADRs in the project repository
3. Heckel Platform standards at the pinned handbook version
4. Heckel Platform ADRs at the pinned handbook version
5. Agent role definitions in the handbook
6. Tool-specific AI instructions (Copilot, Cursor, etc.)

---

# Versioning

Handbook releases use semantic versioning tags: `vMAJOR.MINOR.PATCH`.

* **MAJOR** — breaking changes to mandatory standards or ADR decisions
* **MINOR** — new standards, ADRs, or non-breaking clarifications
* **PATCH** — typo fixes, formatting, minor clarifications

Changes are recorded in `CHANGELOG.md`.

---

# Project Adoption

Every project shall record the adopted handbook version in `ai/project-context.md`:

```
Handbook Version: v1.3.1
```

When upgrading:

1. Review `CHANGELOG.md` for the target version
2. Assess impact on the project
3. Update project documentation and ADRs if platform decisions changed
4. Update the pinned version in `ai/project-context.md`

Projects are not required to upgrade immediately. They must not silently diverge without documenting local overrides in project ADRs.

---

# Local Overrides

Projects may override platform standards only when:

* Customer requirements mandate a different approach
* A project ADR documents the override, rationale, and alternatives
* Human approval is obtained

---

# Mandatory Standards Index

| Document | Topic |
|----------|-------|
| standards/api-design-standard.md | HTTP API conventions |
| standards/architecture.md | Architecture styles |
| standards/cicd-standard.md | CI/CD pipelines |
| standards/coding-standard.md | C# and .NET conventions |
| standards/documentation-standard.md | Required documentation |
| standards/frontend-technology-selection.md | UI technology selection |
| standards/observability-standard.md | Logging, metrics, tracing, alerting |
| standards/repository-standard.md | Repository layout |
| standards/requirements-standard.md | Requirements process |
| standards/security-standard.md | Security baseline |
| standards/testing-standard.md | Testing requirements |
| standards/testing-toolchain.md | Testing libraries and patterns |
| standards/technology-selection.md | Technology framework |

### Conditional standards (apply when hosting model matches)

| Document | When to apply |
|----------|---------------|
| standards/azure-web-application-guide.md | Projects hosted on Azure App Service |

---

# Related Documents

* adrs/ADR-007-Repository-Management-Strategy.md
* adrs/README.md
* CHANGELOG.md

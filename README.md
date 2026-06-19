# Development Standards

Opinionated development standards, architectural decisions, and engineering practices for building maintainable software systems with .NET, Azure, and AI-assisted development.

The purpose of this repository is to provide a pragmatic baseline for new projects, reduce recurring technical discussions, and enable consistent implementations across teams and AI agents.

---

## Guiding Principles

- Simplicity over cleverness
- Maintainability over short-term optimization
- Explicitness over convention magic
- Automation wherever possible
- Security by default
- Fast feedback cycles
- AI should accelerate development, not replace engineering judgment

---

# Repository Structure

```text
dev-standards
├── standards/
│   ├── architecture.md
│   ├── coding-standard.md
│   ├── api-design-standard.md
│   ├── testing-standard.md
│   ├── cicd-standard.md
│   ├── security-standard.md
│   ├── observability-standard.md
│   ├── technology-selection.md
│   ├── frontend-technology-selection.md
│   ├── documentation-standard.md
│   ├── repository-standard.md
│   ├── requirements-standard.md
│   ├── solution-scaffolding-standard.md
│   ├── ai-development-process.md
│   ├── agent-governance.md
│   ├── project-lifecycle.md
│   └── standards-governance.md
│
└── adrs/
    ├── ADR-001-Object-Mapping-Library.md
    ├── ADR-002-Dispatcher-Pattern.md
    ├── ADR-003-Validation-Library.md
    ├── ADR-004-Authentication-Strategy.md
    ├── ADR-005-Logging-Abstraction.md
    ├── ADR-006-AI-Provider-Abstraction.md
    ├── ADR-007-Repository-Management-Strategy.md
    ├── ADR-008-Documentation-Philosophy.md
    ├── ADR-009-Modular-Monolith.md
    ├── ADR-010-Vertical-Slice-Architecture.md
    ├── ADR-011-Layering-and-Dependency-Rules.md
    ├── ADR-012-Database-and-Persistence.md
    └── ADR-TEMPLATE.md
```

---

# Standards

These documents describe preferred practices and conventions used across projects.

| Category | Description |
|---------|-------------|
| Architecture | Application architecture and dependency rules |
| Coding | Naming conventions and coding guidelines |
| API Design | REST API design principles |
| Testing | Unit, integration and end-to-end testing |
| Security | Authentication, authorization and secrets handling |
| CI/CD | Build, deployment and release pipelines |
| Observability | Logging, tracing and metrics |
| Documentation | Documentation philosophy and expectations |
| AI Development | Guidelines for AI-assisted software engineering |
| Agent Governance | Rules and responsibilities for autonomous agents |

---

# Architectural Decision Records (ADRs)

Technical decisions are documented using ADRs.

Examples include:

- Object mapping strategy
- Dispatcher implementation
- Validation framework selection
- Authentication approach
- Logging abstraction
- AI provider integration
- Modular monolith architecture
- Vertical Slice Architecture
- Persistence strategy

Each ADR captures:

- Context
- Decision
- Alternatives considered
- Consequences

---

# Intended Usage

This repository can be used as:

- A starting point for greenfield projects
- A baseline for team engineering practices
- Context for AI coding assistants
- Documentation for onboarding developers
- A template for internal engineering playbooks

---

# Contributing

Standards evolve continuously.

Contributions should prioritize:

- Practical experience
- Reduced complexity
- Long-term maintainability
- Proven patterns over trends

---

# Philosophy

> Good standards remove unnecessary discussions.

> Great standards allow humans and AI agents to make the same decisions repeatedly without supervision.

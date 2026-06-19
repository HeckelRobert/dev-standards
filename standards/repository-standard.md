# Repository Standard

## Purpose

This document defines the standard structure used across all repositories.

Consistency is prioritized over project-specific preferences.

---

# Repository Structure

src/
tests/
docs/
adrs/
ai/
infrastructure/
.github/

---

# src

Contains production code.

Structure should reflect business domains and modules.

Technology layers should not drive organization.

Business capabilities should drive organization.

---

# tests

Contains:

* Unit Tests
* Integration Tests
* Architecture Tests
* End-to-End Tests

---

# docs

Contains:

requirements.md
architecture.md
operations.md
security.md

---

# adrs

Contains architecture decision records.

Examples:

ADR-001-Object-Mapping-Library.md
ADR-004-Authentication-Strategy.md
ADR-009-Modular-Monolith.md

Use `adrs/ADR-TEMPLATE.md` for new records. See `adrs/README.md`.

---

# ai

Contains AI-specific context.

Examples:

project-context.md
module-descriptions.md
coding-guidelines.md
testing-guidelines.md

---

# infrastructure

Contains:

Deployment
Provisioning
Containerization
Infrastructure-as-Code

when applicable.

---

# .github

Contains:

Workflows
Issue Templates
Pull Request Templates
Agent Instructions

---

# Mandatory Documentation

Every project must contain:

Requirements
Architecture
Operations
Security
ADR Documentation

No exceptions.

---

# Mandatory AI Context

Every project must provide sufficient context for:

* AI Assistants
* AI Engineers
* Autonomous Agents

to understand the project structure.

Documentation shall be treated as a production asset.

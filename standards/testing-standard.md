# Testing Standard

## Purpose

This document defines testing requirements for all projects.

The objective is to ensure maintainability, confidence during refactoring, and safe AI-assisted development.

---

# General Principles

Business requirements shall be verified through automated tests whenever practical.

Tests shall provide confidence that generated or modified code behaves as expected.

Tests are considered production assets.

---

# Testing Levels

Projects may implement:

- Unit Tests
- Integration Tests
- Architecture Tests
- End-to-End Tests
- Contract Tests
- Approval Tests
- Snapshot Tests
- Mutation Tests

Selection depends on project requirements.

---

# Minimum Requirements

Every project shall contain:

- Unit Tests for business rules
- Integration Tests for external dependencies
- Architecture Tests for dependency validation

---

# Testing Toolchain

See `standards/testing-toolchain.md` for recommended libraries and patterns.

---

# Architecture Tests

Per ADR-011 and `standards/testing-toolchain.md`.

Architecture tests should verify:

Presentation does not depend on Infrastructure

Domain does not depend on Presentation

Modules do not depend on unrelated modules

---

# AI Generated Code

AI generated code must never bypass tests.

New features shall include tests.

Refactorings shall preserve existing tests.

---

# Coverage

Coverage percentages are not targets.

Important business functionality shall be covered.

---

# Test Naming

Tests should follow:

MethodName_WhenCondition_ThenExpectedBehavior

Examples:

CreateCustomer_WhenNameMissing_ReturnsValidationError

ApproveInvoice_WhenUserUnauthorized_ReturnsForbidden
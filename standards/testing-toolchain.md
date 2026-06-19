# Testing Toolchain

## Purpose

This document defines recommended testing libraries and patterns for Heckel Platform projects.

Minimum testing requirements remain in `standards/testing-standard.md`.

---

# Test Framework

### Default

**xUnit** for all test projects.

### Assertions

**FluentAssertions** for readable assertions.

```csharp
result.IsSuccess.Should().BeFalse();
result.Errors.Should().Contain(e => e.PropertyName == "Name");
```

### Mocking

**NSubstitute** or **Moq** — pick one per solution and stay consistent.

Prefer real collaborators in integration tests over excessive mocking.

---

# Unit Tests

Target: Application handlers, validators, domain rules, mappers.

* No database, network, or file system
* Fast execution (milliseconds)
* Deterministic

Organize tests to mirror feature slices:

```
tests/QualityManagement.UnitTests/CreateInspection/
  CreateInspectionHandlerTests.cs
  CreateInspectionValidatorTests.cs
```

---

# Integration Tests

Target: HTTP endpoints, database repositories, message handlers, external service adapters.

### Web API

Use `WebApplicationFactory<TProgram>` from `Microsoft.AspNetCore.Mvc.Testing`.

### Database

Preferred approaches (in order):

1. **SQLite in-memory** — fast, suitable for EF Core tests without provider-specific features
2. **Testcontainers** — real SQL Server or PostgreSQL in CI when SQLite is insufficient
3. **Dedicated test database** — only when containers are not available

Reset database state between tests. Do not share mutable state across parallel tests.

### Test categories

Tag tests for CI filtering per `templates/.github/workflows/ci.yml`:

```csharp
[Trait("Category", "Integration")]
public class CustomerApiTests { }
```

Unit tests omit the Integration category or use `[Trait("Category", "Unit")]`.

---

# Architecture Tests

Use **NetArchTest.Rules** (or equivalent) to enforce ADR-011 layering.

Example rules:

* Types in `*.Domain` do not reference `*.Infrastructure`
* Types in `*.Domain` do not reference `*.Presentation`
* Presentation does not reference Infrastructure directly
* Feature modules do not reference unrelated modules

Place architecture tests in `tests/Architecture.Tests/`.

---

# End-to-End Tests

Use when critical user workflows require full stack verification.

### Web

**Playwright** for browser-based E2E tests.

Keep E2E tests focused on critical paths. They are slower and more brittle than integration tests.

---

# Approval Tests

Use **Verify** (Verify.Xunit) for snapshot and approval testing of:

* HTML or email output
* Serialized API responses
* Report generation

Review snapshot changes carefully in pull requests.

---

# Contract Tests

When services consume or expose contracts consumed by other teams or systems:

* Publish OpenAPI or schema artifacts
* Validate implementations against contracts in CI
* Consider Pact or schema-based contract tests for cross-service boundaries

---

# CI Integration

Test execution order in CI:

1. Unit tests
2. Integration tests
3. Architecture tests
4. E2E tests (optional, may run on schedule or pre-release)

Failed tests block merge. See `standards/cicd-standard.md`.

---

# Related Documents

* standards/testing-standard.md
* adrs/ADR-011-Layering-and-Dependency-Rules.md
* adrs/ADR-012-Database-and-Persistence.md
* templates/ai/testing-guidelines.md

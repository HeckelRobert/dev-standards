# Coding Standard

## Purpose

This document defines coding conventions for all projects.

The objective is to maximize:

* Maintainability
* Readability
* Testability
* AI-assisted development
* Long-term supportability

---

# General Principles

Code is written for humans first.

Code should be easy to understand.

Prefer explicitness over cleverness.

Optimize for maintenance costs.

Avoid unnecessary abstractions.

Prefer composition over inheritance.

Avoid hidden behavior.

Minimize dependencies.

Prefer standard .NET libraries.

---

# Language Version

Use latest stable .NET LTS.

Use latest stable C# language version.

Enable

Nullable Reference Types

Implicit Usings

Analyzers

---

# Naming

Classes

PascalCase

Methods

PascalCase

Properties

PascalCase

Interfaces

Prefix with I

Private fields

_prefixCamelCase

Constants

PascalCase

Namespaces

Reflect business capabilities.

Do not organize by technical layers.

Good

Company.Project.QualityManagement

Bad

Company.Project.Services

---

# Exceptions

Exceptions represent exceptional situations.

Business validation failures shall not use exceptions.

Preferred approaches:

Result Pattern

Error Objects

Validation Results

Examples

Invalid input

ValidationResult

Database unavailable

Exception

Network timeout

Exception

Unauthorized business action

Result Failure

---

# Error Handling

Business validation and expected failure paths shall use explicit result types, not exceptions.

### Preferred patterns

* `Result` / `Result<T>` for command and query outcomes
* `ValidationResult` or structured validation errors from FluentValidation
* Problem Details (RFC 7807) for HTTP API error responses

### Mapping to HTTP

| Outcome | HTTP Status |
|---------|-------------|
| Validation failure | 400 Bad Request |
| Unauthorized | 401 Unauthorized |
| Forbidden business action | 403 Forbidden |
| Not found | 404 Not Found |
| Conflict | 409 Conflict |
| Unexpected failure | 500 Internal Server Error |

### Test expectations

Tests for validation failures should assert on result or response content, not on thrown validation exceptions.

Example test name: `CreateCustomer_WhenNameMissing_ReturnsValidationError`

---

# Vertical Slice

Preferred abstractions:

ICommand<TResponse>

IQuery<TResponse>

ICommandHandler<TCommand,TResponse>

IQueryHandler<TQuery,TResponse>

Use an internal dispatcher.

Avoid MediatR.

Pipeline behaviors may be introduced later.

Examples:

Validation

Logging

Authorization

Transactions

---

# Validation

Preferred library:

FluentValidation

Validators should reside close to features.

Example

CreateInvoiceValidator

ApproveOrderValidator

---

# Mapping

Preferred library:

Mapster

Simple mappings may be performed manually.

Avoid reflection based mappers.

Mappings shall remain explicit.

---

# Dependency Injection

Use constructor injection.

Avoid Service Locator patterns.

Avoid static dependencies.

Dependencies should be registered in composition roots.

---

# Logging

Depend only on:

ILogger<T>

Logging providers are infrastructure concerns.

Business logic should not know logging implementations.

Log levels:

Trace

Debug

Information

Warning

Error

Critical

Sensitive data shall not be logged.

---

# Async Programming

Prefer async APIs.

Avoid blocking calls.

Avoid .Result

Avoid .Wait()

Pass CancellationToken whenever practical.

---

# Configuration

Use strongly typed options.

Validate configuration at startup.

Avoid direct IConfiguration usage.

---

# Documentation

XML documentation shall only be used for:

Public APIs

Shared Packages

SDKs

Complex algorithms

Business rules shall be documented when intent is not obvious.

---

# Testing

Business logic shall be testable.

Prefer deterministic behavior.

Avoid static state.

Avoid hidden dependencies.

---

# AI Generated Code

AI generated code shall:

Compile

Pass tests

Follow naming conventions

Follow architecture standards

Follow security standards

Generated code shall be reviewed by humans.

---

# Package Selection

Prefer Microsoft packages.

Third party packages require justification.

Questions:

Which problem is solved?

What is the maintenance burden?

Can the dependency be replaced?

Will the dependency still exist in five years?

Prefer fewer dependencies.

Avoid dependencies that provide minimal value.

---

# Clean Code

Methods should remain small.

Classes should have one responsibility.

Dependencies should be minimized.

Avoid premature abstractions.

Delete unused code.

Delete dead features.

Simplicity is preferred over theoretical purity.

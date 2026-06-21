# Solution Scaffolding Standard

## Purpose

This document defines how humans and AI systems create new software projects.

Projects shall be scaffolded from requirements.

Projects shall not be scaffolded from predefined technology stacks.

The objective is to produce solutions optimized for business requirements while maintaining engineering consistency.

---

# Supported Modes

Two modes are supported.

## Interactive Mode

AI acts as a consultant.

AI asks questions.

AI proposes architectural decisions.

AI scaffolds the solution after clarification.

Examples:

* Claude Code
* ChatGPT
* OpenClaw

---

## Specification Mode

AI consumes an existing requirements document.

No questions are asked.

AI derives architectural decisions.

AI scaffolds the project.

Examples:

requirements.md

customer-specification.md

project-definition.json

---

# Scaffolding Workflow

Requirements

↓

Architecture Decisions

↓

Technology Selection

↓

Repository Structure

↓

Documentation

↓

GitHub Setup

↓

Project Creation

---

# Information Required

## Business Context

Solution Name

Purpose

Users

Expected lifetime

Compliance Requirements

Deployment Responsibilities

---

## Solution Type

One or multiple may be selected.

Web Application

Desktop Application

Mobile Application

REST API

GraphQL API

gRPC Service

Background Service

Autonomous Agent

Hybrid Solution

---

## Hosting

Azure

AWS

On Premise

Managed Server

Local Execution

Customer Managed

---

## Authentication

Entra ID

Customer Identity Provider

OpenID Connect

Custom

None

---

## Persistence

Relational Database

Document Database

Embedded Database

File Storage

No Persistence

---

## Messaging

None

In Process

Message Broker

Event Streaming

---

## AI Integration

None

External Provider

Azure OpenAI

OpenAI

Local Models

Hybrid

---

## Monitoring

Logging

Metrics

Tracing

Alerting

---

## Testing

Unit Tests

Integration Tests

Architecture Tests

Contract Tests

Approval Tests

Mutation Tests

---

# Repository Structure

Every project shall contain

src/

tests/

docs/

adrs/

ai/

infrastructure/

when applicable

.github/

Only required presentation folders shall be generated.

Examples:

Presentation/Web/

Presentation/Desktop/

Presentation/Mobile/

Presentation/Api/

Presentation/Worker/

Presentation/Agent/

---

# Documentation Generation

The following documents shall always be generated

requirements.md

architecture.md

operations.md

security.md

project-context.md

coding-guidelines.md

testing-guidelines.md

---

# GitHub Integration

Agents shall create

Issue Templates

Pull Request Templates

GitHub Actions

Dependabot Configuration

Security Configuration

Copilot Instructions

Cursor Rules (from `.cursor/rules/` template or project-specific adaptation)

See `templates/.github/` for reference configurations.

---

# .NET LTS pinning (ADR-013)

When scaffolding .NET projects:

1. Confirm current LTS from the official .NET support policy.
2. Add `global.json` at repository root pinning the SDK.
3. Set `TargetFramework` to `netX.0` matching that LTS.
4. Document pinned version in `docs/architecture.md` after scaffold.

Do not hardcode a major version in handbook standards.

---

# Azure web applications

For projects hosted on Azure App Service, follow `standards/azure-web-application-guide.md` when preparing `docs/operations.md`.

---

AI systems may scaffold projects.

AI systems may not approve projects.

Humans remain responsible for:

Architecture

Security

Compliance

Technology Adoption

Deployment

Cost Decisions

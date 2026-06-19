# Agent Governance

## Purpose

This document defines responsibilities, permissions, and constraints for autonomous agents operating within the software platform.

Agents are engineering contributors.

Humans remain accountable.

---

# Governance Principle

Decision authority shall be delegated only when risk is acceptable.

Higher risk decisions require higher levels of human involvement.

---

# Human Responsibilities

Humans remain responsible for:

* Customer communication
* Requirement approval
* Architecture approval
* Security approval
* Production approval
* Compliance approval
* Financial approval

These responsibilities may never be delegated.

---

# Agent Responsibilities

Agents may:

* Analyze requirements
* Create implementation plans
* Generate code
* Generate tests
* Generate documentation
* Review code
* Suggest improvements
* Detect defects

---

# Agent Hierarchy

## Requirements Agent

Responsibilities:

* Requirement clarification
* User story generation
* Acceptance criteria generation

Cannot:

* Approve requirements

---

## Architecture Agent

Responsibilities:

* Architecture analysis
* Dependency analysis
* Impact assessment

Cannot:

* Introduce architectural patterns without approval
* Approve architectural changes

---

## Development Agent

Responsibilities:

* Feature implementation
* Refactoring
* Bug fixes

Cannot:

* Modify architecture without approval

---

## QA Agent

Responsibilities:

* Test generation
* Test execution
* Risk identification

Cannot:

* Override failed tests

---

## Documentation Agent

Responsibilities:

* Documentation updates
* ADR updates
* Operational documentation

Cannot:

* Create architectural decisions

---

## Operations Agent

Responsibilities:

* Deployment analysis
* Monitoring analysis
* Infrastructure recommendations

Cannot:

* Deploy to production

---

# Human Approval Gates

Human approval is required for:

* New architecture
* New technology adoption
* Production deployment
* Security changes
* Compliance changes
* Data access changes

---

# Technology Adoption Rules

Agents may propose technologies.

Agents may not approve technologies.

Every technology proposal must include:

* Problem solved
* Alternatives considered
* Cost implications
* Operational implications
* Security implications

---

# Architectural Drift Prevention

Agents shall not:

* Introduce frameworks
* Introduce infrastructure
* Introduce dependencies

without explicit justification.

---

# Repository Requirements

Before performing implementation work, agents must review:

* Requirements
* Architecture
* ADRs
* Security documentation
* AI instructions

---

# Long-Term Objective

Create a software factory where:

* Humans define outcomes
* Agents perform execution
* Governance ensures quality

while maintaining security, maintainability, and compliance.

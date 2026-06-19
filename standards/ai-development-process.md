# AI Development Process

## Purpose

This document defines how AI systems, coding assistants, and autonomous agents participate in software development.

The objective is to maximize engineering productivity while maintaining software quality, security, maintainability, and compliance.

AI systems are considered engineering contributors.

Humans remain responsible for final approval and accountability.

---

# Core Principle

AI shall assist engineering decisions.

AI shall not replace engineering responsibility.

No AI-generated change may enter production without verification.

---

# Development Workflow

Every feature, bug fix, enhancement, refactoring, or migration follows the same workflow.

## Step 1: Requirement Definition

Input:

* Business requirement
* Bug report
* User story
* Change request

Output:

* Clear implementation objective

---

## Step 2: Planning

An AI planning agent shall produce:

* Requirement summary
* Affected modules
* Risks
* Architecture impact
* Testing requirements
* Documentation impact

No implementation shall begin before a plan exists.

---

## Step 3: Architecture Validation

Before implementation:

Validate:

* Existing architecture
* Module boundaries
* Security implications
* Compliance implications
* Operational impact

Architectural violations must be reported.

---

## Step 4: Implementation

AI may:

* Create code
* Refactor code
* Generate tests
* Update configuration
* Generate documentation

AI must follow:

* Architecture standards
* Coding standards
* Security standards
* Testing standards

---

## Step 5: Automated Verification

All generated code must pass:

* Build validation
* Static analysis
* Unit tests
* Integration tests
* Architecture tests

Failing verification blocks progression.

---

## Step 6: Documentation Update

AI must update:

* Requirements
* ADRs
* Architecture documentation
* Operational documentation

when impacted by changes.

---

## Step 7: Pull Request Creation

AI creates:

* Pull Request
* Change Summary
* Testing Summary
* Risk Summary

AI shall not merge code.

---

## Step 8: Human Review

Human reviewer validates:

* Business requirements
* Architecture compliance
* Security
* Maintainability
* Operational impact

Only humans approve changes.

---

# AI Responsibilities

AI may:

* Generate code
* Generate tests
* Generate documentation
* Create implementation plans
* Analyze repositories
* Suggest architecture improvements
* Review pull requests

AI may not:

* Approve pull requests
* Merge to production
* Access secrets without authorization
* Bypass security controls

---

# Context Requirements

Every repository shall contain:

/docs
/adrs
/ai

AI systems shall use these resources before implementation.

---

# AI Deliverable Requirements

Every implementation must include:

* Code
* Tests
* Documentation
* Risk assessment

Incomplete implementations are considered failed implementations.

---

# Preferred AI Workflow

Requirement
↓
Planning Agent
↓
Architecture Review Agent
↓
Development Agent
↓
QA Agent
↓
Documentation Agent
↓
Pull Request
↓
Human Approval

---

# Long-Term Vision

The software platform shall support increasingly autonomous engineering workflows while maintaining:

* Human oversight
* Security
* Compliance
* Maintainability
* Software quality

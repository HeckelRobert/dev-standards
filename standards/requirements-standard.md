# Requirements Standard

## Purpose

This document defines how requirements are elicited, documented, validated, and maintained.

Requirements are the primary input for software engineering activities.

Requirements shall be understandable by:

* Customers
* Developers
* AI Assistants
* Autonomous Agents
* Auditors

Requirements shall remain technology agnostic whenever possible.

---

# Principles

Requirements describe desired outcomes.

Requirements shall not prescribe implementation details unless explicitly required.

Technology decisions belong to architecture.

Requirements should be testable.

Requirements should be versioned.

Requirements should evolve over time.

---

# Requirement Sources

Requirements may originate from:

* Workshops
* Customer meetings
* Emails
* Support tickets
* Existing software
* Existing documents
* AI-assisted discovery sessions

---

# Requirement Categories

## Business Requirements

Describe business goals.

Examples:

Reduce manual effort

Improve information availability

Increase process transparency

Support compliance

Reduce operational costs

---

## Functional Requirements

Describe expected behavior.

Examples:

Users shall be able to upload documents.

The system shall answer questions based on uploaded documents.

The system shall send notifications.

---

## Non Functional Requirements

Describe quality characteristics.

Examples:

Availability

Security

Performance

Scalability

Maintainability

Observability

Portability

---

## Compliance Requirements

Examples:

GDPR

ISO27001

TISAX

HIPAA

MDR

Customer-specific requirements

---

## Technical Constraints

Examples:

Must use .NET

Must support Azure

Must support On-Premise

Must integrate with SAP

---

# Requirement Lifecycle

Discovery

↓

Clarification

↓

Approval

↓

Implementation

↓

Verification

↓

Operation

↓

Improvement

---

# Discovery Process

AI systems shall act as consultants.

Questions shall be asked incrementally.

Large questionnaires should be avoided.

Topics:

Business Context

Users

Processes

Compliance

Hosting

Security

Data

Integrations

AI Requirements

Monitoring

Operations

---

# Requirement Template

# Overview

Project Name

Purpose

Customer

Stakeholders

---

# Business Goals

Goal 1

Goal 2

Goal 3

---

# Users

Administrators

Operators

Customers

Guests

---

# Functional Requirements

FR-001

Description

Priority

Acceptance Criteria

---

# Non Functional Requirements

NFR-001

Description

Priority

---

# Compliance

Requirement

Reason

---

# Hosting

Preferred Hosting

Allowed Hosting

Deployment Responsibility

---

# Authentication

Preferred Authentication

Alternative Authentication

---

# Persistence

Preferred Persistence

Alternative Persistence

---

# Messaging

Required

Optional

Not Required

---

# AI Requirements

Provider Restrictions

Data Classification

Allowed Models

Prompt Logging

Cost Limits

Audit Requirements

---

# Monitoring

Logs

Metrics

Tracing

Alerts

---

# Acceptance Criteria

Requirement

Expected Behaviour

Verification Method

---

# Open Questions

Question

Owner

Status

Due Date

---

# AI Behaviour

AI systems shall:

Ask clarifying questions

Identify ambiguities

Suggest alternatives

Identify risks

Suggest missing requirements

AI systems shall not:

Invent requirements

Assume technologies

Ignore compliance constraints

Ignore operational implications

Ignore costs

---

# Completion Criteria

Requirements are complete when:

Business goals are understood

Acceptance criteria exist

Compliance requirements are known

Deployment model is known

Authentication strategy is known

Operational responsibilities are known

Open questions are resolved

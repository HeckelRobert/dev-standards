# Technology Selection Framework

## Purpose

This document defines how technologies are selected.

Technology choices must be based on requirements.

No technology is mandatory unless explicitly defined by platform standards.

---

# Mandatory Standards

The following technologies are mandatory:

## Language

* C#
* Supported .NET LTS Version

## Frontend

See `standards/frontend-technology-selection.md`

## Source Control

* Git
* GitHub

## Authentication Preference

* Microsoft Entra ID

When requirements allow.

## CI/CD

Automated build and verification pipelines are required.

## Documentation

Documentation is mandatory.

## Automated Testing

Automated verification is mandatory.

---

# User Interface

Question:

Does the solution require a user interface?

Options:

* Web
* Desktop
* Mobile
* Hybrid
* No UI

Selection shall be based on user requirements.

---

# API Strategy

Question:

Does the solution require an API?

Evaluate:

* REST
* GraphQL
* gRPC

Selection Criteria:

REST

* Default choice
* Public APIs
* Business applications

GraphQL

* Complex client-specific data requirements

gRPC

* High-performance internal communication

---

# Real-Time Communication

Question:

Does the solution require real-time updates?

Evaluate:

* SignalR
* WebSockets
* Server Sent Events
* Polling

Selection shall be based on latency, complexity, and operational requirements.

---

# Data Storage

Question:

What data must be stored?

Evaluate:

* SQL Server
* PostgreSQL
* SQLite
* Cosmos DB
* MongoDB
* File Storage

Selection shall consider:

* Data structure
* Scale
* Compliance
* Hosting model
* Operational burden

---

# Messaging

Question:

Is asynchronous communication required?

If no:

No broker.

If yes evaluate:

* Azure Service Bus
* RabbitMQ
* Kafka
* Event Hub

Selection Criteria:

Service Bus

* Microsoft-first enterprise environments

RabbitMQ

* General-purpose messaging

Kafka

* High-volume event streaming

Event Hub

* Telemetry and event ingestion

---

# AI Providers

Evaluate:

* Azure OpenAI
* OpenAI
* Local Models
* Future Providers

Selection Criteria:

* Data sensitivity
* Compliance requirements
* Cost
* Performance
* Hosting requirements

---

# Hosting

Preferred order:

1. Azure
2. Customer Requirement
3. Alternative Cloud Provider
4. On-Premise

Hosting decisions shall consider:

* Compliance
* Cost
* Operational effort
* Customer preference

---

# Technology Approval Rule

Every major technology decision must answer:

1. Which requirement does it solve?
2. What alternatives were considered?
3. What are the costs?
4. What are the operational implications?
5. What are the long-term maintenance implications?
6. Can it be replaced later?

If these questions cannot be answered, the technology should not be adopted.

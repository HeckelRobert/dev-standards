# Frontend Technology Selection

## Purpose

This document defines how user interface and client technologies are selected for Heckel Platform projects.

Backend services follow the .NET-first platform standard. Frontend selection is requirement-driven.

---

# Decision Process

1. Confirm that a user interface is required.
2. Identify target platforms: Web, Desktop, Mobile, or Hybrid.
3. Evaluate non-functional requirements: offline support, performance, distribution model, team skills, customer constraints.
4. Document the decision in `architecture.md` and an ADR when the choice is non-obvious or costly to reverse.

---

# Web Applications

## Default

Blazor when the team is .NET-centric and UI complexity is moderate.

## Alternatives

Angular when:

* Rich SPA requirements exist
* Large frontend team or long-lived SPA maintenance is expected
* Customer mandates Angular or existing Angular assets must be integrated

React or other frameworks when customer requirements, existing codebases, or staffing explicitly favor them.

## Selection Criteria

* Team skills
* Customer preference
* Integration with existing systems
* Offline and performance needs
* Long-term maintenance burden
* AI-assisted development support

---

# Desktop Applications

Evaluate in order:

1. **.NET MAUI** — cross-platform desktop with shared .NET backend skills
2. **WPF** — Windows-only, mature enterprise desktop
3. **Electron or web shell** — when reusing a web UI is the primary goal

---

# Mobile Applications

Evaluate in order:

1. **.NET MAUI** — shared logic with .NET backend
2. **Native (Swift, Kotlin)** — when platform-specific UX or performance is mandatory
3. **Hybrid (Capacitor, WebView shell)** — when reusing web UI is the primary goal

---

# API-Only Solutions

No frontend framework is required.

Clients may be third-party systems, mobile apps maintained elsewhere, or autonomous agents.

---

# Shared Principles

Regardless of frontend technology:

* Business logic remains on the server
* Authentication integrates with the platform authentication strategy (see ADR-004)
* API contracts are documented (OpenAPI where applicable)
* Frontend code is organized by feature or business capability where practical
* Sensitive data is not stored in client storage without explicit approval

---

# Approval

Major frontend technology adoption requires human approval.

Agents may propose options but may not approve technology choices.

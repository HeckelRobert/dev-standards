# ADR-004: Authentication-Strategy

## Status

Accepted

---

## Context

Projects require authentication mechanisms.

Customers may impose specific requirements.

Preferred ecosystem is Microsoft.

---

## Decision

Microsoft Entra ID shall be the preferred authentication provider.

Authentication mechanisms must remain replaceable.

---

## Preferred Order

1. Entra ID

2. Customer Identity Provider

3. OpenID Connect

4. Keycloak

5. Custom Authentication

---

## Rationale

Benefits

Microsoft ecosystem integration

Enterprise readiness

Compliance support

Single Sign-On

Managed identities

Conditional Access

---

## Alternatives Considered

Auth0

Keycloak

Custom Authentication

---

## Consequences

Applications shall depend on authentication abstractions.

Authentication providers shall not leak into business logic.

---

## Public consumer applications

Enterprise login (Entra ID) is **not** mandatory when requirements define a **public, anonymous entry point**.

For such applications:

* Document the chosen authentication or access mechanism in `docs/requirements.md` and `docs/security.md`.
* When external LLM calls are involved, apply **ADR-014** (abuse and cost controls — mechanism is project-specific).

Entra ID remains the preferred choice for workforce, authenticated B2B, and enterprise scenarios.

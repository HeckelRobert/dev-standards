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

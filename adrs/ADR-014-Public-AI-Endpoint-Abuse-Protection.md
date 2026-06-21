# ADR-014: Public AI Endpoint Abuse Protection

## Status

Accepted

---

## Context

Applications that expose **public, unauthenticated** endpoints calling **paid external LLMs** face cost and abuse risk: automated traffic, repeated trials, and unauthenticated use can generate unbounded token spend.

Enterprise authentication (Entra ID) is not always appropriate for public entry points. Technical controls must be chosen per project requirements and documented in the project repository.

---

## Decision

When **all** of the following apply, projects shall document and implement **abuse and cost controls before LLM invocation**:

1. Endpoint is reachable without enterprise login.
2. Endpoint triggers external LLM usage.
3. Per-request cost is non-trivial or aggregate cost is unbounded.

### Control categories (select per project)

| Category | Examples (non-prescriptive) | Purpose |
|----------|----------------------------|---------|
| **Access gating** | Enterprise IdP, customer IdP, invite-only, API keys, proof-of-identity flows | Ensure only intended users trigger LLM calls |
| **Bot mitigation** | CAPTCHA, bot management services | Reduce automated abuse |
| **Rate limiting** | Per IP, per session, per identity, per API key | Cap request volume |
| **Server enforcement** | Authorization policies on LLM endpoints | Prevent client bypass |
| **Cost monitoring** | Provider or cloud budget alerts | Detect runaway spend |

The **specific mechanism** (e.g. Entra ID B2C, magic link, payment gate) is a **project decision** recorded in `docs/requirements.md`, `docs/security.md`, and a project ADR when non-obvious.

### When Entra ID still applies

Internal apps, operator consoles, and enterprise B2B products continue to follow ADR-004 (Entra ID preferred).

---

## Rationale

- Establishes platform expectation without prescribing customer-specific UX.
- Prevents runaway AI cost on public surfaces.
- Keeps authentication strategy requirement-driven.

---

## Alternatives Considered

### Prescribing a single verification pattern (e.g. email OTP)

Rejected — too specific for a multi-customer handbook; belongs in project requirements.

### CAPTCHA only

Insufficient as sole control when human abuse is likely.

### No protection; rely on budgets only

Reactive; does not prevent incident-scale spend.

---

## Consequences

- Requirements shall include NFRs for abuse and cost control when public LLM endpoints apply.
- Architecture shall identify which endpoints invoke LLMs and which controls apply.
- Security and operations docs shall cover rate limits and budget alerts.
- Do not log secrets or verification codes.

---

## Review Date

Review when adding new public AI surfaces or changing authentication model.

---

## Related Documents

* adrs/ADR-004-Authentication-Strategy.md
* adrs/ADR-006-AI-Provider-Abstraction.md
* adrs/ADR-015-Tiered-LLM-Model-Selection.md
* `standards/security-standard.md`

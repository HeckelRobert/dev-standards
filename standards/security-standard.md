# Security Standard

## Purpose

Define baseline security requirements for all Heckel Platform projects.

Security is considered from project inception. See `docs/vision.md`.

---

# Authentication

Preferred provider:

Microsoft Entra ID

Alternative providers may be selected per ADR-004.

Authentication shall be configurable and replaceable.

Authentication mechanisms must not leak into business logic.

---

# Authorization

Role based authorization preferred.

Claims based authorization recommended.

Authorization rules shall be documented in `docs/security.md`.

Enforce authorization in Application layer handlers or dispatcher pipeline behaviors, not only at HTTP boundaries.

---

# Secrets

Secrets shall never be stored in repositories, issue comments, or pull requests.

Secrets shall be retrieved at runtime from approved stores:

* Azure Key Vault
* AWS Secrets Manager
* Customer-approved secret management
* Environment variables (development only; not for production secrets)

### Rotation

Document secret rotation procedures in `docs/operations.md`.

* API keys and service credentials: rotate at least annually or on compromise
* Certificates: rotate before expiry with automated monitoring
* Database credentials: use managed identities where possible to reduce static credentials

---

# Dependency and Supply Chain Security

Dependencies shall be scanned for known vulnerabilities in CI.

Use GitHub Dependabot or equivalent. See `templates/.github/dependabot.yml`.

### Vulnerability response

| Severity | Action |
|----------|--------|
| Critical | Address within 7 days |
| High | Address within 30 days |
| Medium | Address in next maintenance window |
| Low | Track and address when convenient |

Document exceptions with risk acceptance and expiry date in a project ADR.

### Package selection

Prefer packages with active maintenance, clear licensing, and low known vulnerability history.

Review new dependencies in pull requests. See `standards/coding-standard.md` package selection.

---

# Threat Modeling

Perform threat modeling when any of the following apply:

* New external-facing API or UI
* Processing of personal or regulated data
* New third-party integration
* AI features that send data to external providers
* Significant authentication or authorization changes

### Minimum threat model output

Document in `docs/security.md` or a project ADR:

* Assets and trust boundaries
* Entry points
* Top threats (STRIDE categories)
* Mitigations and residual risks

Optional tooling: Microsoft Threat Modeling Tool, OWASP Threat Dragon, or structured markdown.

---

# OWASP Baseline

Web applications and APIs shall address OWASP Top 10 risks as applicable:

* Broken access control — enforce authorization in Application layer
* Cryptographic failures — TLS in transit, encryption at rest for sensitive data
* Injection — parameterized queries (EF Core), validate all input
* Insecure design — threat modeling, least privilege
* Security misconfiguration — secure defaults, no debug endpoints in production
* Vulnerable components — dependency scanning
* Authentication failures — use established IdP, secure session/token handling
* Data integrity failures — verify CI/CD pipeline integrity
* Logging failures — audit security events without logging secrets
* SSRF — validate outbound URLs when user input influences requests

---

# Auditability

Security relevant actions should be auditable.

Examples:

* Authentication success and failure
* Authorization failures
* Administrative actions
* Data export and deletion
* AI interactions involving customer data

Audit logs shall include timestamp, actor, action, and target. Retention per compliance requirements.

---

# AI Usage

### Data handling

Sensitive information shall not be transmitted to external LLM providers without explicit customer approval.

Classify data before sending to AI providers:

| Classification | External LLM |
|----------------|--------------|
| Public | Allowed |
| Internal | Requires approval |
| Confidential | Prohibited unless anonymized and approved |
| Personal / Regulated | Prohibited unless contract and DPA allow |

### User transparency

Users must be informed when external LLMs process their data.

### Configuration

Model and provider selection shall remain configurable per environment.

Log AI interactions for audit when requirements demand it. Do not log full prompts containing secrets or personal data.

### Cost and abuse

Implement rate limiting and cost controls for AI endpoints. See `standards/observability-standard.md`.

---

# Data Protection

Only required data should be persisted.

Personal data shall be removable on request (GDPR right to erasure where applicable).

Retention periods shall be configurable and documented.

Encrypt sensitive data at rest when stored in shared or cloud infrastructure.

Minimize personal data in logs, traces, and AI prompts.

---

# Incident Response

Document in `docs/operations.md`:

* Contact path for security incidents
* Steps to revoke compromised credentials
* Steps to isolate affected systems
* Customer notification procedure when required by contract or regulation

Security incidents involving personal data may trigger regulatory notification obligations.

---

# Related Documents

* adrs/ADR-004-Authentication-Strategy.md
* adrs/ADR-006-AI-Provider-Abstraction.md
* standards/api-design-standard.md
* standards/observability-standard.md
* standards/cicd-standard.md

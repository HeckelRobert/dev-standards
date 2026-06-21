# Observability Standard

## Purpose

This document defines logging, metrics, tracing, health monitoring, and alerting requirements for Heckel Platform projects.

Observability is mandatory for production systems. See `docs/vision.md`.

---

# General Principles

Production systems must be diagnosable without attaching a debugger.

Observability data must not contain secrets, credentials, or unnecessary personal data.

Use platform abstractions in business code. See ADR-005 (`ILogger<T>`).

Provider selection (Application Insights, OpenTelemetry exporters, Seq) is an infrastructure concern.

---

# Logging

### Business code

Depend only on `ILogger<T>`.

### Structured logging

Use structured log messages with named properties, not string interpolation of sensitive values.

```csharp
_logger.LogInformation("Inspection {InspectionId} created for customer {CustomerId}", id, customerId);
```

### Log levels

| Level | Use for |
|-------|---------|
| Trace | Detailed diagnostic flow (disabled in production by default) |
| Debug | Development diagnostics |
| Information | Normal business events, request completion |
| Warning | Recoverable issues, degraded behaviour |
| Error | Failures requiring attention |
| Critical | Service-threatening failures |

### Required log context

Include where practical:

* Correlation or trace ID
* Authenticated user or service principal (not PII beyond what operations require)
* Request path or operation name
* Duration for significant operations

### Prohibited in logs

* Passwords, tokens, API keys
* Full credit card or payment data
* Unredacted personal data beyond operational need

---

# Metrics

Expose metrics for:

* Request rate and latency (per endpoint or operation)
* Error rate
* Dependency call duration (database, external APIs)
* Background job success and failure counts
* AI token usage and cost-related counters when AI is used

Prefer OpenTelemetry metrics API. Export via Application Insights, Prometheus, or customer-approved backends.

Use consistent naming: dot-separated lowercase.

```
http.server.request.duration
db.client.operation.duration
ai.completion.tokens.total
```

---

# Tracing

Production systems should support distributed tracing.

Use OpenTelemetry for trace instrumentation.

Propagate trace context across HTTP calls and message handlers.

Instrument:

* Incoming HTTP requests
* Outgoing HTTP client calls
* Database operations
* Message publish and consume
* AI provider calls

---

# Health Checks

Every deployable service shall expose health endpoints.

| Endpoint | Purpose | Exposure |
|----------|---------|----------|
| `/health/live` | Process is running | Orchestrator / load balancer |
| `/health/ready` | Ready to accept traffic (DB, dependencies) | Orchestrator / load balancer |

Projects using URL versioning may use `/api/v1/health` (or similar) — document the canonical probe path in `docs/operations.md`.

Register dependency checks for database, message broker, and critical external services. **Do not** call paid external LLMs on every health probe.

### Azure App Service

Enable **Health check** in the App Service blade after first deploy; point to the same path as `/health/ready` or a dedicated liveness path.

See `standards/azure-web-application-guide.md`.

Health check failures should appear in monitoring and alerting.

---

# Alerting

Define alerts in `docs/operations.md` for at minimum:

* Health check failures
* Elevated error rate (5xx)
* Elevated latency (p95 threshold per project)
* Dependency unavailability
* Disk or memory thresholds (when self-hosted)
* AI cost anomalies (when AI is used)
* LLM cost or rate-limit threshold breaches (when AI is used — ADR-014)

Alerts must be actionable. Every alert has an owner and a documented response step.

Avoid alert fatigue: prefer SLO-based alerts over raw log grepping.

---

# Local Development

Developers shall be able to view logs locally without cloud dependencies.

Console logging is sufficient for local development.

OpenTelemetry export to local collectors is optional.

---

# AI Workloads

When AI providers are used, track:

* Request count and latency
* Token usage (input and output)
* Error rate by provider and model
* Estimated cost per operation where possible

See ADR-006 and `standards/security-standard.md` for data handling rules.

Apply ADR-014 (abuse protection) and ADR-015 (tiered models) for public or high-volume AI features.

---

# Related Documents

* adrs/ADR-005-Logging-Abstraction.md
* adrs/ADR-006-AI-Provider-Abstraction.md
* standards/architecture.md
* templates/docs/operations.md

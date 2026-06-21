# Azure Web Application Guide

## Purpose

Reusable checklist for Heckel Platform projects hosted on **Azure App Service** (Linux) with .NET LTS, optional SPA frontend, Key Vault, Application Insights, and common supporting services.

Adapt per project `docs/requirements.md` and `docs/architecture.md`. Not every project needs every step.

---

# Prerequisites

* Azure subscription with Contributor on target resource group
* DNS access when using custom domains
* LLM or other AI services (if required by requirements)
* Naming convention agreed for the project

---

# Recommended resource order

| Step | Resource | Notes |
|------|----------|-------|
| 1 | Resource group | Single region for MVP |
| 2 | Log Analytics workspace | Foundation for Insights |
| 3 | Application Insights | **One** instance per environment; link to workspace |
| 4 | Key Vault | Secrets; soft-delete recommended |
| 5 | LLM provider service (if required) | Model tier per ADR-015; provider per ADR-006 |
| 6 | Outbound messaging (e.g. ACS Email) | Only if requirements need email/SMS |
| 7 | App Service plan (Linux) | B1+ for custom domains and Always On |
| 8 | Web App (.NET LTS major) | Match pinned LTS from ADR-013 |
| 9 | Custom domain + TLS | CNAME + App Service managed certificate |
| 10 | Managed Identity RBAC | Key Vault Secrets User; service-specific roles |
| 11 | Budget alerts | On cost-sensitive services (e.g. AI) |

---

# App Service (.NET LTS)

| Setting | Recommendation |
|---------|----------------|
| OS | Linux |
| Runtime | Current .NET **LTS** major (see ADR-013) |
| Platform release channel | **Standard** for production |
| HTTPS only | On |
| Minimum TLS | 1.2 |
| System-assigned Managed Identity | On |

Confirm runtime:

```bash
az webapp list-runtimes --os linux | findstr -i dotnet
```

---

# Application Insights — single instance

**Common mistake:** Creating App Insights in step 2, then enabling Insights on the Web App with **Create new** — results in two instances.

**Correct approach:**

1. Create one Application Insights resource linked to Log Analytics.
2. Web App → Application Insights → **Link to existing resource**.
3. Delete orphan duplicate after verifying telemetry in Live metrics.

---

# Health checks

### Application (required)

Per `standards/observability-standard.md`:

| Endpoint | Purpose |
|----------|---------|
| `/health/live` | Process running |
| `/health/ready` | Ready for traffic (optional dependency checks) |

Versioned APIs may use a different path — document the **probe path** in `docs/operations.md`.

### Azure App Service (recommended)

**Monitoring → Health check** → enable after first deploy → path matches app health endpoint.

---

# Custom domain and SSL

| URL | Certificate |
|-----|-------------|
| `https://<app>.azurewebsites.net` | Azure default (automatic) |
| Custom domain (e.g. `app.example.com`) | DNS validation + **App Service managed certificate** |

Steps: add custom domain → CNAME to `*.azurewebsites.net` → validate → managed cert binding (SNI).

---

# Key Vault and Managed Identity

1. Enable system-assigned identity on App Service.
2. Grant **Key Vault Secrets User** on the vault.
3. Store secrets in Key Vault; reference from App Service settings:

   `@Microsoft.KeyVault(SecretUri=https://<vault>.vault.azure.net/secrets/<name>/)`

4. Grant additional roles per integration (document in `docs/operations.md`).

Never commit secrets to Git.

---

# Public AI endpoints

If requirements include **public, unauthenticated LLM usage**, document abuse and cost controls per **ADR-014** and model tiering per **ADR-015** in the project repository.

---

# Post-MVP items

* Custom email domain verification (when using transactional email)
* Azure Front Door or WAF
* Staging deployment slot
* Infrastructure as Code (Bicep/Terraform)

---

# Related Documents

* adrs/ADR-013-DotNet-LTS-Version-Policy.md
* adrs/ADR-014-Public-AI-Endpoint-Abuse-Protection.md
* adrs/ADR-015-Tiered-LLM-Model-Selection.md
* `templates/docs/operations.md`
* `standards/observability-standard.md`
* `prompts/deployment-readiness.md`

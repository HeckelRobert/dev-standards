# CI/CD Standard

## Purpose

This document defines minimum continuous integration and delivery requirements for Heckel Platform projects.

Automated pipelines are mandatory. See `standards/technology-selection.md`.

---

# General Principles

Every change is built and verified before merge.

Pipelines must be deterministic and repeatable.

Secrets are never stored in workflow files or repositories.

Failed verification blocks merge.

Humans approve production deployment.

---

# Required Pipeline Triggers

Pipelines shall run on:

* Pull requests targeting the main branch
* Pushes to the main branch

Optional:

* Scheduled dependency and security scans
* Manual deployment workflows

---

# Required Build Steps

Every pipeline shall execute at minimum:

1. **Restore** dependencies
2. **Build** all solution projects in Release configuration
3. **Dependency vulnerability scan** — see below; **must fail the pipeline** when High or Critical vulnerabilities are reported for referenced packages (including transitive). See `standards/security-standard.md`.
4. **Unit tests**
5. **Integration tests** (when present; required before Phase 2 pilot graduation)
6. **Architecture tests** (when present; required before Phase 2 pilot graduation)

### Vulnerability scan (.NET)

Use:

```bash
dotnet list package --vulnerable --include-transitive
```

* `continue-on-error` must be **false** for this step.
* Do not ship release artifacts while High or Critical findings remain unless documented risk acceptance exists in a project ADR with expiry.

---

# Recommended Steps

* Static analysis / code analyzers
* Code coverage reporting (informational only; not a merge gate)
* Container image build (when applicable)
* Publish deployment artifacts

---

# Branch Policy

* `main` is protected
* Pull requests require successful pipeline execution
* Pull requests require at least one human approval
* Direct pushes to `main` are discouraged

Feature branches should be short-lived.

Naming convention: `feature/`, `fix/`, `chore/` prefixes are recommended.

---

# Deployment

### Non-Production

Automated deployment to development or staging environments is encouraged after merge to `main`.

### Production

Production deployment requires:

* Successful pipeline on the release commit
* Human approval (Technical Director or delegate)
* Updated `docs/operations.md` when deployment process changes

Agents shall not deploy to production.

---

# Secrets and Configuration

Use GitHub Actions secrets or customer-approved secret stores.

Never commit:

* Connection strings
* API keys
* Certificates
* Tokens

Environment-specific configuration is injected at deployment time.

---

# Templates

Reference workflow templates are provided in `templates/.github/workflows/`.

Projects shall adapt templates to their solution structure and hosting model.

---

# Agent Responsibilities

Agents may:

* Propose workflow changes
* Fix failing pipelines
* Add test steps when new test projects are introduced

Agents may not:

* Disable required verification steps without approval
* Add secrets to the repository
* Configure production deployment without human approval

---

# Related Documents

* standards/testing-standard.md
* standards/security-standard.md
* standards/solution-scaffolding-standard.md
* `templates/.github/workflows/ci.yml`

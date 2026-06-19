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
3. **Unit tests**
4. **Integration tests** (when present; required before Phase 2 pilot graduation)
5. **Architecture tests** (when present; required before Phase 2 pilot graduation)

---

# Recommended Steps

* Static analysis / code analyzers
* Dependency vulnerability scanning (see `standards/security-standard.md`)
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

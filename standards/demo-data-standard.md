# Demo Data Standard

## Purpose

Projects that include demonstrations, pilots, or workshops shall ship **realistic sample data** so stakeholders can evaluate value without production data, manual setup, or developer tooling.

This standard applies to any solution type when a demo path is part of delivery (desktop, web, API with sample payloads, etc.).

---

# Principles

* Sample data must look **credible to domain experts** — not empty shells or single-line placeholders.
* Demos must work **out of the box** after install or first run (bundled data, sensible defaults).
* Document a **short demo script** (for example 5 minutes) in the project README.
* Never use real customer data in the repository.

---

# Content Requirements

When sample data is included:

| Area | Requirement |
|------|-------------|
| **Structured metadata** | Machine-readable descriptors (JSON, seed scripts, fixtures) with realistic fields — not only title and identifier. |
| **Documents** | PDF or file samples with **multi-line, domain-appropriate content** (drawings, offers, work instructions), not blank or one-line stubs. |
| **Coverage** | Enough variety to show matching, filtering, or search (multiple records/projects where applicable). |
| **Flagship scenario** | One primary demo path documented end-to-end (input → result → reuse). |

---

# Generation and Maintenance

* Provide scripts to **regenerate** synthetic documents or seed data as part of build/publish pipelines where files are generated.
* Keep sample data **versioned in the repository** or produced deterministically in CI/publish — not hand-copied ad hoc.
* When schema changes, update sample data and document **re-index or rescan** steps in `docs/operations.md`.

---

# README and Presentation

* Top of README: what the demo proves for **business stakeholders** (benefit, not technology).
* Include step-by-step demo instructions in **English**.
* Separate **developer/presenter** section (build, test, publish) below the business content.

---

# Related Documents

* standards/documentation-standard.md
* standards/desktop-distribution-standard.md (when the demo is a desktop installer)
* standards/solution-scaffolding-standard.md

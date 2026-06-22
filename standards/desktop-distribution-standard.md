# Desktop Distribution Standard

## Purpose

Define how **desktop and local client applications** are packaged for end users who are not developers.

**Does not apply** to:

* Web applications consumed in the browser
* Mobile store distribution (follow platform store guidelines)
* APIs or background services without a desktop UI

---

# End-User Expectations

Non-technical users expect:

* A **normal application name** in Start Menu / desktop (display name, not repository or namespace)
* An **application icon**
* **One obvious way to start** the app — not `.bat` files, shell scripts, or `dotnet run`
* **Installer-based setup** where appropriate (Windows: MSI preferred for business workshops and IT-managed PCs)

---

# Windows Desktop (Default)

When targeting Windows 10/11 desktop:

| Item | Requirement |
|------|-------------|
| **Installer** | Provide an **MSI** (or equivalent Windows installer) for workshop and pilot delivery unless a project ADR documents otherwise. |
| **Shortcuts** | Start Menu shortcut; **desktop shortcut** when appropriate for the scenario. |
| **Icon** | Application icon (`.ico`) on executable, shortcuts, and installer. |
| **Display name** | Use the product display name in UI, installer, and shortcuts (for example **Quotation Accelerator**). Use technical project/namespace names only in code and repository. |
| **Self-contained runtime** | Publish self-contained or framework-dependent per `docs/operations.md`; users must not install the .NET SDK. |
| **Assets at runtime** | Icons and content copied to output (`CopyToOutputDirectory` or equivalent) — verify cold start on a clean machine. |

Portable ZIP-only distribution is acceptable for **internal developer smoke tests**, not as the primary deliverable for business demos.

---

# Other Desktop Platforms

macOS and Linux desktop projects shall document distribution in `docs/operations.md` (DMG/pkg, AppImage, etc.) using the same principles: icon, clear launcher, installer or store-appropriate package.

---

# Demo and Sample Data

Desktop pilots that demonstrate document or project reuse shall follow `standards/demo-data-standard.md` (realistic bundled `sample-data/`, scripted PDFs or fixtures, documented demo path).

---

# CI and Publish

* Publish/installer build steps shall be **scripted and repeatable** (for example `scripts/publish-installer.ps1`).
* Document output paths in `docs/operations.md` and the README **developer section**.
* Run vulnerability scan before release artifacts (see `standards/cicd-standard.md`).

---

# Related Documents

* standards/demo-data-standard.md
* standards/cicd-standard.md
* standards/security-standard.md
* standards/solution-scaffolding-standard.md

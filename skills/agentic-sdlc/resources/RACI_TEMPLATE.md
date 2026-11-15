<!-- asdlc_version: "3.0.0" | distribution_tier: "customer-safe" -->
# 🛡️ Program & 8-Stage HITL Gate RACI Matrix (`RACI.md`): `<Project / Application Title>`

- **Project:** `<Project / Application Title>`
- **Schema Version:** `3.0.0`
- **Managed By:** `@project-conductor` (Stage 1 Upfront RACI Spreadsheet Intake & Continuous PMO Overwatch)
- **Starter Google Sheet Template (Make a Copy):** [A/SDLC v3.0 Stage 1 RACI & Gate Approval Roster](https://docs.google.com/spreadsheets/d/1KZ4mN9t8sEU3--lyKkg5zlCUtqUJ-Vnobfdu6qMBL80/copy)
- **Local Starter Templates:** `.okf/intake/raci/RACI_STARTER_TEMPLATE.xlsx` and `.okf/intake/raci/RACI_STARTER_TEMPLATE.csv`
- **Governance Invariant:** AI subagents may be Responsible (`R`), Consulted (`C`), or Informed (`I`), never Accountable (`A`). Every stage gate (`1..8`) requires strictly one Accountable human role. Custom `3..N` enterprise role rosters are supported.
- **Authenticated Surfaces (`TEAM_STRICT`, `2+` Distinct Humans):** `GITHUB_ISSUES_PR` (`GITHUB_ISSUE`), `GOOGLE_SHEETS_TRACKER` (`GOOGLE_SHEETS`), or `FLIGHT_DECK_UI` (`DEPLOYED_FLIGHT_DECK`). Only the Accountable (`A`) human can approve a gate; any `R`, `A`, or `C` human on that gate can request changes.
- **How to Approve or Request Changes (Plain-English Cheat Sheet):**
  - **Where to find the commit SHA:** Every dispatched GitHub Gate Issue and Google Sheet Assigned Comment includes the exact pre-filled approval line with the 12+ character commit SHA so business and engineering approvers can copy and paste it directly.
  - **Approve (`A` owner only):** Post an unedited comment or reply such as `APPROVED G1 9f8e7d6c5b4a` (use `G1` through `G8` plus the 12+ character commit SHA). **Do not edit a posted comment afterward** (`createdAt == updatedAt` is enforced to block tampering; if you make a typo, post a fresh comment instead of editing).
  - **Request Changes (`R`, `A`, or `C` participant):** Post `CHANGES_REQUESTED: Add retry timeout to Section 4`. This taints that commit SHA and holds your notes in quarantine (`.sdlc/rework/gate_<N>_changes_requested.json`) until an operator explicitly reviews and confirms them for rework (either directly in chat in Pure Markdown mode or via `python3 scripts/sdlc_hud.py --confirm-rework <N>` when CLI scripts are installed).
- **Mid-Project Updates:** Unapproved gates can switch between the 3 authenticated surfaces without changing `raci_sha256` once the `A` owner's target email or GitHub handle is locked. Roster edits to `RACI.md` and `.sdlc/raci.json` can be proposed via Pull Request at any stage, gated by `.github/CODEOWNERS` and Stage 1 Sponsor / Repository Admin approval.

## 1. Enterprise Roles & Assigned Team Roster (Default 6 Roles; Custom `3..N` Supported)

| Role ID | Enterprise Role Title | Assigned Individual | Corporate Email | GitHub Handle | Department / Function |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `executive_sponsor` | **Executive Sponsor / Business Owner** | Executive Sponsor (`@executive-sponsor`) | `executive-sponsor@enterprise.local` | `@executive-sponsor` | Business Unit Leadership |
| `product_owner` | **Agile Product Owner** | Product Owner Lead (`@product-owner-human`) | `product-owner@enterprise.local` | `@product-owner-human` | Product Management |
| `lead_architect` | **Lead AI / Systems Architect** | Principal Systems Architect (`@lead-architect`) | `lead-architect@enterprise.local` | `@lead-architect` | Enterprise Architecture |
| `tech_lead` | **Full-Stack Engineering Tech Lead** | Full-Stack Tech Lead (`@tech-lead`) | `tech-lead@enterprise.local` | `@tech-lead` | Application Engineering |
| `security_lead` | **Security & Governance Lead (CISO Delegate)** | Cloud Security Architect (`@security-lead`) | `security-lead@enterprise.local` | `@security-lead` | Cybersecurity & AI Governance |
| `sre_finops_lead` | **Quality, SRE & FinOps Lead** | Platform SRE & FinOps Lead (`@sre-finops-lead`) | `sre-finops@enterprise.local` | `@sre-finops-lead` | Site Reliability & Cloud FinOps |

## 2. Program & 8-Stage HITL Gate RACI Assignment Matrix

| Gate / Stage | Accountable (`A`) Sign-Off Owner | Responsible (`R`) AI Subagents | Approval Channel | Executive Sponsor | Agile Product Owner | Lead AI Architect | Full-Stack Tech Lead | Security Lead | Quality SRE & FinOps Lead |
| :--- | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Program Overall Governance & Release Charter** | Executive Sponsor | `@project-conductor` | `PROJECT_DEFAULT` | **A** | R | C | C | C | I |
| **Stage 1: Project Onboarding, RACI & Asset Intake** | Executive Sponsor | `@project-conductor` | `PROJECT_DEFAULT` | **A** | R | C | I | I | I |
| **Stage 2: Product Discovery & Requirements (`PRD.md`)** | Agile Product Owner | `@product-owner` | `PROJECT_DEFAULT` | C | **A** | C | I | I | I |
| **Stage 3: Technical Design & API Blueprint (`SPEC.md`)** | Lead AI Architect | `@spec-architect` | `PROJECT_DEFAULT` | I | C | **A** | R | C | C |
| **Stage 4: Workspace & Guardrail Setup (`AGENTS.md`)** | Lead AI Architect | `@parallel-builder-orchestrator + @spec-architect + @project-conductor` | `PROJECT_DEFAULT` | I | I | **A** | R | C | C |
| **Stage 5: Parallel Backend & Frontend Coding** | Full-Stack Tech Lead | `@parallel-builder-orchestrator` + `.sdlc/agents/builders/*.md` | `PROJECT_DEFAULT` | I | C | C | **A** | I | I |
| **Stage 6: Automated Security & Code Review** | Security Lead | `@security-governance-critic` | `PROJECT_DEFAULT` | I | I | C | R | **A** | C |
| **Stage 7: Testing, Quality & Cost Check** | Quality SRE & FinOps Lead | `@eval-telemetry-auditor` | `PROJECT_DEFAULT` | I | C | I | R | I | **A** |
| **Stage 8: Continuous Improvement & Next Iteration** | Agile Product Owner | `@kaizen-evolution-agent + @project-conductor` | `PROJECT_DEFAULT` | C | **A** | C | C | I | R |

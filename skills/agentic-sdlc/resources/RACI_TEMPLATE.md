<!-- asdlc_version: "3.0.0" | distribution_tier: "customer-safe" -->
# 🛡️ Program & 8-Stage HITL Gate RACI Matrix (`RACI.md`) — <Project / Application Title>

- **Project:** `<Project / Application Title>`
- **Schema Version:** `2.0.0`
- **Managed By:** `@project-conductor` (Stage 1 Onboarding & Continuous PMO Overwatch)
- **Governance Invariant:** AI subagents may be Responsible (`R`), Consulted (`C`), or Informed (`I`), never Accountable (`A`). Every stage gate requires exactly one Accountable human role.

## 1. Six Core Enterprise Roles & Assigned Team Roster

| Role ID | Enterprise Role Title | Assigned Individual | Department / Function |
| :--- | :--- | :--- | :--- |
| `executive_sponsor` | **Executive Sponsor / Business Owner** | Executive Sponsor (`@executive-sponsor`) | Business Unit Leadership |
| `product_owner` | **Agile Product Owner** | Product Owner Lead (`@product-owner-human`) | Product Management |
| `lead_architect` | **Lead AI / Systems Architect** | Principal Systems Architect (`@lead-architect`) | Enterprise Architecture |
| `tech_lead` | **Full-Stack Engineering Tech Lead** | Full-Stack Tech Lead (`@tech-lead`) | Application Engineering |
| `security_lead` | **Security & Governance Lead (CISO Delegate)** | Cloud Security Architect (`@security-lead`) | Cybersecurity & AI Governance |
| `sre_finops_lead` | **Quality, SRE & FinOps Lead** | Platform SRE & FinOps Lead (`@sre-finops-lead`) | Site Reliability & Cloud FinOps |

## 2. Program & 8-Stage HITL Gate RACI Assignment Matrix

| Gate / Stage | Accountable (`A`) Sign-Off Owner | Responsible (`R`) AI Subagents | Approval Channel | Executive Sponsor | Agile Product Owner | Lead AI Architect | Full-Stack Tech Lead | Security Lead | Quality SRE & FinOps Lead |
| :--- | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Program Overall Governance & Release Charter** | Executive Sponsor | `@project-conductor` | `PROJECT_DEFAULT` | **A** | R | C | C | C | I |
| **Stage 1: Project Onboarding, RACI & Asset Intake** | Executive Sponsor | `@project-conductor` | `PROJECT_DEFAULT` | **A** | R | C | I | I | I |
| **Stage 2: Product Discovery & Requirements (`PRD.md`)** | Agile Product Owner | `@product-owner` | `PROJECT_DEFAULT` | C | **A** | C | I | I | I |
| **Stage 3: Technical Design & API Blueprint (`SPEC.md`)** | Lead AI Architect | `@spec-architect` | `PROJECT_DEFAULT` | I | C | **A** | R | C | C |
| **Stage 4: Workspace & Guardrail Setup (`AGENTS.md`)** | Lead AI Architect | `@spec-architect + @project-conductor` | `PROJECT_DEFAULT` | I | I | **A** | R | C | C |
| **Stage 5: Parallel Backend & Frontend Coding** | Full-Stack Tech Lead | `@fastapi-backend-builder` & `@vue-tailwind-frontend-builder` | `PROJECT_DEFAULT` | I | C | C | **A** | I | I |
| **Stage 6: Automated Security & Code Review** | Security Lead | `@security-governance-critic` | `PROJECT_DEFAULT` | I | I | C | R | **A** | C |
| **Stage 7: Testing, Quality & Cost Check** | Quality SRE & FinOps Lead | `@eval-telemetry-auditor` | `PROJECT_DEFAULT` | I | C | I | R | I | **A** |
| **Stage 8: Continuous Improvement & Next Iteration** | Agile Product Owner | `@kaizen-evolution-agent + @project-conductor` | `PROJECT_DEFAULT` | C | **A** | C | C | I | R |

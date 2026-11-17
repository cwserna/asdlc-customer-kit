---
name: org-standards-builder
asdlc_version: "3.1.0"
distribution_tier: "customer-safe"
description: >-
  Standalone Enterprise Organizational Standards Builder and Intranet Distiller
  (/org-standards-builder). Helps customers and Customer Engineers (CEs) turn hundreds of
  scattered internal website pages, Confluence/SharePoint wikis, PDFs, or unwritten tribal
  knowledge into a clean, two-tier A/SDLC v3.1 standards package: a slim, deterministic
  org-standards.md (<= 120 lines) pinned for Stages 1 to 8 plus deep domain reference manuals in
  .okf/runbooks/, including mandated Stage 6 security scanners and Stage 7/8 monitoring tools for
  .sdlc/toolchain_config.json. Supports 3 intake modes (Mode 1: Intranet Harvester Prompt / Bulk
  File Ingest, Mode 2: Guided Portal Scavenger Hunt, Mode 3: Expert Architect Interview), filters
  out non-code bureaucratic process noise, and grills the human 2 to 3 questions per turn on
  contradictions, hard numeric thresholds, tribal knowledge, and application profile scoping.
  Trigger whenever the user invokes /org-standards-builder, org-standards-builder, or asks to
  create, distill, harvest, or customize an org-standards.md file from internal standards.
---

# Enterprise Organizational Standards Builder (`org-standards-builder`)

This standalone skill helps enterprise teams and Customer Engineers (CEs) build a clean, code-enforceable **`org-standards.md`** and **`.okf/runbooks/`** catalog without drowning in hundreds of internal wiki pages or playing 20 Questions from memory.

It is **100% decoupled from `/agentic-sdlc`** so customers can run it before Stage 1 onboarding, inside any standalone repository, or as a copy-paste prompt inside Gemini Enterprise and NotebookLM. Its output is formatted to slot directly into **A/SDLC v3.0 (Stages 1 to 8)** and `.okf/manifest.yaml`.

### Companion Files in This Skill Package
* **Copy-Paste Intranet Harvester Prompt (For Gemini Enterprise / NotebookLM / Copilot):** [`prompts/INTRANET_HARVESTER_PROMPT.md`](./prompts/INTRANET_HARVESTER_PROMPT.md)
* **Zero-Install Copy-Paste Architect Prompt (For Browser Chat UIs):** [`prompts/STANDALONE_ARCHITECT_PROMPT.md`](./prompts/STANDALONE_ARCHITECT_PROMPT.md)
* **Stack-Agnostic `org-standards.md` Template (A/SDLC v3.0 Stages 1 to 8):** [`resources/ORG_STANDARDS_TEMPLATE.md`](./resources/ORG_STANDARDS_TEMPLATE.md)
* **Master `.okf/runbooks/INDEX.md` Template:** [`resources/RUNBOOK_INDEX_TEMPLATE.md`](./resources/RUNBOOK_INDEX_TEMPLATE.md)
* **CE & Customer Field Guide:** [`README.md`](./README.md)

---

## Core Design Principles (Why This Exists)

1. **Never Force Humans to Recite an Intranet from Memory:** When a customer has hundreds of standards on an internal website (SharePoint, Confluence, Backstage, ServiceNow, or an internal portal), do not start with open-ended interview questions. Ingest or harvest the written pages first, then grill the human only on conflicts, gaps, and application scoping.
2. **Never Hardcode Vendor Demo Stacks:** An `org-standards.md` file must reflect the **customer's actual technology stack, identity provider, security rules, testing gates, and observability tools**. Never insert unrequested vendor products or demo frameworks unless the customer confirms they use them.
3. **Protect Stages 2 to 8 from Context Rot (The Two-Tier Split):**
   * **Tier 1 (`org-standards.md`, strictly `<= 120 lines`):** Pinned in `.okf/manifest.yaml` and loaded into every prompt across Stages 1 to 8. Contains only deterministic, code-enforceable rules that alter how `PRD.md`, `SPEC.md`, `AGENTS.md`, application code, and automated tests are written and audited.
   * **Tier 2 (`.okf/runbooks/<domain>.md`):** Deep reference standards (database naming conventions, approved Terraform modules, compliance control matrices, UI token tables) stored by domain so coding and review agents load them only when needed.
   * **Tier 3 (`PROCESS_NOISE`, Discarded to `.okf/runbooks/DISCARDED_PROCESS_LOG.md`):** Non-code bureaucracy (Change Advisory Board meeting schedules, Jira ticket workflows, HR training policies, legacy mainframe standards) that an AI coding agent cannot enforce in source code.

---

## Step-by-Step Execution Runbook

### Phase 1: Turn 1 Intake Mode Selection (`ask_question`)

When invoked, immediately greet the user and call `ask_question` with these two questions to select the intake track and target output path:

1. **Question 1 (How are your internal standards stored right now?):**
   * `(Recommended) Mode 1: Bulk File Ingest or Intranet Harvester Prompt (We have an internal standards site, exported files, or an enterprise AI search tool)`
   * `Mode 2: Guided Portal Scavenger Hunt (I have our internal standards website open in my browser; tell me what to search and paste domain by domain)`
   * `Mode 3: Expert Architect Interview (We want to define our org-standards.md from scratch by answering targeted engineering questions)`
2. **Question 2 (Are we building a Master Org Catalog, an Application-Specific Profile, or both?):**
   * `(Recommended) Both: Build the reusable Master Catalog (.okf/runbooks/) and distill a slim <=120-line org-standards.md for our target application`
   * `Master Org Baseline Only: Create our company-wide .okf/runbooks/ catalog and a baseline org-standards.md template for future teams`
   * `Single Application Only: Distill an org-standards.md tailored to one specific application we are about to build`

---

### Phase 2: Execute the Chosen Intake Mode

#### Track A: Mode 1 (Bulk File Ingest or Intranet Harvester Prompt)
Ask the user whether they already have local files (or a reachable URL/directory) ready to read, or if their standards site is locked behind corporate SSO:
* **If local files or a directory exist:** Use `read_file` or `run_command` to scan all provided Markdown, HTML, TXT, CSV, or PDF exports.
* **If the standards site is open in a local debug browser:** Offer to read the open tabs or sitemap via Chrome DevTools MCP (`list_pages`, `evaluate_script`) if available.
* **If the hundreds of standards live on an SSO-gated intranet (SharePoint, Confluence, Backstage, Internal Wiki):**
  1. Display the ready-to-copy prompt from [`prompts/INTRANET_HARVESTER_PROMPT.md`](./prompts/INTRANET_HARVESTER_PROMPT.md) in a fenced code block.
  2. Instruct the user to paste that prompt into **Gemini Enterprise, Vertex AI Search, NotebookLM, M365 Copilot, or Glean** (connected to their internal standards site) and paste the resulting `RAW_STANDARDS_EXTRACT.md` output back into the chat (or save it to disk).

#### Track B: Mode 2 (Guided Portal Scavenger Hunt)
When the user only has a web browser open to a massive internal website and no bulk export tool, guide them through **5 focused scavenger rounds** (one domain at a time). In each round, give them exact search keywords to type into their internal portal search bar and ask them to paste the raw text (or summary) of the top 1 to 3 matching pages:
1. **Round 1 (Languages, Frameworks & API Contracts):** Ask them to search their portal for `approved tech stack`, `reference architecture`, `API standards`, `REST`, `gRPC`, `OpenAPI`.
2. **Round 2 (Authentication, IAM, Secrets, Mandated Security Scanners & Input Security):** Ask them to search for `authentication`, `OAuth`, `OIDC`, `service accounts`, `secret management`, `SQL injection`, `AI safety`, `DLP`, `SAST`, `Wiz`, `Snyk`, `SonarQube`, `Semgrep`, `CodeQL`, `Veracode`, `Checkmarx`, `SARIF`.
3. **Round 3 (Database, Data Privacy & External Integrations):** Ask them to search for `database standards`, `schema migrations`, `data classification`, `PII`, `encryption`.
4. **Round 4 (Code Quality, Testing Thresholds & CI/CD Gates):** Ask them to search for `unit test coverage`, `code review checklist`, `PR size`, `static analysis`, `linter`, `container scanning`, `secret scanning`.
5. **Round 5 (Logging, OpenTelemetry, Approved APM/Monitoring Tools & Cloud Cost):** Ask them to search for `logging standard`, `OpenTelemetry`, `OTLP`, `tracing`, `monitoring`, `Datadog`, `Dynatrace`, `Grafana`, `Splunk`, `Cloud Trace`, `tagging`, `FinOps`.

As the user pastes raw, messy intranet text in each round, immediately strip out corporate fluff and categorize the enforceable rules before moving to the next round.

#### Track C: Mode 3 (Expert Architect Interview)
Skip raw document ingestion and proceed directly to **Phase 4 (The High-Value Human Grill)**, walking through the 5 engineering domains in batches of 2 to 3 questions per turn.

---

### Phase 3: The 3-Bucket Triage & Classification Engine

Before asking follow-up questions, classify every extracted standard into one of three buckets and show the user a concise **Triage Summary Table**:

| Bucket | Destination | Classification Rule | Examples |
| :--- | :--- | :--- | :--- |
| **Bucket 1: `PINNED_CONTRACT`** | `./org-standards.md` (`<= 120 lines`) | Deterministic rules that every stage of an A/SDLC build (Stages 1 to 8) must follow on every turn. | Approved backend/frontend languages, API spec format, IAM/auth pattern, parameterized query requirement, max LoC per slice, minimum test coverage %, OpenTelemetry tracing rules. |
| **Bucket 2: `DOMAIN_RUNBOOK`** | `./.okf/runbooks/<domain>.md` | Detailed engineering standards needed only during specific tasks so they do not bloat every prompt. | Full database table naming rules, approved Terraform module registries, detailed UI color/typography tokens, regulatory control mappings (SOC2, HIPAA, API RP 53, NERC CIP). |
| **Bucket 3: `PROCESS_NOISE`** | `./.okf/runbooks/DISCARDED_PROCESS_LOG.md` | Human committee procedures and administrative policies that an AI coding agent cannot enforce in code. | CAB meeting schedules, ServiceNow ticket templates, vendor procurement workflows, quarterly HR compliance training, legacy mainframe rules unrelated to modern repos. |

---

### Phase 4: The High-Value Human Grill (2 to 3 Questions per Turn, Completion-Driven)

Never ask the human to repeat what was already in their documents. Instead, act as a sharp Principal Architect and use `ask_question` in batches of **2 to 3 focused questions per turn** across as many turns as needed until all 4 exit criteria are 100% resolved:

1. **Contradiction Resolution:**
   * Identify every conflict across their internal standards pages (for example, an older standard requiring static API keys vs. a newer standard requiring OIDC Workload Identity, or two competing frontend frameworks). Force the user to pick the single authoritative rule for this `org-standards.md`.
2. **Converting Soft Prose into Hard Deterministic Thresholds:**
   * Enterprise wikis often use vague instructions like *"write comprehensive unit tests"*, *"keep pull requests small"*, or *"ensure low latency"*.
   * Grill the user to lock down exact, checkable numbers for Stage 4 (`AGENTS.md`), Stage 6 (`@security-governance-critic`), and Stage 7 (`@eval-telemetry-auditor`), providing sensible defaults if their wiki does not specify a number:
     * **Max Lines of Code (LoC) per vertical coding slice** (for example, `<= 300 LoC`)
     * **Max lines in `AGENTS.md`** (for example, `<= 150 lines`)
     * **Minimum automated test-to-code ratio or line coverage %** (for example, `>= 35%` test-to-code ratio or `>= 80%` unit coverage)
     * **Mandatory security, scanner & PII redaction gates** (for example, 100% parameterized SQL queries, zero hardcoded secrets, PII scrubbing on logs and telemetry spans, plus the exact Stage 6 security scanners and Stage 7/8 monitoring/APM backends mandated by corporate policy so Stage 1 can pre-populate `.sdlc/toolchain_config.json`)
3. **Unwritten Tribal Knowledge Check:**
   * Explicitly ask: *"What is the #1 unwritten rule at your company that causes a Principal Engineer or Security Reviewer to reject a Pull Request, even though it isn't clear on the internal website?"*
4. **Application Profile Filtering (If Building for a Specific App):**
   * Ask about the target application's workload profile (internal web tool, external customer portal, data pipeline, or edge/OT service; cloud host; data sensitivity tier; whether the app calls LLMs or is a deterministic non-AI service) so only the rules relevant to that application make it into the final `<= 120-line` `org-standards.md`.

---

### Phase 5: Generate the Two-Tier A/SDLC v3.1 Output Package

Once all Phase 4 questions are answered, write the following files to the user's chosen workspace directory using `write_file`:

1. **`./org-standards.md` (Strictly `<= 120 lines`):**
   * Use the structure in [`resources/ORG_STANDARDS_TEMPLATE.md`](./resources/ORG_STANDARDS_TEMPLATE.md).
   * Ensure it uses **1-indexed A/SDLC v3.1 stages (`Stages 1 to 8`)** in its grounding header and maps cleanly to:
     * **Section 1: Mandatory Reference Architecture & Tech Stack** (Customer's actual languages, frameworks, runtime versions, service topology, and API contract format)
     * **Section 2: Security, Identity, Data Privacy, Mandated Scanners & AI Safety Guardrails** (Customer's actual auth/IAM provider, secret manager, query safety rules, mandated Stage 6 security scanners and SARIF expectations, input validation/screening, and human-in-the-loop approval boundaries)
     * **Section 3: Code Quality, Slicing & Verification Standards** (Deterministic slice size ceiling, `AGENTS.md` line cap, test coverage floor, test runners, and linter/static analysis gates)
     * **Section 4: Observability, OpenTelemetry, Approved Monitoring Tools & FinOps Guardrails** (Structured logging format, OpenTelemetry tracing/span requirements, approved Stage 7/8 monitoring/APM query backends, PII redaction rules, model routing tiers if using LLMs, and cloud cost controls)
     * **Section 5: Regulatory Frameworks & Linked `.okf/runbooks/` Index** (Direct relative links to the deep domain runbooks generated in `.okf/runbooks/`)
2. **`./.okf/runbooks/INDEX.md` + Domain Runbooks:**
   * Use [`resources/RUNBOOK_INDEX_TEMPLATE.md`](./resources/RUNBOOK_INDEX_TEMPLATE.md) to create `.okf/runbooks/INDEX.md`.
   * Write the detailed domain reference files in `.okf/runbooks/`:
     * `.okf/runbooks/architecture-and-apis.md`
     * `.okf/runbooks/security-and-iam.md`
     * `.okf/runbooks/data-and-storage.md`
     * `.okf/runbooks/testing-and-ci.md`
     * `.okf/runbooks/observability-and-finops.md`
     * `.okf/runbooks/DISCARDED_PROCESS_LOG.md` (Audit trail of non-code bureaucratic pages excluded from the coding harness, with a one-line reason per item so governance teams have full traceability).

### Phase 6: Final Verification & Handoff Summary

After writing the files:
1. Verify that `./org-standards.md` is **`<= 120 lines`**, contains **zero unconfirmed vendor assumptions**, and has **zero vague rules** where a deterministic metric is required.
2. Present a summary showing:
   * Total internal standards analyzed vs. distilled into `org-standards.md` (`Bucket 1`), archived in `.okf/runbooks/` (`Bucket 2`), and filtered out to `DISCARDED_PROCESS_LOG.md` (`Bucket 3`).
   * Clickable links to `./org-standards.md` and `./.okf/runbooks/INDEX.md`.
   * The exact path to pass into Stage 1 of `/agentic-sdlc --new` when they are ready to start their project build.

<!-- asdlc_version: "3.1.0" | distribution_tier: "customer-safe" -->
# Organizational Development Standards & Policies (`org-standards.md`)

> **A/SDLC v3.1 Grounding Contract (`Stages 1 to 8`):** Ingested by `@project-conductor` in **Stage 1 (Project Onboarding, RACI, GitHub Setup, Telemetry Sink, Toolchain Discovery & Asset Intake)**, cited by `@product-owner` in **Stage 2 (`PRD.md`)**, enforced by `@spec-architect` in **Stage 3 (`SPEC.md`)** and `@parallel-builder-orchestrator` in **Stage 4 (`AGENTS.md`)** and **Stage 5 (Parallel Builder Execution)**, audited by `@security-governance-critic` in **Stage 6 (`SECURITY_AUDIT.md`)**, verified by `@eval-telemetry-auditor` in **Stage 7 (`EVAL_REPORT.md`)**, and evolved by `@kaizen-evolution-agent` in **Stage 8 (`KAIZEN_REPORT.md`)**.
> **Open Knowledge Format (`.okf/`):** Pinned at the top of `.okf/manifest.yaml` (`pinned_contracts`) for a **90% Vertex AI Context Cache discount** across Stages 1 to 8. Keep this file **`<= 120 lines`** and store deep reference manuals in `.okf/runbooks/`.

---

## 1. Stack-Adaptive Reference Architecture (Bound to `.sdlc/tech_stack.json`; Reference Cartridge Profile Shown Below)
> **Note:** A/SDLC v3.0 never forces a hardcoded vendor stack. Every project binds to the customer's actual stack declared in `.sdlc/tech_stack.json` (or distilled via `/org-standards-builder`). The bullets below show the reference cartridge profile.
- **Backend Framework:** Python 3.12+ with **FastAPI**, **Pydantic v2** strict schema validation (`extra="forbid"`), and **Google Cloud Agent Development Kit (ADK 2.0)** (or the project's declared stack in `.sdlc/tech_stack.json`).
- **Frontend Framework & UI Design System:** **Vue.js 3** (Composition API `<script setup>`) with **Tailwind CSS** utility styling governed by the **Clean Enterprise Light First Design Language** (or the project's ingested `.okf/intake/styles/` brand style guide and `.sdlc/tech_stack.json` UI stack). Default tokens enforce `#F8FAFC` alabaster canvas, `#FFFFFF` pure cards, `#E2E8F0` `1px` borders, `#0B57D0` Google Cloud Cobalt primary actions, `Plus Jakarta Sans` headings, `Inter` UI body, and `JetBrains Mono` (`tabular-nums`) for all KPIs and telemetry.
- **Service Topology:** Strict **Dual-Service Split**: Control Plane runs on `http://localhost:8000` (Flight Deck); Target Application runs independently on `http://localhost:8001` or `http://localhost:8002`.
- **API Contract Standard:** Contract-First **OpenAPI 3.1** (or stack-native gRPC Protobuf / GraphQL schema per `.sdlc/tech_stack.json`) locked in **Stage 3 (`SPEC.md`)** before any **Stage 5** code generation.

---

## 2. Security, Identity & AI Safety Guardrails
- **Pre-LLM Input Defense:** All untrusted user prompts, telemetry notes, and external payloads MUST pass **Google Cloud Model Armor** screening (`Prompt Injection`, `Jailbreak`, `SQL/Command Injection`, and `Sensitive Data DLP`) prior to model invocation.
- **Database & Query Safety:** 100% parameterized SQL queries (`?` / `$1` placeholders); raw f-string or concatenated SQL queries are strictly prohibited (**Stage 6** `CM-2026-999` gate).
- **Workload & Agent Identity:** Enforce **SPIFFE Workload Identity** (`spiffe://<enterprise-trust-domain>/ns/asdlc/sa/agentic-sdlc-coordinator`) and **Workforce Identity Federation (WIF)** over static service account keys.
- **Human-in-the-Loop (`A2UI`) Actuation Gate:** High-impact write operations, physical OT actuation, or financial transactions require explicit human sign-off via an **ADK 2.0 `A2UI` confirmation card**.

---

## 3. Code Quality, Slicing & Verification Standards
- **Incremental Vertical Slicing:** Every **Stage 5** coding task MUST be scoped to **`<= 300 Lines of Code (LoC)`** per slice to prevent context rot.
- **Context-Rot Ceiling:** Project harness rules (**Stage 4** `AGENTS.md`) MUST remain **`<= 150 lines`**, offloading deep domain reference manuals into `.okf/runbooks/`.
- **Test-Driven Development (TDD) Floor:** Minimum **`>= 35.0%` test-to-code ratio** (`58%+` target) verified via automated `pytest`, `vitest`, `go test`, or stack-native test suites before **Stage 7 (`EVAL_REPORT.md`)** release sign-off.
- **Tool Budgeting:** Each specialized subagent is capped at **`<= 8` domain-specific tools** with explicit `Read`, `Write`, and `Compute` separation.

---

## 4. FinOps, Model Routing & Observability Standards
- **3-Tier Semantic Model Router (`< 5ms` routing overhead):**
  - **Tier 1 (`gemini-2.5-flash-lite`):** Nominal heartbeats, simple classification, and syntax checks.
  - **Tier 2 (`gemini-2.5-flash`):** Stage 1 onboarding and asset intake, Stage 2 discovery interviews (`PRD.md`), standard RAG synthesis, and Stage 5 parallel builder coding slices.
  - **Tier 3 (`gemini-2.5-pro`):** Stage 3 architecture specification (`SPEC.md`), Stage 4 guardrail and builder synthesis (`AGENTS.md`), Stage 6 adversarial security review (`SECURITY_AUDIT.md`), Stage 7 evaluation auditing (`EVAL_REPORT.md`), Stage 8 Kaizen evolution (`KAIZEN_REPORT.md`), and complex multi-signal anomaly triage.
- **Prefix Context Caching:** Pin `org-standards.md`, `RACI.md`, `PRD.md`, `SPEC.md`, and `AGENTS.md` at the front of every prompt to achieve a **90% input token discount**.
- **Customer Security & Monitoring Toolchain (`.sdlc/toolchain_config.json`):** Configured in Stage 1 via auto-probe and confirmation across 9 Stage 6 security presets (`wiz`, `github_codeql`, `semgrep`, `snyk`, `sonarqube`, `trivy`, `gitleaks`, `codemender`, `model_armor`), 8 Stage 7/8 monitoring presets (`local_jsonl`, `gcp_cloud_observability`, `datadog`, `dynatrace`, `grafana_lgtm`, `splunk`, `azure_monitor`, `aws_cloudwatch`), or unlimited custom Bring Your Own Tool entries (with OASIS SARIF 2.1.0 ingestion and `WARN_AND_DEGRADE_LLM_ONLY` Tool Execution Ledgers).
- **Unified 3-Pattern OpenTelemetry Tracing (`.sdlc/telemetry_config.json`):** Emit standard `gen_ai.*` attributes (`gen_ai.agent.id`, `gen_ai.conversation.id`, `gen_ai.operation.name`, `gen_ai.request.model`, `gen_ai.usage.input_tokens`, `gen_ai.usage.output_tokens`) when `app_uses_llm: true`, or standard HTTP/RPC/DB OpenTelemetry spans when `app_uses_llm: false`, with PII/secret redaction callbacks (`OTEL-PII-REDACT`) across Pattern A (`LOCAL_FILE_SINK`), Pattern B (`SHARED_REMOTE_SINK`), or Pattern C (`CLOUD_OUTER_LOOP`).

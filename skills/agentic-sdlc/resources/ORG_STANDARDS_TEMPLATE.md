<!-- asdlc_version: "3.0.0" | distribution_tier: "customer-safe" -->
# Organizational Development Standards & Policies (`org-standards.md`)

> **Stage 0 Grounding Artifact:** Ingested by `@product-owner` during **Stage 0 (Product Discovery & Requirements)** to align `PRD.md`, `SPEC.md` (Stage 1), and `AGENTS.md` (Stage 2) with internal engineering, security, compliance, and FinOps standards.
> **Open Knowledge Format (`.okf/`):** Pinned at the top of `.okf/manifest.yaml` (`pinned_contracts`) for a **90% Vertex AI Context Cache discount** across Stages 1–6.

---

## 1. Mandatory Full-Stack Reference Architecture
- **Backend Framework:** Python 3.12+ with **FastAPI**, **Pydantic v2** strict schema validation (`extra="forbid"`), and **Google Cloud Agent Development Kit (ADK 2.0)**.
- **Frontend Framework:** **Vue.js 3** (Composition API `<script setup>`) with **Tailwind CSS** utility styling and responsive desktop/tablet layouts.
- **Service Topology:** Strict **Dual-Service Split** — Control Plane runs on `http://localhost:8000` (Flight Deck); Target Application runs independently on `http://localhost:8001` or `http://localhost:8002`.
- **API Contract Standard:** Contract-First **OpenAPI 3.1** locked in `SPEC.md` before any Stage 3 code generation.

---

## 2. Security, Identity & AI Safety Guardrails
- **Pre-LLM Input Defense:** All untrusted user prompts, telemetry notes, and external payloads MUST pass **Google Cloud Model Armor** screening (`Prompt Injection`, `Jailbreak`, `SQL/Command Injection`, and `Sensitive Data DLP`) prior to model invocation.
- **Database & Query Safety:** 100% parameterized SQL queries (`?` / `$1` placeholders); raw f-string or concatenated SQL queries are strictly prohibited (`CM-2026-999` gate).
- **Workload & Agent Identity:** Enforce **SPIFFE Workload Identity** (`spiffe://...`) and **Workforce Identity Federation (WIF)** with end-user OAuth token propagation over shared static service account keys.
- **Human-in-the-Loop (`A2UI`) Actuation Gate:** High-impact write operations, physical actuation, or financial transactions require explicit human sign-off via an **ADK 2.0 `A2UI` confirmation card**.

---

## 3. Code Quality, Slicing & Verification Standards
- **Incremental Vertical Slicing:** Every Stage 3 coding task MUST be scoped to **`<= 300 Lines of Code (LoC)`** per slice to prevent context rot.
- **Context-Rot Ceiling:** Project harness rules (`AGENTS.md`) MUST remain **`<= 150 lines`**, offloading deep domain reference manuals into `.okf/runbooks/`.
- **Test-Driven Development (TDD) Floor:** Minimum **`>= 35.0%` test-to-code ratio** (`58%+` target) verified via automated `pytest` and `vitest` suites before Stage 5 release sign-off.
- **Tool Budgeting:** Each specialized subagent is capped at **`<= 8` domain-specific tools** with explicit `Read`, `Write`, and `Compute` separation.

---

## 4. FinOps, Model Routing & Observability Standards
- **3-Tier Semantic Model Router (`< 5ms` routing overhead):**
  - **Tier 1 (`gemini-2.5-flash-lite`):** Nominal heartbeats, simple classification, and syntax checks.
  - **Tier 2 (`gemini-2.5-flash`):** Stage 0 discovery interviews, standard RAG synthesis, and Stage 3 vertical slice coding.
  - **Tier 3 (`gemini-2.5-pro`):** Stage 1 architecture specification (`SPEC.md`), Stage 4 adversarial security review, and complex multi-signal anomaly triage.
- **Prefix Context Caching:** Pin `org-standards.md`, `PRD.md`, `SPEC.md`, and `AGENTS.md` at the front of every prompt to achieve a **90% input token discount**.
- **OpenTelemetry GenAI Tracing:** Emit standard `gen_ai.*` attributes (`gen_ai.agent.id`, `gen_ai.operation.name`, `gen_ai.request.model`, `gen_ai.usage.input_tokens`, `gen_ai.usage.output_tokens`) on every turn.

---

## 5. Domain Regulatory & Background Reference Documents
- **Primary Industry / Regulatory Frameworks:** `<Specify domain standards, e.g., API RP 53, PHMSA 49 CFR 195, NACE SP0169, SEC Reg BI / COPPA, SOC2 / ISO 27001>`
- **Authoritative Background Documents & Runbooks:**
  - `.okf/manifest.yaml` — Open Knowledge Format bundle manifest
  - `.okf/runbooks/README.md` — Version-pinned domain runbooks and legacy schema mappings

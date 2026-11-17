<!-- asdlc_version: "3.1.0" | distribution_tier: "customer-safe" -->
# Organizational Development Standards & Policies (`org-standards.md`)

> **A/SDLC v3.1 Grounding Contract (`Stages 1 to 8`):** Ingested in **Stage 1 (`@project-conductor`)**, cited in **Stage 2 (`PRD.md` via `@product-owner`)**, enforced in **Stage 3 (`SPEC.md` via `@spec-architect`)** and **Stage 4 (`AGENTS.md` via `@parallel-builder-orchestrator`)**, audited in **Stage 6 (`@security-governance-critic`)**, and verified in **Stage 7 (`@eval-telemetry-auditor`)**.
> **Open Knowledge Format (`.okf/`):** Pinned at the top of `.okf/manifest.yaml` (`pinned_contracts`) for prefix context caching across Stages 1 to 8. Keep this file **`<= 120 lines`** and store deep reference manuals in `.okf/runbooks/`.

---

## 1. Mandatory Reference Architecture & Technology Stack
- **Organization & Application Profile:** `<Organization Name>` • `<Application / Workload Type, e.g., Internal Web App / Customer Portal / Data Service / Edge OT>`
- **Backend Language & Framework:** `<e.g., Python 3.12+ with FastAPI & Pydantic v2 / Go 1.22+ / Java 21 Spring Boot / C# .NET 8>`
- **Frontend Framework & UI System:** `<e.g., Vue.js 3 + Tailwind CSS / React 18 + TypeScript / Angular / Backend-Only API>`
- **Database & Persistence Layer:** `<e.g., Cloud SQL PostgreSQL / AlloyDB / Cloud Firestore / BigQuery / Snowflake>`
- **Service Topology & Target Runtime:** `<e.g., Cloud Run containers / GKE / On-Prem Kubernetes, plus local dev ports>`
- **API Contract Standard:** `<e.g., Contract-First OpenAPI 3.1 / gRPC Protobuf v3 / GraphQL schema locked in SPEC.md before Stage 5 coding>`

---

## 2. Security, Identity (IAM), Data Privacy & AI Safety Guardrails
- **Authentication & Workload Identity:** `<e.g., OIDC / OAuth 2.0 via Workforce Identity Federation / Okta / Entra ID / SPIFFE; static service account keys prohibited>`
- **Secret & Credential Management:** `<e.g., Google Cloud Secret Manager / HashiCorp Vault; zero credentials or API keys in source code or .env commits>`
- **Database & Query Safety:** `<e.g., 100% parameterized queries or ORM prepared statements; raw string-concatenated SQL is a critical Stage 6 blocker>`
- **Pre-LLM Input & Prompt Defense:** `<e.g., Strict schema validation, prompt-injection screening, and DLP/PII scrubbing on all untrusted inputs before model or tool calls>`
- **Approved Stage 6 Security Scanners (`.sdlc/toolchain_config.json`):** `<e.g., Wiz CLI, GitHub CodeQL, Semgrep, Snyk, SonarQube, Trivy, Gitleaks, CodeMender, or Custom SARIF tool>`
- **Human-in-the-Loop Approval Gate:** `<e.g., High-impact write actions, production mutations, financial transactions, or OT actuation require explicit human confirmation>`

---

## 3. Code Quality, Slicing & Verification Standards
- **Incremental Vertical Slicing Ceiling:** Every Stage 5 coding slice MUST remain **`<= <300> Lines of Code (LoC)`** per task to prevent context rot.
- **Harness Rule Ceiling (`AGENTS.md`):** Project `AGENTS.md` MUST remain **`<= <150> lines`**, offloading detailed domain tables into `.okf/runbooks/`.
- **Automated Testing Floor (Stage 7 Gate):** Minimum **`>= <35.0%>` test-to-code ratio** (or **`>= <80%>` unit test coverage**) verified via `<pytest / vitest / go test / jest / junit>` before Stage 7 sign-off.
- **Static Analysis & Linting:** `<e.g., ruff / mypy / eslint / golangci-lint / sonar must pass with zero high-severity findings>`
- **Unwritten PR Rejection Rules (Tribal Guardrails):**
  - `<Rule 1 that senior engineers or security reviewers always enforce in PR reviews>`
  - `<Rule 2 that senior engineers or security reviewers always enforce in PR reviews>`

---

## 4. Observability, OpenTelemetry & FinOps Guardrails
- **OpenTelemetry & Distributed Tracing:** Emit structured `<OpenTelemetry gen_ai.* or standard HTTP/RPC/DB spans>` configured via `.sdlc/telemetry_config.json` (`<LOCAL_FILE_SINK / SHARED_REMOTE_SINK / CLOUD_OUTER_LOOP>`).
- **Approved Stage 7 & 8 Monitoring / APM Backends (`.sdlc/toolchain_config.json`):** `<e.g., Local JSONL, Google Cloud Trace & BigQuery, Datadog, Dynatrace, Grafana LGTM, Splunk, Azure Monitor, AWS CloudWatch, or Custom>`
- **PII & Secret Redaction in Telemetry:** Scrub all `<PII, bearer tokens, API keys, and customer credentials>` before logs or spans leave the application process.
- **Model Routing & Token FinOps (If Using GenAI/LLMs):**
  - **Fast / Low-Cost Tier:** `<Model name and approved use cases>`
  - **Standard Production Tier:** `<Model name and approved use cases>`
  - **Deep Reasoning / Review Tier:** `<Model name and approved use cases>`
- **Cloud Resource Tagging & Cost Controls:** `<Mandatory cost-center/project labels and budget circuit breakers>`

---

## 5. Regulatory Frameworks & Linked Domain Runbooks (`.okf/runbooks/`)
- **Applicable Regulatory / Industry Standards:** `<e.g., SOC 2 Type II, ISO 27001, HIPAA, PCI-DSS, NERC CIP, PHMSA 49 CFR 195, API RP 53>`
- **Detailed Domain Runbooks (Optional Paths Generated by `/org-standards-builder`, Loaded on Demand):**
  - `.okf/runbooks/INDEX.md`: Master catalog of deep organizational standards
  - `.okf/runbooks/architecture-and-apis.md`: Detailed framework patterns, API error schemas, and naming rules
  - `.okf/runbooks/security-and-iam.md`: Detailed IAM roles, encryption ciphers, and threat controls
  - `.okf/runbooks/data-and-storage.md`: Database migration rules, retention schedules, and PII classification tables
  - `.okf/runbooks/testing-and-ci.md`: CI/CD pipeline stages, test fixture rules, and release checklists
  - `.okf/runbooks/observability-and-finops.md`: Log schemas, SLO definitions, and FinOps tagging matrices

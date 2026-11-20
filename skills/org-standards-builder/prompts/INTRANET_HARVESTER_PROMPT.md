<!-- asdlc_version: "3.1.1" | distribution_tier: "customer-safe" -->
# Intranet Standards Harvester Prompt (`INTRANET_HARVESTER_PROMPT.md`)

## When to Use This Prompt
Use this copy-paste prompt when your organization has **dozens or hundreds of engineering, security, architecture, and compliance standards** stored on an internal website (such as SharePoint, Confluence, Backstage, ServiceNow, an internal developer portal, or a folder of PDFs/Google Docs).

Run this prompt inside **whichever enterprise AI tool already has read access to your internal website or document repository**:
* **Google Gemini Enterprise / Vertex AI Search** (connected to SharePoint, Confluence, Google Drive, or internal intranet portals)
* **Google NotebookLM** (after uploading exported PDFs, Markdown files, or intranet URLs as sources)
* **Microsoft 365 Copilot / Glean / Internal Enterprise RAG Search**

Once your enterprise search tool outputs the structured `RAW_STANDARDS_EXTRACT.md` below, feed that output directly into the **`/org-standards-builder`** skill (or the companion [`STANDALONE_ARCHITECT_PROMPT.md`](./STANDALONE_ARCHITECT_PROMPT.md)) to resolve conflicts, lock numeric thresholds, and generate your final `org-standards.md` (`<= 120 lines`) and `.okf/runbooks/` catalog.

---

## Copy-Paste Prompt (For Gemini Enterprise, NotebookLM, or Internal Enterprise Search)

```text
You are a Principal Enterprise Systems Architect and Standards Distiller.

I need you to scan our internal engineering, architecture, security, testing, data governance, and cloud standards catalog (across our connected intranet, wiki pages, or uploaded source documents) and extract ONLY the technical rules that software engineers and AI coding agents must enforce when designing, writing, testing, and reviewing software.

CRITICAL FILTERING RULES:
1. STRIP OUT BUREAUCRATIC PROCESS NOISE: Ignore non-code human procedures such as Change Advisory Board (CAB) meeting schedules, ServiceNow/Jira ticket workflows, HR training policies, vendor procurement steps, and legacy mainframe standards unrelated to application code. List discarded topics briefly at the very end under a single "Discarded Process Noise" bullet list.
2. PRESERVE EXACT TECHNICAL RULES & NUMBERS: Whenever a document specifies exact languages, framework versions, authentication protocols, database rules, encryption standards, API formats, test coverage percentages, or logging requirements, extract the exact rule and cite the source page title or URL/ID.
3. FLAG CONTRADICTIONS: If two internal pages disagree (for example, an older page mandating one authentication method or framework and a newer page mandating another), explicitly flag both under a "Detected Contradictions & Ambiguities" section so a human architect can pick the winner.
4. DO NOT INVENT STANDARDS: Only extract rules that actually exist in our sources. If a category below is not covered in our internal documents, write "NOT SPECIFIED IN SOURCES (Requires Architect Input)".

Please output your response in clean Markdown using this exact structure (`RAW_STANDARDS_EXTRACT.md`):

# Raw Enterprise Standards Extract (`RAW_STANDARDS_EXTRACT.md`)

## 1. Languages, Frameworks, Runtime Versions & Reference Architecture
- **Backend Languages & Frameworks:** [List approved languages, versions, and frameworks + source citation]
- **Frontend / UI Frameworks & Design Systems:** [List approved UI frameworks, component libraries, accessibility rules + source citation]
- **Service Topology & Hosting Targets:** [Containers, Kubernetes, Serverless, VM, Edge/On-Prem rules + source citation]
- **API Contract Standards:** [OpenAPI, gRPC, GraphQL, versioning, pagination, error payload format + source citation]

## 2. Security, Identity (IAM), Secrets & AI/Input Safety
- **User & Service Authentication:** [OAuth2, OIDC, SAML, mTLS, Workload Identity, service account key rules + source citation]
- **Secret & Key Management:** [Approved secret managers, rotation rules, prohibition on hardcoded credentials + source citation]
- **Database & Input Safety:** [Parameterized SQL rules, input validation, XSS/CSRF/injection defenses + source citation]
- **Mandated Security Scanners & AppSec Tools (Stage 6):** [Wiz, GitHub CodeQL, Semgrep, Snyk, SonarQube, Trivy, Gitleaks, CodeMender, Veracode, Checkmarx, Prisma Cloud, or internal scanners + CLI/MCP/SARIF rules + source citation]
- **AI & LLM Guardrails (if applicable):** [Approved models/endpoints, prompt injection screening, DLP/PII redaction, human-in-the-loop approval gates + source citation]

## 3. Data Governance, Storage & External Integrations
- **Approved Databases & Storage Engines:** [Relational, NoSQL, object storage, caching, schema migration tools + source citation]
- **Data Classification, PII & Encryption:** [Encryption at rest/in transit, PII handling, residency rules, retention policies + source citation]
- **External & Partner API Rules:** [Egress controls, proxy/gateway requirements, retry/timeout/circuit-breaker standards + source citation]

## 4. Code Quality, Slicing, Testing & CI/CD Gates
- **Automated Testing Requirements:** [Required unit/integration/E2E frameworks, minimum test coverage %, TDD rules + source citation]
- **Code Size, Complexity & Linting:** [PR/slice size limits, cyclomatic complexity, mandatory linters/formatters, SAST/DAST scanners + source citation]
- **Repository & Branching Standards:** [Branch protection, commit/tag conventions, code review sign-off rules + source citation]

## 5. Observability, Logging, OpenTelemetry & FinOps
- **Logging & Tracing Standards:** [Structured JSON logging, OpenTelemetry / distributed tracing attributes, correlation IDs + source citation]
- **Metrics, Alerting, APM & Monitoring Backends (Stage 7/8):** [Health check endpoints, latency/error SLOs, approved OTLP ingest endpoints and monitoring/APM query backends such as Google Cloud Observability, Datadog, Dynatrace, Grafana LGTM, Splunk, Azure Monitor, AWS CloudWatch, or internal tools + source citation]
- **Cloud Cost & FinOps Tagging:** [Mandatory resource tags/labels, budget alerts, model/compute tiering rules + source citation]

## 6. Deep Domain & Regulatory Reference Material (For `.okf/runbooks/`)
- [List detailed domain tables, naming conventions, Terraform module lists, or industry regulations like SOC2, ISO 27001, HIPAA, PCI-DSS, NERC CIP, PHMSA, or API RP 53 that are too long for a 120-line summary but should be preserved in domain runbooks]

## 7. Detected Contradictions & Ambiguities (Requires Human Decision)
- **Conflict / Gap 1:** [Page A says X (date/link) vs. Page B says Y (date/link)]
- **Soft Rules Needing Hard Numbers:** [List vague rules like "write good tests" or "keep PRs small" that lack a numeric threshold]

## 8. Discarded Process Noise (Excluded from AI Coding Harness)
- [One-line bullet per excluded administrative/process page and why it is not code-enforceable]
```

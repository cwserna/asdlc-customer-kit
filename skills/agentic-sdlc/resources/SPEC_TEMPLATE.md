<!-- asdlc_version: "3.1.1" | distribution_tier: "customer-safe" -->
# Executable Specification (`SPEC.md`: Single Source of Design Truth)

> **Methodology:** Spec-Driven Development (`Stage 3: Technical Design & API Blueprint`, `A/SDLC v3.1`)
> **Status:** `ACTIVE_CONTRACT`
> **Toolchain, OpenTelemetry & Outer-Loop Configuration:** `./.sdlc/toolchain_config.json` • `./.sdlc/telemetry_config.json` • `./.sdlc/cloud_outer_loop.json`

## 1. Problem-First Scoping & KPIs (Google Cloud WAF)
- **Business Objective:** `<What operational problem or decision is being accelerated?>`
- **Target Persona:** `<e.g., Drilling Engineer / Operations Manager / CE Demo Audience>`
- **Impact × Feasibility Quadrant:** `Do First (High Impact, High Feasibility)`

| KPI Category | Metric | Baseline | Target |
| :--- | :--- | :--- | :--- |
| **Business Value** | Task handling / decision latency | `<e.g., 45 mins>` | `<e.g., < 30 secs>` |
| **Cost Efficiency** | Avg cost per workflow turn (Semantic Router + 90% Cache) | `<Baseline Pro>` | `<3x reduction>` |
| **Quality / Precision** | Golden dataset evaluation pass rate | `N/A` | `>= 95%` |

---

## 2. External & Internal Data Source Connectivity, Auth & Sandbox Strategy
| Data Source | Protocol & Schema (`.okf/intake/schemas/`) | Authentication & Secret Management | Network & Residency Boundary | Stage 5 & Stage 7 Testing Strategy (Sandbox vs. Deterministic Contract Mock) |
| :--- | :--- | :--- | :--- | :--- |
| `<e.g., Partner Inventory API>` | `<REST OpenAPI 3.1 / GraphQL / gRPC / MCP Server>` | `<OAuth2 Client Credentials in Secret Manager / WIF / SPIFFE>` | `<Public HTTPS / Private Service Connect / VPC-SC>` | `<Deterministic local contract mock for Stage 5/7 tests; never hits live prod>` |

---

## 3. Shared Parent Contract (Stack-Adaptive API, Data & UI Schemas)
All synthesized builders in `.sdlc/builder_manifest.json` MUST adhere strictly to these endpoints and schemas:

### Endpoint 1: `POST /api/v1/sdlc/evaluate`
- **Request Schema (`TelemetryRequest`):**
```json
{
  "asset_id": "RIG-PERM-042",
  "query": "Analyze mud pump pressure spike and recommend remediation",
  "priority": "HIGH"
}
```
- **Response Schema (`TelemetryEvaluationResponse`):**
```json
{
  "trace_id": "otel-span-8f92a1",
  "routed_model": "gemini-2.5-pro",
  "cached_tokens_ratio": 0.90,
  "model_armor_verdict": "SAFE",
  "summary": "Pressure spike detected on Triplex Pump #2; initiate choke valve check.",
  "recommended_actions": ["Inspect relief valve", "Throttle SPM by 15%"]
}
```

### Endpoint 2: `POST /api/v1/kaizen/override` (Stage 8 Kaizen Feedback & Edge Store-and-Forward Contract)
- **Request Schema (`KaizenOverrideRequest`):**
```json
{
  "trace_id": "otel-span-8f92a1",
  "session_id": "sess-perm-001",
  "operator_id": "operator@example.com",
  "override_type": "HUMAN_CORRECTION",
  "operator_notes": "Choke manifold relief valve was already isolated; root cause was suction dampener pre-charge loss.",
  "expected_outcome": "Check suction dampener bladder nitrogen pre-charge before throttling SPM."
}
```
- **Response Schema (`KaizenOverrideReceipt`):**
```json
{
  "override_id": "ovr-9012",
  "model_armor_verdict": "SAFE",
  "pii_redacted": true,
  "buffered_in_edge_sqlite": true,
  "sink_pattern": "LOCAL_FILE_SINK",
  "status": "QUEUED_FOR_STAGE8_KAIZEN"
}
```

---

## 4. Split OpenTelemetry Ingest/Query, Security Toolchain & Cloud Outer-Loop Contract (`A/SDLC v3.1`)
1. **Split Write (`ingest`) vs. Read (`query`) Telemetry Contract (`.sdlc/telemetry_config.json`):**
   - **LLM Scope (`app_uses_llm`):** `<true (emit gen_ai.* attributes) | false (emit standard OpenTelemetry HTTP, RPC, DB, and error spans without LLM fields)>`
   - **Write / Ingest Path (`ingest`, for Stage 5 Builders):** `<LOCAL_JSONL (.sdlc/otel_traces.jsonl) | OTLP/gRPC or OTLP/HTTP endpoint + service_name + auth env var names>`
   - **Read / Query Path (`query`, for Stage 7 & Stage 8 Auditors):** `<FILE (.sdlc/otel_traces.jsonl) | MCP (<server>/<tool>) | CLI (gcloud/bq/az/aws) | HTTP_API (Datadog/Dynatrace/Grafana/Splunk/Custom) | MANUAL_EXPORT>`
   - **Unified 3-Pattern Sink Topology:**
     - **Pattern A (`LOCAL_FILE_SINK`):** Exports spans to `.sdlc/otel_traces.jsonl` and overrides to `.sdlc/kaizen_overrides.jsonl`.
     - **Pattern B (`SHARED_REMOTE_SINK`):** Dual-exports spans and overrides to Google Cloud Trace / BigQuery or the customer's APM/OTLP collector while local Stage 7 and Stage 8 agents query the shared sink on demand.
     - **Pattern C (`CLOUD_OUTER_LOOP`):** Exports spans and overrides to Cloud Trace, BigQuery, and Cloud Pub/Sub + Eventarc to wake up Always-On Stage 7 (Cloud Run + ephemeral Cloud Build gVisor sandbox) and Stage 8 (Vertex AI Agent Engine).
2. **Customer Security & Monitoring Toolchain Contract (`.sdlc/toolchain_config.json`, Policy: `WARN_AND_DEGRADE_LLM_ONLY`):**
   | Stage | Tool / Preset (`preset_id` or `custom`) | Access Method (`MCP` / `CLI` / `CI_CHECK` / `HTTP_API` / `FILE` / `MANUAL_EXPORT` / `LLM_ONLY`) | Command, MCP Tool, Endpoint, or SARIF Path (`.sdlc/reports/`) | Required Auth Env Vars (Names Only) |
   | :--- | :--- | :--- | :--- | :--- |
   | **Stage 6** | `<e.g., wiz / semgrep / snyk / github_codeql / codemender / custom>` | `<CLI / MCP / CI_CHECK / MANUAL_EXPORT>` | `<e.g., semgrep scan --sarif --output .sdlc/reports/semgrep.sarif .>` | `<e.g., WIZ_CLIENT_ID, WIZ_CLIENT_SECRET>` |
   | **Stage 7 & 8** | `<e.g., local_jsonl / gcp_cloud_observability / datadog / dynatrace / grafana_lgtm / custom>` | `<FILE / MCP / CLI / HTTP_API>` | `<e.g., .sdlc/otel_traces.jsonl or MCP/API query>` | `<e.g., DD_API_KEY, DD_APP_KEY>` |
   - **Missing or Unreachable Tool Behavior:** If any configured scanner or monitoring tool is missing, unauthenticated, or unreachable at runtime, Stage 6 and Stage 7 MUST warn explicitly, degrade to `LLM_ONLY` (or local fallback), and log exact proof in the **Tool Execution Ledger** inside `SECURITY_AUDIT.md` and `EVAL_REPORT.md` for human gate review.
3. **Edge Store-and-Forward Buffer (`EDGE-DISCONNECT`) & PII Scrubbing (`OTEL-PII-REDACT`):**
   - Local SQLite buffer (`.sdlc/edge_telemetry_buffer.db`) queues spans and `/api/v1/kaizen/override` payloads during field WAN disconnects and flushes upon reconnect.
   - Deterministic PII redaction callbacks (`before_model_callback` and `before_tool_callback` for ADK apps, or an OpenTelemetry span processor for non-LLM apps) scrub PII, API keys, and bearer tokens before any span is written to disk or exported remotely.
4. **Cloud Outer-Loop Identities & Guardrails (`.sdlc/cloud_outer_loop.json`):**
   - **Stage 7 Eval Identity:** `sa-asdlc-stage7-eval` (`spiffe://<enterprise-trust-domain>/ns/asdlc/sa/stage7-eval`), executing untrusted PR tests exclusively inside an ephemeral Cloud Build gVisor sandbox (`--network=none`).
   - **Stage 8 Kaizen Identity:** `sa-asdlc-stage8-kaizen` (`spiffe://<enterprise-trust-domain>/ns/asdlc/sa/stage8-kaizen`), enforcing `PENDING_KAIZEN_PR` two-phase state commit (`STATE-RACE`), `max_daily_kaizen_prs: 5`, and bot-branch loop prevention (`HITL-GATE-BYPASS`).

---

## 5. BDD Acceptance Scenarios (`Given / When / Then`)
1. **Scenario 1 (Nominal Path + Semantic Routing + Real OpenTelemetry Span Export):**
   - **Given** a valid telemetry query payload,
   - **When** submitted to `POST /api/v1/sdlc/evaluate`,
   - **Then** the Semantic Router selects the optimal Gemini tier in `< 5ms`, scrubs PII via ADK 2.0 callbacks, exports a structured `gen_ai.*` span to the sink in `.sdlc/telemetry_config.json`, and returns `HTTP 200`.
2. **Scenario 2 (Adversarial Threat Defense: Model Armor):**
   - **Given** an input or `/api/v1/kaizen/override` payload containing an indirect prompt injection or SQL injection payload,
   - **When** inspected by the Agent Gateway / Model Armor middleware,
   - **Then** the request is blocked with `HTTP 400` (`model_armor_verdict: BLOCKED_PROMPT_INJECTION`) before reaching any tool, `.sdlc/golden_eval_set.json`, or `AGENTS.md`.
3. **Scenario 3 (Disconnected Edge Store-and-Forward & Stage 8 Kaizen Promotion):**
   - **Given** a valid operator override submitted to `POST /api/v1/kaizen/override` during a simulated WAN dropout,
   - **When** connectivity is restored and Stage 8 (`@kaizen-evolution-agent`) runs,
   - **Then** the buffered override is flushed to `.sdlc/kaizen_overrides.jsonl` (or Cloud Pub/Sub), promoted into `.sdlc/golden_eval_set.json`, and packaged into a `kaizen/loop-*` remediation plan.

---

## 6. Proposed Parallel Builder Decomposition Plan (`1..N` Builders)
| Builder ID (`builder_id`) | Role Title & Technology Focus | Wave | Exclusive Write Glob (`owned_paths`) | Bound `SPEC.md` Contract Sections | Verification Command (`verification_cmd`) |
| :--- | :--- | :---: | :--- | :--- | :--- |
| `fastapi-adk-backend` | FastAPI + Pydantic v2 + ADK + OTel Exporter Backend | `1` | `["backend/**", "tests/backend/**"]` | Sections 2, 3, 4, 5 | `pytest tests/backend -v` |
| `vue-tailwind-frontend` | Vue 3 (`<script setup>`) + Tailwind CSS UI | `1` | `["frontend/**", "tests/frontend/**"]` | Sections 3, 5 | `npm --prefix frontend test` |

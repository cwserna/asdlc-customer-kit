<!-- asdlc_version: "3.1.1" | distribution_tier: "customer-safe" -->
# Master Organizational Runbooks Catalog (`.okf/runbooks/INDEX.md`)

> **Two-Tier Context-Rot Defense (A/SDLC v3.1):**
> * **Tier 1 (`./org-standards.md`, `<= 120 lines`):** Pinned in `.okf/manifest.yaml` and loaded on every turn across Stages 1 to 8.
> * **Tier 2 (`./.okf/runbooks/*.md`):** Deep domain reference standards catalogued below. AI agents read these files on demand only when designing, building, or auditing the corresponding domain.

## 1. Active Domain Runbooks

| Domain Runbook | Scope & Contents | Primary A/SDLC Consumers |
| :--- | :--- | :--- |
| `architecture-and-apis.md` | Approved libraries, service boundaries, OpenAPI/gRPC conventions, error envelopes, pagination, and UI design tokens. | `@spec-architect` (Stage 3), `@parallel-builder-orchestrator` (Stages 4 & 5) |
| `security-and-iam.md` | Identity providers, OAuth/OIDC flows, workload identity, secret rotation, encryption standards, and AI safety rules. | `@spec-architect` (Stage 3), `@security-governance-critic` (Stage 6) |
| `data-and-storage.md` | Database engines, naming conventions, migration rules, PII classification, residency boundaries, and backup SLAs. | `@product-owner` (Stage 2), `@spec-architect` (Stage 3) |
| `testing-and-ci.md` | Unit/integration/E2E testing rules, mock vs. sandbox policies, static analysis tools, and branch protection gates. | `@parallel-builder-orchestrator` (Stage 5), `@eval-telemetry-auditor` (Stage 7) |
| `observability-and-finops.md` | Structured logging fields, OpenTelemetry span attributes, SLO alerting thresholds, and cloud cost tagging rules. | `@eval-telemetry-auditor` (Stage 7), `@kaizen-evolution-agent` (Stage 8) |

## 2. Audit Log of Filtered Process Noise

* `DISCARDED_PROCESS_LOG.md`: Lists administrative and committee procedures from the internal standards website that were intentionally excluded from the AI coding harness because they are not enforceable in source code.

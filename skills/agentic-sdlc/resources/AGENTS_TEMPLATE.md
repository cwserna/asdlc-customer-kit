<!-- asdlc_version: "3.1.1" | distribution_tier: "customer-safe" -->
# Project Harness Rules (`AGENTS.md` / `GEMINI.md`)

> **Equation:** `Agent = Model + Harness`

## 1. Mandatory Pre-Flight Protocol
1. **Read `SPEC.md` & `.sdlc/toolchain_config.json` First:** Never modify backend routes, frontend API calls, security scanner integrations, or OpenTelemetry exporters without verifying `SPEC.md` and `.sdlc/toolchain_config.json`.
2. **Incremental Vertical Slicing:** Keep every modification scoped to `<= 300 LoC` and leave the test suite green after each slice.
3. **No Unsolicited Git Mutations:** Do not run `git commit` or `git push` unless explicitly requested by the developer or governed by Stage-Gate sync rules.

## 2. Cooperating Harness Tuples
- **Full-Stack Tuple:** `backend/` (FastAPI + Pydantic v2 + Google ADK) and `frontend/` (Vue.js 3 + Tailwind CSS) share `SPEC.md`.
- **TDD Tuple:** Every backend slice must pass `pytest backend/tests/test_harness.py` before completion.

## 3. Security, Observability, Toolchain & FinOps Invariants
- **Governance:** Enforce Model Armor input sanitization (when `app_uses_llm: true`), bounded `max_iterations` on all agent loops, and configured customer security scanners in `.sdlc/toolchain_config.json` (falling back via `WARN_AND_DEGRADE_LLM_ONLY` with a mandatory Tool Execution Ledger in `SECURITY_AUDIT.md`).
- **OpenTelemetry:** Wire span export to `.sdlc/telemetry_config.json` `ingest` (`gen_ai.*` attributes when `app_uses_llm: true`, or standard HTTP/RPC/DB OpenTelemetry spans when `app_uses_llm: false`) and verify via `.sdlc/telemetry_config.json` `query` in Stage 7 (`EVAL_REPORT.md`).
- **Cost Optimization:** Route LLM queries via the Semantic Model Router (`gemini-2.5-pro` / `gemini-2.5-flash` / `gemini-2.5-flash-lite`) and preserve deterministic prompt prefixes for 90% Context Caching.

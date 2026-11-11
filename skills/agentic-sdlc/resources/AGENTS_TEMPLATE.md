<!-- asdlc_version: "3.0.0" | distribution_tier: "customer-safe" -->
# Project Harness Rules (`AGENTS.md` / `GEMINI.md`)

> **Equation:** `Agent = Model + Harness` (`: Harness Engineering`)

## 1. Mandatory Pre-Flight Protocol
1. **Read `SPEC.md` First:** Never modify backend routes or frontend API calls without verifying `SPEC.md`.
2. **Incremental Vertical Slicing:** Keep every modification scoped to `<= 300 LoC` and leave the test suite green after each slice.
3. **No Unsolicited Git Mutations:** Do not run `git commit` or `git push` unless explicitly requested by Christian.

## 2. Cooperating Harness Tuples
- **Full-Stack Tuple:** `backend/` (FastAPI + Pydantic v2 + Google ADK) and `frontend/` (Vue.js 3 + Tailwind CSS) share `SPEC.md`.
- **TDD Tuple:** Every backend slice must pass `pytest backend/tests/test_harness.py` before completion.

## 3. Security, Observability & FinOps Invariants
- **Governance (`M2S2`):** Enforce Model Armor input sanitization and bounded `max_iterations` on all agent loops.
- **OpenTelemetry (`M3L5`):** Emit `gen_ai.agent.id`, `gen_ai.operation.name`, `gen_ai.request.model`, `gen_ai.usage.input_tokens`, and `gen_ai.usage.output_tokens`.
- **Cost Optimization (`M3L5`):** Route queries via the Semantic Model Router (`gemini-2.5-pro` / `gemini-2.5-flash` / `gemini-2.5-flash-lite`) and preserve deterministic prompt prefixes for 90% Context Caching.

---
name: agentic-sdlc
asdlc_version: "3.0.0"
distribution_tier: "customer-safe"
description: >-
  Orchestrates the 8-Stage Agentic SDLC (A/SDLC v3.0) workflow, Agent-Driven v1.0-to-v3.0 Smart
  3-Way Upgrade & Definition Validator (--upgrade), Unified 3-Pattern OpenTelemetry
  Sink Configuration (.sdlc/telemetry_config.json), Split-Plane Always-On Cloud Outer Loop for
  Stages 7 & 8 (.sdlc/cloud_outer_loop.json), Mandatory Stage 1 GitHub (or Alternate Git)
  Repository Configuration & Access Validation, Stage-Gate Git Sync, Exhaustive Completion-Driven
  Grilling Per Phase/Stage, Zero-Prebuilt-Code Standalone Workspace Management, and Two-Way Door
  Flight Deck Remote Synchronization (--list, --resume [id|path], --status [id], --park [id],
  --delete [id], --new, --upgrade, --git-setup <url>, --git-status, --git-sync [stage], --outer-loop-init,
  --outer-loop-status, --remote-set <url>, --remote-status, --remote-sync, --remote-remove,
  --clone <project-id> --url <url>) across Stage 1: Project Onboarding, RACI, GitHub Setup,
  Telemetry Sink & Asset Intake, Stage 2: Product Discovery & Requirements, Stage 3: Technical
  Design & API Blueprint, Stage 4: Workspace & Guardrail Setup, Stage 5: Parallel Backend &
  Frontend Coding, Stage 6: Automated Security & Code Review, Stage 7: Testing, Quality & Cost
  Check, and Stage 8: Continuous Improvement & Next Iteration. Trigger whenever the user invokes
  /agentic-sdlc (with or without flags), wants to list, resume, park, inspect, delete, clone,
  upgrade with --upgrade or --outer-loop-init, or remote-sync an A/SDLC project, conduct Stage 1 onboarding,
  GitHub repo setup, and RACI/asset intake, run a Product Owner interview, or coordinate the
  SDLC subagents.
---

# Agentic SDLC (A/SDLC v3.0) Workflow Conductor (Stages 1 to 8)

This skill implements the **8-Stage Agentic SDLC Process (`v3.0`)**, combining Stage 1 Project Onboarding, 6-Role RACI Governance (`RACI.md`), Mandatory GitHub (or Alternate Git) Repository Configuration & Access Validation (`.sdlc/git_config.json`), **Unified 3-Pattern OpenTelemetry Sink Configuration (`.sdlc/telemetry_config.json`)**, **Always-On Cloud Outer-Loop Orchestration for Stages 7 & 8 (`.sdlc/cloud_outer_loop.json`)**, Background Asset & Data Source Intake (`.okf/intake/`), and **Exhaustive Completion-Driven Grilling Per Phase/Stage** with contract-first Spec-Driven Development (`org-standards.md` + `PRD.md` $\rightarrow$ `SPEC.md` $\rightarrow$ `AGENTS.md`), parallel Full-Stack Builder agents, automated Security & Governance review, Evaluation-Driven Development (EDD), and closed-loop Kaizen evolution.

- **System & Infrastructure Architecture Mirror:** [`${REPO_ROOT}/ARCHITECTURE.md`](${REPO_ROOT}/ARCHITECTURE.md)
- **Local Blueprint Mirror:** [`resources/ELEVATE_2026_AGENTIC_SDLC_BLUEPRINT.md`](./resources/ELEVATE_2026_AGENTIC_SDLC_BLUEPRINT.md)
- **Observability Guide:** [`resources/OBSERVABILITY_USER_GUIDE.md`](./resources/OBSERVABILITY_USER_GUIDE.md)
- **GitHub Repository:** [cwserna/agentic-sdlc-harness](https://github.com/cwserna/agentic-sdlc-harness)

> **v3.0 Core Governance Pillars:**
> 1. **100% Standalone Default (Zero Prebuilt Python Code or Cloud Server Required):** All 8 stages, RACI checks, and gate approvals operate natively on plain JSON and Markdown files in the project workspace (`.sdlc/state.json`, `.sdlc/raci.json`, `.sdlc/tech_stack.json`, `.sdlc/git_config.json`, `.sdlc/telemetry_config.json`, `RACI.md`, `org-standards.md`, `PRD.md`, `SPEC.md`, `AGENTS.md`) using standard AI agent tools (`read_file`, `write_file`, `edit_file`, `ask_question`, `run_command`).
> 2. **Mandatory Stage 1 GitHub (or Alternate Git) Repository Configuration, Access Validation & Stage-Gate Git Sync:** Every new project configures and validates a remote Git repository in Stage 1 (defaulting to GitHub via existing repo URL or `gh repo create <owner>/<repo> --private|--public`, or linking an alternate Git provider when specified). Stage 1 verifies local `git config` identity, `gh auth status`, `git ls-remote origin` (read), and `git push --dry-run origin HEAD:refs/heads/main` (write), persisting `.sdlc/git_config.json` (`access_verified: true`) before Gate 1 can be approved. Approving any Stage Gate (`1` through `8`) automatically commits deliverables, tags `stage-<N>-approved`, and pushes to `origin`.
> 3. **Exhaustive Completion-Driven Grilling Per Phase/Stage (No Artificial Round Cap):** Across Stage 1 (`@project-conductor`), Stage 2 (`@product-owner`), Stage 3 (`@spec-architect`), and Stage 4 (`@parallel-builder-orchestrator`), agents keep per-turn pacing gentle (**2 to 3 focused questions per `ask_question` call**) so the stakeholder is never overwhelmed, while **continuing across as many follow-up turns in that phase or stage as needed** until 100% of the phase exit checklist items and conditional follow-ups (including External & Internal Data Source Access Discovery and OpenTelemetry Sink Topology) are completely answered.
> 4. **Unified 3-Pattern OpenTelemetry Sink & Always-On Cloud Outer Loop (`.sdlc/telemetry_config.json` & `.sdlc/cloud_outer_loop.json`):** Connects the running application (`TASK -> SESSION -> TRACE -> SPAN` with `gen_ai.*` attributes) directly to Stage 7 (`@eval-telemetry-auditor`) and Stage 8 (`@kaizen-evolution-agent`) across Pattern A (`LOCAL_FILE_SINK`), Pattern B (`SHARED_REMOTE_SINK`), and Pattern C (`CLOUD_OUTER_LOOP`).
> 5. **Two-Way Door Optional Flight Deck Remote (`--remote-set <url>`, `--remote-status`, `--remote-sync`, `--remote-remove`, `--clone <project-id> --url <url>`):** Any standalone local workspace can attach to a local Docker container or Cloud Run Flight Deck server at any stage (Stages 1 to 8), synchronize state and deliverables over standard REST endpoints (`import-bundle` and `export-bundle`), or detach back to 100% standalone local files without losing state or gate receipts.
>
> **Formatting Rule:** Keep all user-facing prompts, stage summaries, and generated project artifacts (`RACI.md`, `org-standards.md`, `PRD.md`, `SPEC.md`, `AGENTS.md`, `EVAL_REPORT.md`, `KAIZEN_REPORT.md`) in clean, plain engineering language, without internal course or deck codes (such as `M0L1`, `M2S1`, `M3L5`, etc.).

---

## OpenTelemetry & The 3-Pattern Cloud Outer-Loop Architecture (A/SDLC v3.0)

### 1. What OpenTelemetry Is & Why Google Cloud Recommends It
**OpenTelemetry (OTel)** is the open-source Cloud Native Computing Foundation (CNCF) observability framework officially recommended and natively supported by Google Cloud across Cloud Trace, Cloud Logging, Cloud Monitoring, BigQuery, and Vertex AI Agent Engine. In **A/SDLC v3.0**, OpenTelemetry acts as the nervous system connecting a running application (`TASK -> SESSION -> TRACE -> SPAN` with `gen_ai.*` semantic convention attributes such as `gen_ai.agent.id`, `gen_ai.conversation.id`, `gen_ai.operation.name`, `gen_ai.request.model`, `gen_ai.usage.input_tokens`, and `gen_ai.usage.output_tokens`) directly to **Stage 7 (`@eval-telemetry-auditor`)** and **Stage 8 (`@kaizen-evolution-agent`)**.

Before spans leave the application, deterministic **ADK 2.0 `before_model_callback` and `before_tool_callback` hooks** scrub PII, API keys, and bearer tokens (`OTEL-PII-REDACT`), and a local **Edge Store-and-Forward SQLite Buffer** queues spans and operator overrides during field WAN dropouts (`EDGE-DISCONNECT`).

### 2. The 3 Supported Telemetry & Outer-Loop Patterns (`.sdlc/telemetry_config.json`)
To ensure Stage 7 and Stage 8 agents automatically know where to read live telemetry regardless of how a customer deploys their application, **A/SDLC v3.0** configures `.sdlc/telemetry_config.json` in Stage 1 and locks the exporter contract in Stage 3 across three supported topologies:

| Customer Topology | Where the Application Runs | Where Stage 7 & 8 Agents Run | Where OpenTelemetry Is Captured (`sink_type`) | How Stage 7 & 8 Agents Read It Automatically |
| :--- | :--- | :--- | :--- | :--- |
| **Pattern A (`LOCAL_FILE_SINK`)** | 100% local mode (`localhost:8001` or `pytest`) | Developer workstation (Jetski / Antigravity) | Local JSONL files: `.sdlc/otel_traces.jsonl` and `.sdlc/kaizen_overrides.jsonl` | Agents read `.sdlc/telemetry_config.json` and parse `.sdlc/otel_traces.jsonl` and `.sdlc/kaizen_overrides.jsonl` directly via `read_file` or `telemetry_outer_loop.py`. |
| **Pattern B (`SHARED_REMOTE_SINK`)** | Deployed server, Kubernetes, or Cloud Run | Developer workstation (Jetski / Antigravity triggered on demand) | Shared remote sink: Google Cloud Trace / BigQuery, or an OTLP collector (Jaeger, Grafana Tempo, Postgres, or Flight Deck Remote) | Agents read `.sdlc/telemetry_config.json` and pull live `gen_ai.*` spans and sanitized `/api/v1/kaizen/override` events from Cloud Trace, BigQuery, or the configured OTLP collector endpoint into the local session. |
| **Pattern C (`CLOUD_OUTER_LOOP`)** | Deployed in customer cloud | Always-on enterprise cloud deployment in customer GCP (`deploy/cloud_outer_loop/`) | Cloud Trace, BigQuery, and Cloud Pub/Sub + Eventarc | **Stage 7** runs on Cloud Run + an ephemeral Cloud Build gVisor sandbox (`--network=none`) for untrusted PR test execution (`RCE-STAGE7`). **Stage 8** runs on Vertex AI Agent Engine + Cloud Pub/Sub & Eventarc, opening automated `kaizen/loop-*` GitHub Pull Requests with Two-Phase `PENDING_KAIZEN_PR` state commits (`STATE-RACE`) and a `max_daily_kaizen_prs: 5` anti-runaway circuit breaker (`HITL-GATE-BYPASS`). |

### 3. Upgrading Legacy `v1.0 / v2.x` Projects (`/agentic-sdlc --outer-loop-init`)
1. **Safe Local Default (`Pattern A`):** Any `v1.0` or `v2.x` project without `.sdlc/telemetry_config.json` defaults safely to `Pattern A (LOCAL_FILE_SINK)` when resumed via `/agentic-sdlc --resume`.
2. **One-Command Upgrade (`--outer-loop-init`):** Running `/agentic-sdlc --outer-loop-init --pattern <LOCAL_FILE_SINK|SHARED_REMOTE_SINK|CLOUD_OUTER_LOOP>` (or `python3 scripts/sdlc_hud.py --outer-loop-init`) upgrades any existing `v1.0` or `v2.x` workspace in place by writing `.sdlc/telemetry_config.json` and `.sdlc/cloud_outer_loop.json`, seeding `.sdlc/otel_traces.jsonl` and `.sdlc/kaizen_overrides.jsonl`, appending the non-breaking OpenTelemetry exporter delta to `SPEC.md`, and generating `deploy/cloud_outer_loop/` manifests when `CLOUD_OUTER_LOOP` is selected.

---

## Plain-English 8-Stage Overview (`Stages 1 to 8`)

| Stage Name | Description | Responsible AI Subagent (`R`) | Accountable Human Role (`A`) | Next Stage in the Process |
| :--- | :--- | :--- | :--- | :--- |
| **Stage 1: Project Onboarding, RACI, GitHub Setup, Telemetry Sink & Asset Intake** | Initializes the project charter, configures the **6-Role Program & Gate RACI Matrix (`RACI.md`)**, configures and validates the **GitHub (or Alternate Git) Repository (`.sdlc/git_config.json`)** for read/write access, configures the **3-Pattern OpenTelemetry Sink & Cloud Outer-Loop Topology (`.sdlc/telemetry_config.json` & `.sdlc/cloud_outer_loop.json`)**, walks through the **Stage 1 Background Asset & Data Source Intake Checklist** (`org-standards.md`, `.okf/intake/{designs,styles,docs,schemas}/`, and external/internal data source inventory), and runs the **Tech Stack Discovery Side-Quest** to persist `.sdlc/tech_stack.json`. | **Project Conductor Agent** (`@project-conductor`) | **Executive Sponsor / Business Owner** (`executive_sponsor`) | **Stage 2: Product Discovery & Requirements** |
| **Stage 2: Product Discovery & Requirements** | Interviews the stakeholder across 4 completion-driven phases (asking 2 to 3 questions per turn until every phase exit criterion, conditional Data Source Access rule, and OpenTelemetry Observability & Stage 8 Kaizen Feedback SLA is resolved) grounded in Stage 1's ingested designs, style guides, `.sdlc/tech_stack.json`, and `org-standards.md`, and produces a locked **Product Requirements Document (`PRD.md`)**. | **Product Owner Agent** (`@product-owner`) | **Agile Product Owner** (`product_owner`) | **Stage 3: Technical Design & API Blueprint** |
| **Stage 3: Technical Design & API Blueprint** | Translates `PRD.md`, `org-standards.md`, `.sdlc/tech_stack.json`, and `.okf/intake/` assets into a locked **Stack-Adaptive Technical Specification (`SPEC.md`)** that defines data/API/UI contracts, external/internal data source connectivity/auth/sandbox strategies, the **OpenTelemetry Exporter & Cloud Outer-Loop Contract** (`POST /api/v1/kaizen/override`, Edge SQLite buffer, ADK 2.0 PII redaction callbacks, and `sa-asdlc-stage7-eval` / `sa-asdlc-stage8-kaizen` SPIFFE/WIF identities), and the **Proposed Parallel Builder Decomposition Plan** (`1..N` non-overlapping project-specific builders). | **Spec Architect Agent** (`@spec-architect`) | **Lead AI / Systems Architect** (`lead_architect`) | **Stage 4: Workspace, Guardrail & Builder Synthesis** |
| **Stage 4: Workspace, Guardrail & Builder Synthesis** | Dynamically synthesizes `1..N` project-specific builders (sized from `SPEC.md`) in `.sdlc/agents/builders/<builder-id>.md` and `.sdlc/builder_manifest.json`, provisions `deploy/cloud_outer_loop/` manifests and verifies OpenTelemetry sink reachability, enforces Hybrid Gate 4 Roster Approval (`HITL_GATED` vs `AUTONOMOUS_GUARDRAILED`), sets up `AGENTS.md <= 150 lines`, and pins all contracts in `.okf/manifest.yaml` for 90% lower token cost. | **Parallel Builder Orchestrator + Spec Architect + Project Conductor** (`@parallel-builder-orchestrator`, `@spec-architect`, `@project-conductor`) | **Lead AI / Systems Architect** (`lead_architect`) | **Stage 5: Parallel Builder Execution** |
| **Stage 5: Parallel Builder Execution** | Orchestrates concurrent wave execution of the project's synthesized builders (`.sdlc/agents/builders/*.md`) against their exclusive `owned_paths` globs and `SPEC.md` contracts, wiring a real OpenTelemetry `TracerProvider` and `SpanProcessor` (exporting to `.sdlc/otel_traces.jsonl` locally and Cloud Trace/BigQuery in cloud mode) plus `POST /api/v1/kaizen/override`, followed by cross-builder integration verification. | **Parallel Builder Orchestrator** (`@parallel-builder-orchestrator` + `.sdlc/agents/builders/*.md`) | **Engineering Tech Lead** (`tech_lead`) | **Stage 6: Automated Security & Code Review** |
| **Stage 6: Automated Security & Code Review** | Acts as an independent red-team reviewer that inspects all generated code for security flaws, prompt-injection risks, SPIFFE identity rules, ADK 2.0 PII redaction callbacks, and deviations from `SPEC.md` and `org-standards.md`. | **Security & Governance Critic** (`@security-governance-critic`) | **Security & Governance Lead** (`security_lead`) | • **If Passed:** **Stage 7: Testing, Quality & Cost Check**<br>• **If Issues Found:** Returns to **Stage 5 (Coding)** |
| **Stage 7: Testing, Quality & Cost Check** | Runs automated end-to-end tests (locally or inside an ephemeral Cloud Build gVisor sandbox in Pattern C), inspects real captured OpenTelemetry `gen_ai.*` spans from the configured sink in `.sdlc/telemetry_config.json`, tracks AI token spend, and publishes a final **Release Scorecard (`EVAL_REPORT.md`)**. | **Evaluation & Telemetry Auditor** (`@eval-telemetry-auditor`) | **Quality, SRE & FinOps Lead** (`sre_finops_lead`) | **Stage 8: Continuous Improvement & Next Iteration** |
| **Stage 8: Continuous Improvement & Next Iteration** | Ingests live OpenTelemetry traces and Model Armor screened `/api/v1/kaizen/override` events from `.sdlc/telemetry_config.json`, promotes incidents into `.sdlc/golden_eval_set.json`, updates lessons-learned rules (`AGENTS.md <= 150 lines`), opens automated `kaizen/loop-*` GitHub Pull Requests with Two-Phase `PENDING_KAIZEN_PR` state commits in Pattern C, and routes the next improvement back via the 4-Speed Return Loop. | **Kaizen Evolution + Project Conductor** (`@kaizen-evolution-agent` & `@project-conductor`) | **Agile Product Owner** (`product_owner`) | • **Loop 1 (Bug/Guardrail):** → **Stage 4 / Stage 5**<br>• **Loop 2 (Delta Feature):** → **Stage 3 (`SPEC.md`)**<br>• **Loop 3 (Strategic Epic):** → **Stage 2 (`PRD.md`)**<br>• **Loop 4 (Charter/RACI/Assets):** → **Stage 1 (`RACI.md` & `.okf/intake/`)** |

---

## Project Lifecycle, Git Repository, OpenTelemetry Outer-Loop & Two-Way Door Remote Commands (`/agentic-sdlc`)

`@project-conductor` executes every project lifecycle, Git repository setup, OpenTelemetry Outer-Loop configuration, and remote synchronization command **natively using `read_file`, `write_file`, `edit_file`, `ask_question`, `run_command`, and `curl`** when `sdlc_hud.py` is not installed on disk (and can optionally invoke `python3 ${ASDLC_SKILLS_HOME}/agentic-sdlc/scripts/sdlc_hud.py` as a shortcut when the repository is present). Always handle `/agentic-sdlc` flags first:

1. **`/agentic-sdlc --list`:**
   - **Native File Execution:** Read `~/.gemini/asdlc/projects_registry.json` and any local `.sdlc/state.json`, `.sdlc/git_config.json`, `.sdlc/telemetry_config.json`, and `.sdlc/remote.json` files via `read_file` to display the portfolio of projects, including `X/8` approved stages, active frontier stage, session state (`ACTIVE` vs `PARKED`), workspace directory, verified Git repository (`remote_url` and `access_verified`), OpenTelemetry pattern (`LOCAL_FILE_SINK`, `SHARED_REMOTE_SINK`, or `CLOUD_OUTER_LOOP`), and optional Flight Deck remote link.
   - **Optional Script Shortcut (if present):** `python3 ${ASDLC_SKILLS_HOME}/agentic-sdlc/scripts/sdlc_hud.py --list`
2. **`/agentic-sdlc --status [project-id]` or `/agentic-sdlc --project status`:**
   - **Native File Execution:** Read `.sdlc/state.json`, `.sdlc/raci.json`, `.sdlc/git_config.json`, `.sdlc/telemetry_config.json`, `.sdlc/cloud_outer_loop.json`, and `.sdlc/remote.json` (if linked) via `read_file` to render the 8-Stage ASCII Flight HUD, Accountable (`A`) RACI gate owner, verified GitHub/Git repository status, active OpenTelemetry sink pattern, approval channel, tokenomics summary, and clickable deliverable links.
   - **Optional Script Shortcut (if present):** `python3 ${ASDLC_SKILLS_HOME}/agentic-sdlc/scripts/sdlc_hud.py --status [project-id]`
3. **`/agentic-sdlc --resume [project-id-or-path]`:**
   - If `[project-id-or-path]` is omitted, list existing workspaces and call `ask_question` to let the user pick which project to resume.
   - **Native File Execution:** Read `.sdlc/state.json`, `RACI.md`, `.sdlc/git_config.json`, `.sdlc/telemetry_config.json` (defaulting safely to `Pattern A: LOCAL_FILE_SINK` if absent on a legacy `v1.0/v2.x` workspace), `.okf/intake/ASSET_MANIFEST.md`, completed `PRD.md`/`SPEC.md`, and any `pending_revision_notes` via `read_file`, and write `.sdlc/session_checkpoint.json` and `.sdlc/RESUME_BRIEF.md` via `write_file` (or run `python3 ${ASDLC_SKILLS_HOME}/agentic-sdlc/scripts/sdlc_hud.py --resume "<project-id-or-path>"` if present).
   - Display the 8-Stage ASCII HUD and immediately call `ask_question` with the **4-Option Next-Action Picker**:
     1. `(Recommended) Run / Re-run Active Stage Agent (@<agent>)` (or `Approve Stage Gate & Advance` if `STAGE_COMPLETE_AWAITING_SIGN_OFF`)
     2. `Approve Active Stage Gate as Accountable (A) Owner & Advance`
     3. `Jump to a Specific Stage (Stages 1 to 8) or Trigger a Stage 8 Kaizen Loop`
     4. `Park / Exit Project and Save Session Checkpoint (.sdlc/RESUME_BRIEF.md)`
4. **`/agentic-sdlc --park [project-id]`:**
   - **Native File Execution:** Update `.sdlc/state.json` (`status: "PARKED"`) and write `.sdlc/session_checkpoint.json` and `.sdlc/RESUME_BRIEF.md` via `write_file` (or run `python3 ${ASDLC_SKILLS_HOME}/agentic-sdlc/scripts/sdlc_hud.py --park [project-id] --note "<handoff notes>"` if present) so the user can resume seamlessly from any surface later.
5. **`/agentic-sdlc --delete [project-id]`:**
   - Protected built-in DVR reference cartridges (`permian-rig-triage-demo`) cannot be deleted.
   - Always use `ask_question` to confirm the **Two-Tier Delete Mode** before executing:
     - **Option 1 (`UNREGISTER`, Recommended):** Removes the project from `projects_registry.json` while keeping all workspace files on disk so it can be re-attached later via `--resume <path>`.
     - **Option 2 (`PURGE_DISK`):** Archives compliance artifacts, removes the project from the registry, and permanently deletes the workspace directory from disk (`--mode PURGE_DISK --confirm-purge`).
6. **`/agentic-sdlc` (No Flags) vs `/agentic-sdlc --new`:**
   - When invoked with `--new`, jump directly to **Stage 1: Project Onboarding, RACI, GitHub Setup, Telemetry Sink & Background Asset Intake** below.
   - When invoked as bare `/agentic-sdlc` without flags and existing projects are present, first call `ask_question` to ask whether the user wants to:
     - `(Recommended) Resume an Existing Project` (listing the active/registered projects with their current `Stage X/8` status), or
     - `Create a New Project (Start Stage 1 Onboarding)`.
7. **`/agentic-sdlc --git-setup <url-or-owner/repo>` & `--git-status` & `--git-sync [stage]`:**
   - **`--git-setup`:** Links an existing GitHub/Git repository URL (`--git-mode existing`) or creates a new GitHub repository (`--git-mode create-github --git-visibility private|public`), verifies read (`git ls-remote origin`) and write (`git push --dry-run origin HEAD:refs/heads/main`) access, and writes `.sdlc/git_config.json` (`python3 scripts/sdlc_hud.py --git-setup <url-or-slug> --git-mode existing|create-github`).
   - **`--git-status`:** Re-verifies live read and write access to the configured `origin` remote and prints `.sdlc/git_config.json` (`python3 scripts/sdlc_hud.py --git-status`).
   - **`--git-sync [stage]`:** Commits current stage deliverables, creates an annotated tag (`stage-<N>-approved`), and pushes the branch and tag to `origin` (`python3 scripts/sdlc_hud.py --git-sync [stage]`).
8. **`/agentic-sdlc --outer-loop-init` & `/agentic-sdlc --outer-loop-status` (A/SDLC v3.0 Telemetry Sink & Cloud Outer-Loop Management):**
   - **`--outer-loop-init`:** Upgrades any new or existing `v1.0 / v2.x` workspace to **A/SDLC v3.0** by configuring `.sdlc/telemetry_config.json` (`LOCAL_FILE_SINK`, `SHARED_REMOTE_SINK`, or `CLOUD_OUTER_LOOP`) and `.sdlc/cloud_outer_loop.json`, seeding `.sdlc/otel_traces.jsonl` and `.sdlc/kaizen_overrides.jsonl`, verifying live GCP project and sink access for Patterns B and C, appending the OpenTelemetry exporter contract delta to `SPEC.md`, and generating `deploy/cloud_outer_loop/` manifests (`python3 scripts/sdlc_hud.py --outer-loop-init --pattern <LOCAL_FILE_SINK|SHARED_REMOTE_SINK|CLOUD_OUTER_LOOP> --gcp-project <id>`).
   - **`--outer-loop-status`:** Reads `.sdlc/telemetry_config.json` and `.sdlc/cloud_outer_loop.json`, inspects captured `gen_ai.*` spans and sanitized override events from the active sink, and displays `PENDING_KAIZEN_PR` lock state and daily Kaizen PR circuit-breaker counters (`python3 scripts/sdlc_hud.py --outer-loop-status`).
9. **`/agentic-sdlc --remote-set <url>` (Attach Standalone Project to Optional Flight Deck Remote):**
   - **Native Execution (`write_file` + `curl`):** Read `RACI.md` and `.sdlc/raci.json` via `read_file` to count distinct human assignees (`1` distinct human selects `enforcement_policy: "ADVISORY_SYNC"`, while `2+` distinct humans select `enforcement_policy: "TEAM_STRICT"`). Write `.sdlc/remote.json` containing `remote_url`, `project_id`, `owner_email`, `hostname`, `local_workspace_path`, and `enforcement_policy` via `write_file`, and push the current workspace bundle via `curl -fsSL -X POST <url>/api/v1/sdlc/projects/import-bundle -H "Content-Type: application/json" -d @.sdlc/bundle_payload.json` (or run `python3 scripts/sdlc_hud.py --remote-set <url>` if present).
10. **`/agentic-sdlc --remote-status` & `/agentic-sdlc --remote-sync`:**
    - **`--remote-status`:** Read `.sdlc/remote.json` via `read_file` and query `curl -fsSL <url>/api/v1/sdlc/projects/<id>/state` to display the remote Flight Deck URL, `enforcement_policy` (`ADVISORY_SYNC` vs `TEAM_STRICT`), and remote vs local `state_version` (or run `python3 scripts/sdlc_hud.py --remote-status` if present).
    - **`--remote-sync`:** Push local `.sdlc/state.json` and workspace Markdown files (`PRD.md`, `SPEC.md`, `RACI.md`, `AGENTS.md`, `org-standards.md`) to `curl -fsSL -X POST <url>/api/v1/sdlc/projects/import-bundle` and pull any newer remote gate approvals via `curl -fsSL <url>/api/v1/sdlc/projects/<id>/export-bundle` (or run `python3 scripts/sdlc_hud.py --remote-sync` if present).
11. **`/agentic-sdlc --remote-remove` (Detach Back to 100% Standalone Local Mode):**
    - **Native Execution (`curl` + `write_file`):** Pull the latest state and gate receipts via `curl -fsSL <url>/api/v1/sdlc/projects/<id>/export-bundle`, write the hydrated `.sdlc/state.json` and `workspace_files` locally via `write_file`, remove `.sdlc/remote.json`, and continue 100% standalone locally (or run `python3 scripts/sdlc_hud.py --remote-remove` if present).
12. **`/agentic-sdlc --clone <project-id> --url <url>` (Hydrate Local Workspace from Remote Flight Deck):**
    - **Native Execution (`curl` + `write_file`):** Fetch `curl -fsSL <url>/api/v1/sdlc/projects/<project-id>/export-bundle`, write all `workspace_files` (`PRD.md`, `SPEC.md`, `RACI.md`, `AGENTS.md`, `org-standards.md`), `.sdlc/state.json`, `.sdlc/raci.json`, `.sdlc/tech_stack.json`, `.sdlc/git_config.json`, `.sdlc/telemetry_config.json`, and `.sdlc/remote.json` to disk using `write_file`, and begin working locally (or run `python3 scripts/sdlc_hud.py --clone <project-id> --url <url>` if present).
13. **`/agentic-sdlc --upgrade` & Silent Startup Version Check (`v1.0`/`v2.x` to `v3.0.0` Smart 3-Way Agent Merge + Workspace Migration):**
    - **Silent Startup Version Check:** At the beginning of every `/agentic-sdlc` session, inspect the `asdlc_version` field in the YAML frontmatter of the user's installed `~/.gemini/config/agents/*.md` and `~/.gemini/config/skills/*/SKILL.md` (or `.agent/`). If `asdlc_version` is absent (`v1.0` or `v2.x`) or lower than `"3.0.0"`, notify the user and offer to run `/agentic-sdlc --upgrade`.
    - **Phase A: Smart 3-Way Agent & Skill Definition Merge:**
      1. Back up all existing installed agent and skill definitions to `~/.gemini/config/.backups/asdlc-upgrade-<timestamp>/`.
      2. Compare each installed agent and skill `.md` file against the canonical `v3.0.0` definitions (`asdlc_version: "3.0.0"`). If the user previously added organization-specific rules or custom instructions inside a `v1.0` agent definition, extract those custom additions and migrate them into the active project's `org-standards.md` or `AGENTS.md` so zero custom context is lost.
      3. After user confirmation via `ask_question`, write the clean `v3.0.0` agent and skill definitions into `~/.gemini/config/agents/` and `~/.gemini/config/skills/` (or `.agent/`).
      4. **Mandatory `v1.0` Skill Reload Notice:** Because `v1.0` users initially had the legacy `v1.0` `agentic-sdlc` skill loaded in session memory, explicitly instruct the user after writing the new `v3.0.0` files to **reload the `agentic-sdlc` skill (or start a fresh chat session)** so the newly installed `v3.0.0` skill and subagent definitions take effect in memory.
    - **Phase B: Full Non-Destructive `v1.0` Project Workspace Migration:**
      1. Convert 0-indexed `v1.0` stages (`Stage 0` to `Stage 6`) to 1-indexed `v3.0` stages (`Stage 1` to `Stage 8`) in `.sdlc/state.json`.
      2. Non-destructively scaffold missing `v3.0` governance and telemetry files: `RACI.md`, `.sdlc/raci.json`, `.sdlc/git_config.json`, and `.sdlc/telemetry_config.json` (defaulting to `LOCAL_FILE_SINK` with `pii_redaction_enabled: true`).
      3. Offer to append the `v3.0` Day-2 Observability & OpenTelemetry sections to existing `PRD.md` (Section 7) and `SPEC.md` (Section 5) files.

---

## Step-by-Step Execution Runbook

### Stage 1: Project Onboarding, RACI, GitHub Setup, Telemetry Sink & Background Asset Intake (`@project-conductor`)
Whenever the user asks to **bootstrap a new project**, **start a new A/SDLC project**, or run **`a-sdlc`** on a new workspace:
1. **Turn 1: Ask for an Open-Ended Description of the Application, GitHub Repository, Telemetry Topology & Stage 1 Background Assets First (if not already provided in the prompt):**
   - **NEVER** start Turn 1 with a multiple-choice radio button selector for the application idea.
   - Output this exact Stage 1 opening prompt in plain text (without calling `ask_question` on Turn 1):
     ```markdown
     ### 8-Stage Agentic SDLC (A/SDLC v3.0) Workflow Ready

     We will run the 8-stage pipeline (Stage 1: Project Onboarding, RACI, GitHub Setup, Telemetry Sink & Asset Intake → Stage 2: Product Discovery → Stage 3: Technical Blueprint → Stage 4: Workspace & Guardrail Setup → Stage 5: Parallel Builder Execution → Stage 6: Security & Governance Review → Stage 7: Testing, Quality & FinOps → Stage 8: Kaizen Continuous Evolution).

     ### Stage 1: Tell Me What You Want to Build, Your GitHub Repo, Telemetry Mode & Background Assets

     Before we configure the workspace, assign the 6-role RACI matrix, validate your GitHub repository, configure your OpenTelemetry sink, and ingest your background assets, please describe in plain text:

     1. **Application Idea, Target Users & Core Problem:** What application do you want to build, who are the primary users, and what business or operational problem are we solving?
     2. **GitHub (or Alternate Git) Repository:** Would you like to link an existing GitHub repository URL (`https://github.com/<owner>/<repo>`), have me create a new GitHub repository (`<owner>/<repo>`), or configure an alternate Git host?
     3. **OpenTelemetry & Outer-Loop Pattern (`.sdlc/telemetry_config.json`):** Will this project run in Pattern A (`LOCAL_FILE_SINK` for 100% local prototyping), Pattern B (`SHARED_REMOTE_SINK` for a deployed app with local Stage 7/8 agents), or Pattern C (`CLOUD_OUTER_LOOP` for Always-On Cloud Run + Vertex AI Agent Engine Stage 7/8 automation)?
     4. **Organizational Standards (`org-standards.md`) & Background Assets (`.okf/intake/`):** Local file path or Google Doc URL to your organization's `org-standards.md`, plus any UI/UX wireframes, style guides, domain runbooks, API/database schemas, or external/internal data sources.
     ```
2. **Turn 2+ (Exhaustive Completion-Driven Stage 1 Grilling at 2 to 3 Questions per Turn):**
   - Once the user describes the application they want to build, **grill them via `ask_question` in batches of 2 to 3 focused questions per turn**, continuing across as many follow-up turns as needed until **all 7 Stage 1 Exit Criteria** are completely resolved:
     1. **Project Identity & Target Workspace Path**
     2. **6-Role Human RACI Matrix & Multi-Channel Approval Routing (`RACI.md`, `.sdlc/raci.json`, `.sdlc/approval_workflows.json`)**
     3. **Governance Execution Policy (`HITL_GATED` vs `AUTONOMOUS_GUARDRAILED`) & Optional Flight Deck Remote**
     4. **GitHub (or Alternate Git) Repository Configuration & Verified Read/Write Access (`.sdlc/git_config.json` with `access_verified: true`)**
     5. **Organizational Standards (`org-standards.md`), Tech Stack Profile (`.sdlc/tech_stack.json`) & Background Assets (`.okf/intake/`)**
     6. **External & Internal Data Source Inventory** (identifying every partner/distributor API, SaaS system, ERP/CRM, or internal database and whether sample payloads exist or credentials/sandboxes must be provisioned)
     7. **Unified OpenTelemetry Sink & Cloud Outer-Loop Configuration (`.sdlc/telemetry_config.json` & `.sdlc/cloud_outer_loop.json`)** (selecting `LOCAL_FILE_SINK`, `SHARED_REMOTE_SINK`, or `CLOUD_OUTER_LOOP`, and verifying live GCP project and sink access when Pattern B or Pattern C is selected)
3. **Scaffold the Stage 1 Workspace Files & Validate Git and Telemetry Access (`write_file` + `git`/`gh` or `bootstrap_harness.py`):**
   - **Default Native Path (`write_file` + `git`/`gh`):** Directly write `.sdlc/state.json`, `.sdlc/raci.json`, `.sdlc/tech_stack.json`, `.sdlc/git_config.json`, `.sdlc/telemetry_config.json`, `.sdlc/cloud_outer_loop.json`, `.sdlc/otel_traces.jsonl`, `.sdlc/kaizen_overrides.jsonl`, `RACI.md`, `org-standards.md`, `.okf/intake/ASSET_MANIFEST.md`, `PRD.md`, `SPEC.md`, `AGENTS.md` (`<= 150 lines`), `.okf/manifest.yaml`, and `.sdlc/golden_eval_set.json`, initialize `.git` (`git init -b main`), link or create the remote repository (`gh repo create` or `git remote add origin`), and validate read (`git ls-remote origin`) and write (`git push --dry-run origin HEAD:refs/heads/main`) access.
   - **Optional Script Shortcut (if `scripts/bootstrap_harness.py` is installed on disk):**
     ```bash
     python3 ${ASDLC_SKILLS_HOME}/agentic-sdlc/scripts/bootstrap_harness.py \
       --project-name "<Project Name>" \
       --target-dir "<Target Directory>" \
       --org-standards "<Local Path to org-standards.md>" \
       --git-remote "<https://github.com/owner/repo or owner/repo>" \
       --repo-mode <existing|create-github> \
       --repo-visibility <private|public> \
       --telemetry-pattern <LOCAL_FILE_SINK|SHARED_REMOTE_SINK|CLOUD_OUTER_LOOP> \
       --gcp-project "<Optional GCP Project ID for Patterns B/C>" \
       --designs-dir "<Optional Designs Path>" \
       --style-guide "<Optional Style Guide Path>" \
       --docs-dir "<Optional Docs Path>" \
       --policy <HITL_GATED|AUTONOMOUS_GUARDRAILED>
     ```
4. **Gate 1 Sign-Off, Git Tag (`stage-1-approved`) & Transition to Stage 2 (`@product-owner`):**
   - Once all 7 Stage 1 Exit Criteria are satisfied, `.sdlc/git_config.json` has `access_verified: true`, and `.sdlc/telemetry_config.json` is verified, record Gate 1 approval by `executive_sponsor`, commit and push `stage-1-approved` to `origin`, and launch the **Stage 2 Product Owner 4-Phase Discovery Interview**.

### Stage 2: Product Discovery & Requirements (`@product-owner` -> `PRD.md`)
1. **Ground in Stage 1 Assets (`org-standards.md`, `RACI.md`, `.sdlc/git_config.json`, `.sdlc/telemetry_config.json` & `.okf/intake/`):** Reads `org-standards.md` and `.okf/intake/ASSET_MANIFEST.md` (designs, style guides, domain docs, schemas, and Stage 1 data source inventory) so the Product Owner interview builds directly on existing organizational and design context.
2. **4-Phase Completion-Driven Stakeholder Discovery Interview (2 to 3 Questions/Turn, No Turn Cap):** Interviews the stakeholder across 4 digestible phases (Phase 1: Vision, KPIs & `org-standards.md`; Phase 2: High-Level Scope, Epics, Data Source Access Rules & OpenTelemetry / Stage 8 Kaizen Feedback SLA; Phase 3: MoSCoW User Stories & Given/When/Then Criteria; Phase 4: `PRD.md` Handoff). Never advance to the next phase until 100% of that phase's exit checklist items (including Read vs. Write-Back Boundary, Role & Tenant Scoping, Freshness & Sync SLA for every data source, and which operator overrides, thumbs-down actions, or latency breaches trigger Stage 8 Kaizen evolution) are answered.
3. **Generate `PRD.md` Citation, Gate 2 Git Sync (`stage-2-approved`) & Handoff:** Cites the enforced `org-standards.md` policies, `.sdlc/telemetry_config.json` pattern, and `.okf/intake/` assets in **Section 1** and **Section 5** of `PRD.md` via [`resources/PRD_TEMPLATE.md`](./resources/PRD_TEMPLATE.md), records Stage 2 sign-off by the Accountable **Agile Product Owner (`product_owner`)**, pushes `stage-2-approved` to `origin`, and hands off to `@spec-architect` (Stage 3).

### Stage 3: Technical Design & API Blueprint (`@spec-architect` -> `SPEC.md`)
1. **Completion-Driven Technical, Data Source & OpenTelemetry Grilling (2 to 3 Questions/Turn Until 100% Resolved):** Before generating `SPEC.md`, asks 2 to 3 focused questions per turn across as many turns as needed until all Stage 3 Exit Checklist items are resolved (Problem-First KPIs, Protocol & Schema, Authentication & Secret Management, Network & Residency Boundary, Stage 5/7 Sandbox vs. Deterministic Contract Mock Strategy, API Failure Modes, UI/`A2UI` states, **OpenTelemetry Exporter & Cloud Outer-Loop Contract**, and Parallel Builder Decomposition).
2. Translates `PRD.md`, `org-standards.md`, `.sdlc/tech_stack.json`, `.sdlc/telemetry_config.json`, and `.okf/intake/{designs,styles,schemas}/` into a locked Stack-Adaptive Technical Specification (`SPEC.md`) across the **4-Layer Agentic Architecture**, locking the dual OpenTelemetry exporter (`.sdlc/otel_traces.jsonl` + Cloud Trace/BigQuery), `POST /api/v1/kaizen/override` + Edge Store-and-Forward SQLite buffer schema, ADK 2.0 PII redaction callbacks, `sa-asdlc-stage7-eval` / `sa-asdlc-stage8-kaizen` SPIFFE/WIF identities, and a **`## Proposed Parallel Builder Decomposition Plan`** (`1..N` non-overlapping project-specific builders dynamically sized from `SPEC.md`) using [`resources/SPEC_TEMPLATE.md`](./resources/SPEC_TEMPLATE.md), signed off by `lead_architect` and synced to `origin` (`stage-3-approved`).

### Stage 4: Workspace, Guardrail, Cloud Outer-Loop & Dynamic Builder Synthesis (`@parallel-builder-orchestrator` + `@spec-architect` + `@project-conductor`)
1. Synthesizes `1..N` project-specific builders (dynamically sized from `SPEC.md`) in `.sdlc/agents/builders/<builder-id>.md` and `.sdlc/builder_manifest.json`, asks 2 to 3 clarifying questions if any `owned_paths`, data-source mock boundaries, or `verification_cmd` rules are ambiguous, provisions `deploy/cloud_outer_loop/` manifests and verifies OpenTelemetry sink reachability at Gate 4, enforces Hybrid Gate 4 Roster Approval (`HITL_GATED` vs `AUTONOMOUS_GUARDRAILED`), generates `AGENTS.md` (`<= 150 lines`), pins all contracts in `.okf/manifest.yaml` for **90% lower token cost**, and pushes `stage-4-approved` to `origin`.

### Stage 5: Parallel Builder Execution (`@parallel-builder-orchestrator` & `.sdlc/agents/builders/*.md`)
1. Call `invoke_subagent` with `@parallel-builder-orchestrator` to execute all synthesized builders in parallel waves (`+81%` parallel speed boost) against their exclusive `owned_paths` globs and `SPEC.md` contracts, wiring real OpenTelemetry `TracerProvider` and `SpanProcessor` exporters (writing to `.sdlc/otel_traces.jsonl` locally and Cloud Trace/BigQuery in cloud mode), ADK 2.0 PII redaction callbacks, and `POST /api/v1/kaizen/override`, followed by cross-builder integration verification, sign-off by the Accountable **Engineering Tech Lead (`tech_lead`)**, and Git sync (`stage-5-approved`).

### Stage 6: Automated Security & Code Review (`@security-governance-critic`)
1. Invoke `TypeName: "security-governance-critic"` via `invoke_subagent` to audit code against `org-standards.md`, the **4 CISO Security Interrogatives**, **6 Stack-Wide Agentic Threat Vectors**, **Model Armor**, **ADK 2.0 PII Redaction Callbacks (`OTEL-PII-REDACT`)**, and `SECURITY_AUDIT.md` (plus optional `scripts/cm_triage.py` if present), signed off by the Accountable **Security & Governance Lead (`security_lead`)** and synced to `origin` (`stage-6-approved`).

### Stage 7: Testing, Quality & Cost Check (`@eval-telemetry-auditor`)
1. Runs automated test suites (`pytest`, `vitest`, `go test`, or stack-native runner for the `>= 35%` test-to-code benchmark; executed inside an ephemeral Cloud Build gVisor sandbox with `--network=none` when running in Pattern C), 7-Dimension Evaluation-Driven Development (EDD), real OpenTelemetry `gen_ai.*` span inspection from the configured sink in `.sdlc/telemetry_config.json`, and 90% Context Cache FinOps verification, writing `EVAL_REPORT.md` via `write_file` (and optionally running `python3 ${ASDLC_SKILLS_HOME}/agentic-sdlc/scripts/verify_sdlc_gates.py --project-dir <PROJECT_DIR>` if present), signed off by the Accountable **Quality, SRE & FinOps Lead (`sre_finops_lead`)** and synced to `origin` (`stage-7-approved`).

### Stage 8: Continuous Improvement & Next Iteration (`@kaizen-evolution-agent` + `@project-conductor`)
1. Executes **Systematic Hillclimbing** by reading live OpenTelemetry traces and Model Armor screened `/api/v1/kaizen/override` events from the configured sink in `.sdlc/telemetry_config.json`, updating `AGENTS.md` (`<= 150 lines`) and `.sdlc/golden_eval_set.json`, opening an automated `kaizen/loop-*` GitHub Pull Request with Two-Phase `PENDING_KAIZEN_PR` state commit in Pattern C (`max_daily_kaizen_prs: 5`), syncing `stage-8-approved` to `origin`, and routing work via the **4-Speed Return Loop**:
   - **Quick Bug / Guardrail Fix (Loop 1 → Stage 4 / Stage 5):** Fixes a bug or harness rule without changing `SPEC.md`.
   - **Delta Feature (Loop 2 → Stage 3: Technical Design & API Blueprint):** Updates `SPEC.md` first for a new endpoint or UI screen, then triggers Stage 5 coding.
   - **Strategic Epic (Loop 3 → Stage 2: Product Discovery & Requirements):** Updates `PRD.md` and `BACKLOG.md` for a new user persona or major capability wave.
   - **Charter, RACI or Design/Style Asset Refresh (Loop 4 → Stage 1: Project Onboarding, RACI & Asset Intake):** Updates `RACI.md`, `org-standards.md`, `.sdlc/telemetry_config.json`, or `.okf/intake/` design/style assets.

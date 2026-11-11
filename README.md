<!-- asdlc_version: "3.0.0" | distribution_tier: "customer-safe" -->
# 🚀 The Agentic SDLC (A/SDLC v3.0.0): Customer-Safe Pure Markdown Kit

> **Distribution Tier:** `customer-safe` (`100% Pure Markdown`, Zero Executable Scripts Required)
> **Release Version:** `v3.0.0` ([`VERSION`](./VERSION) • [`UPGRADE.md`](./UPGRADE.md))
> **Supported Harnesses:** Google Antigravity IDE/CLI, Gemini CLI, and any Markdown-compatible AI coding harness.

---

## 1. What Is Included in This Customer-Safe Kit

This repository contains the **100% Pure Markdown Customer-Safe Edition** of the **8-Stage Agentic Software Development Lifecycle (A/SDLC v3.0.0)**. Every file in this kit is human-readable plain-text Markdown (`.md`) so enterprise security and governance teams can audit and approve it immediately without reviewing third-party Python or shell scripts.

### 1.1 The 8 Specialist AI Subagents (`agents/`)
| Subagent File | Stage Ownership | Role Summary |
| :--- | :--- | :--- |
| [`agents/project-conductor.md`](./agents/project-conductor.md) | **Stages 1, 4 & 8** | Project Onboarding, Git Repo Validation, 3-Pattern OpenTelemetry Sink Setup, 6-Role RACI, 6-Pillar Intake, and `v1.0 -> v3.0` Smart Upgrade Conductor (`@project-conductor`). |
| [`agents/product-owner.md`](./agents/product-owner.md) | **Stage 2** | Agile Product Owner conducting the 4-Phase Socratic discovery interview to produce `PRD.md` (`@product-owner`). |
| [`agents/spec-architect.md`](./agents/spec-architect.md) | **Stages 3 & 4** | Lead AI Architect authoring locked `SPEC.md`, OpenTelemetry/Outer-Loop contracts, and `AGENTS.md` (`@spec-architect`). |
| [`agents/parallel-builder-orchestrator.md`](./agents/parallel-builder-orchestrator.md) | **Stages 4 & 5** | Synthesizes `1..N` project-specific builders in `.sdlc/agents/builders/` and orchestrates parallel coding waves (`@parallel-builder-orchestrator`). |
| [`agents/security-governance-critic.md`](./agents/security-governance-critic.md) | **Stage 6** | Adversarial Red-Team Reviewer auditing prompt injection, SPIFFE/WIF IAM, Model Armor guardrails, and PII redaction (`@security-governance-critic`). |
| [`agents/eval-telemetry-auditor.md`](./agents/eval-telemetry-auditor.md) | **Stage 7** | 7-Dimension Evaluation-Driven Development (EDD), OpenTelemetry span verification, and FinOps cost auditor (`@eval-telemetry-auditor`). |
| [`agents/kaizen-evolution-agent.md`](./agents/kaizen-evolution-agent.md) | **Stage 8** | Continuous Evolution, Golden Eval Set promoter, and Loop 1 to 4 router (`@kaizen-evolution-agent`). |
| [`agents/adversarial-doc-critic.md`](./agents/adversarial-doc-critic.md) | **Cross-Stage** | 4-Lens Adversarial Document & Architecture Critic (`@adversarial-doc-critic`). |

### 1.2 The 4 Core Skills & 6 Stage Templates (`skills/`)
* [`skills/agentic-sdlc/SKILL.md`](./skills/agentic-sdlc/SKILL.md): Primary `/agentic-sdlc` workflow conductor (`--new`, `--resume`, `--status`, `--list`, `--park`, `--upgrade`, `--outer-loop-init`).
* [`skills/asdlc-onboarding-coach/SKILL.md`](./skills/asdlc-onboarding-coach/SKILL.md): Pre-flight environment, Google Cloud, Git/GitHub, and OpenTelemetry readiness coach (`/asdlc-onboarding-coach`).
* [`skills/product-owner/SKILL.md`](./skills/product-owner/SKILL.md): Stage 2 Product Owner interview skill (`/product-owner`).
* [`skills/review-council/SKILL.md`](./skills/review-council/SKILL.md): Blind Adversarial Review Council skill (`/review-council`).
* [`skills/agentic-sdlc/resources/`](./skills/agentic-sdlc/resources/): Standardized Markdown templates (`RACI_TEMPLATE.md`, `ASSET_MANIFEST_TEMPLATE.md`, `ORG_STANDARDS_TEMPLATE.md`, `PRD_TEMPLATE.md`, `SPEC_TEMPLATE.md`, `AGENTS_TEMPLATE.md`).

---

## 2. Quickstart: New Installation vs. Upgrading from `v1.0`

### Option A: Fresh Installation (New Users)
Copy `agents/*.md` and `skills/*` into your AI harness configuration directory (`~/.gemini/config/` or `.agent/` inside your workspace), start a new chat session, and run:
1. `/asdlc-onboarding-coach` to verify your Google Cloud, Git/GitHub, and OpenTelemetry readiness.
2. `/agentic-sdlc --new` to launch Stage 1 Project Onboarding.

### Option B: Upgrading from `v1.0` or `v2.x` (Agent-Driven Smart 3-Way Merge)
If you already have `A/SDLC v1.0` (or `v2.x`) installed, see [`UPGRADE.md`](./UPGRADE.md). Open your AI chat inside this repository folder and paste:
```text
Read ./UPGRADE.md and ./skills/agentic-sdlc/SKILL.md in this v3.0.0 repository and execute the Smart 3-Way Agent & Workspace Upgrade against my installed ~/.gemini/config/ (or .agent/) definitions and my active A/SDLC project workspaces.
```
After Step 1 finishes updating your installed files, **start a new chat session (or reload the `agentic-sdlc` skill)** so the `v3.0.0` definitions load into memory.

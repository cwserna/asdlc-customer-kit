<!-- asdlc_version: "3.0.0" | distribution_tier: "customer-safe" -->
# 📦 Stage 1 Onboarding & Background Asset Manifest (`ASSET_MANIFEST.md`) — <Project / Application Title>

- **Project:** `<Project / Application Title>`
- **Managed By:** `@project-conductor` (Stage 1 Onboarding & Continuous PMO Overwatch)
- **Schema Version:** `2.0.0`

## 1. Stage 1 Background Asset Intake Checklist

- [x] **1. Organizational Development Standards (`org-standards.md`)** (Tech stack rules, cloud architecture guardrails, security compliance, and testing standards)
- [ ] **2. UI/UX Designs, Mockups & Wireframes (`.okf/intake/designs/`)** (Screen layouts, user flows, Figma links, component wireframes, and system topology diagrams)
- [ ] **3. Brand Guidelines & Style Guides (`.okf/intake/styles/`)** (Color palettes, typography tokens, Tailwind theme presets, dark/light mode rules, and voice/tone)
- [ ] **4. Domain Runbooks & Reference Docs (`.okf/intake/docs/`)** (Existing PRDs, SOPs, domain glossaries, legacy runbooks, and stakeholder briefing decks)
- [ ] **5. Existing API Schemas & Data Contracts (`.okf/intake/schemas/`)** (OpenAPI specs, SQL DDL schemas, BigQuery/Spanner definitions, and sample JSON payloads)
- [ ] **6. External & Internal Data Source Inventory (`.okf/intake/schemas/` & `ASSET_MANIFEST.md`)** (Upstream/downstream internal databases, partner/distributor REST APIs, MCP servers, file feeds, and whether non-production sandboxes or sanitized sample payloads exist for Stage 2 `@product-owner` and Stage 3 `@spec-architect`)
- [x] **7. Mandatory GitHub / Git Repository Configuration (`.sdlc/git_config.json`)** (Validated remote repository URL, branch, and verified read/write push access `access_verified: true`)

## 2. Ingested Asset Inventory (`.okf/intake/`)

| Asset ID | Category | Title | Workspace Path | External Link / Source |
| :--- | :--- | :--- | :--- | :--- |
| `asset-org-standards` | `org_standards` | **Organizational Development Standards (`org-standards.md`)** | `org-standards.md` | Local File |

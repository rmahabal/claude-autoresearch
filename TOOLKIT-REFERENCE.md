# FinBlocks — Complete Toolkit Reference

> Master inventory of all Claude Code plugins, skills, commands, and integrations installed for the FinBlocks project. Last updated: 2026-03-25.

---

## Quick Navigation

| Category | Count | Source |
|----------|-------|--------|
| [Autonomous Loops](#autonomous-loops) | 2 plugins, 11 commands | autoresearch + Ralph Wiggum |
| [PM Skills — Core](#pm-skills--core-68-skills) | 68 skills | rmahabal/pm-skills |
| [PM Skills — Advanced](#pm-skills--advanced-43-skills) | 43 skills | rmahabal/product-manager-skills |
| [Visual & Docs](#visual--document-generation) | 8 commands | visual-explainer |
| [MCP Integrations](#mcp-integrations) | 3 servers | GitHub, Slack, Linear |
| [Custom FinBlocks Commands](#custom-finblocks-commands) | 8 commands | Project-specific |
| **Total** | **143 skills + commands** | |

---

## Autonomous Loops

These are the two autonomous iteration engines. Use them for batch work, iterative refinement, and overnight runs.

### Ralph Wiggum Loop

| Property | Detail |
|----------|--------|
| **Source** | `ralph-loop@claude-plugins-official` |
| **Purpose** | Autonomous multi-task batch work — task list driven |
| **Best for** | Generating multiple deliverables, repetitive analysis, batch document creation |
| **Commands** | `/ralph-loop`, `/cancel-ralph`, `/help` |

| Command | Usage | Example |
|---------|-------|---------|
| `/ralph-loop` | Start autonomous batch work | `/ralph-loop "Generate PRD for each increment. Output <promise>ALL DONE</promise> when finished." --max-iterations 20 --completion-promise "ALL DONE"` |
| `/cancel-ralph` | Cancel active loop | `/cancel-ralph` |

**Key flags:**
- `--max-iterations N` — Safety cap on iterations
- `--completion-promise "TEXT"` — Clean exit trigger

**When to use Ralph vs Autoresearch:**
| Scenario | Use |
|----------|-----|
| Generate 5 catalog docs in batch | Ralph (task-list driven) |
| Iterate on a single spec until quality score hits target | Autoresearch (metric-driven) |
| Run repetitive file generation | Ralph |
| Stress-test pricing across scenarios | Autoresearch:scenario |
| Overnight improvement loop with measurable KPI | Autoresearch |

---

### Claude Autoresearch (Customized for FinBlocks)

| Property | Detail |
|----------|--------|
| **Source** | `rmahabal/claude-autoresearch` (forked + customized) |
| **Purpose** | Autonomous goal-directed iteration — metric driven |
| **Best for** | Iterative refinement toward measurable targets, multi-persona analysis, scenario exploration |
| **Commands** | 9 total (1 root + 8 subcommands) |

| Command | Purpose | PM Use Case |
|---------|---------|-------------|
| `/autoresearch` | Core autonomous loop: modify → verify → keep/discard → repeat | Iterate on spec quality until rubric score hits target |
| `/autoresearch:plan` | Interactive wizard to build Goal → Scope → Metric → Verify | Set up any iteration run interactively |
| `/autoresearch:predict` | Multi-persona swarm analysis (3-8 perspectives) | **Use `--pm` flag** for FinBlocks personas (Dana, Alex, Sam, Buyer, Devil's Advocate) |
| `/autoresearch:scenario` | Edge case explorer across 12+ dimensions | **Use `--domain finserv`** for financial services dimensions (regulatory, multi-party, credit decisioning) |
| `/autoresearch:ship` | Universal 8-phase shipping workflow | Ship `product-spec`, `catalog-doc`, `prototype`, `strategy-doc` with PM-specific checklists |
| `/autoresearch:learn` | Autonomous documentation engine | Learn and document product knowledge base |
| `/autoresearch:debug` | Scientific bug-hunting (7 techniques) | Lower priority — code-focused |
| `/autoresearch:fix` | Autonomous error crusher | Lower priority — code-focused |
| `/autoresearch:security` | STRIDE/OWASP security audit | Lower priority — code-focused |

#### FinBlocks Customizations (what was changed)

| File Modified | What Was Added |
|--------------|----------------|
| `predict-workflow.md` | **PM Persona Set** (`--pm` flag): Dana (Analyst), Alex (RM), Sam (Credit Officer), Enterprise Buyer (B1/B2), Devil's Advocate — replaces code personas for product analysis |
| `scenario-workflow.md` | **Financial Services Domain** (`--domain finserv`): 5 new exploration dimensions (regulatory, multi-party, document lifecycle, credit decisioning, portfolio cascade) + FinServ-specific extra checks |
| `ship-workflow.md` | **PM Deliverable Types**: `product-spec`, `catalog-doc`, `prototype`, `strategy-doc` with inventory checks + full checklists (persona validation, SKU matching, prototype rendering) |
| `SKILL.md` | **PM Domain Adaptation Table**: metrics, scopes, verify commands, and guards for product specs, pricing, catalogs, competitors, prototypes, persona journeys |

#### Autoresearch Quick-Start Examples for FinBlocks

```bash
# Swarm analysis of origination spec using PM personas
/autoresearch:predict --pm
Scope: G:/My Drive/FinBlocks/03-product/origination/*.md
Goal: Identify gaps in spec completeness and persona coverage

# Explore edge cases in loan origination workflow
/autoresearch:scenario --domain finserv
Scenario: Commercial loan application flows from intake to closing with multiple guarantors
Depth: deep
Iterations: 30

# Ship a product spec with PM checklist
/autoresearch:ship --type product-spec
Target: G:/My Drive/FinBlocks/03-product/origination/1a-intake-portal.md

# Iterate on pricing model until competitive gap closes
/autoresearch
Goal: Reduce competitive pricing gap below 15% for mid-market segment
Scope: G:/My Drive/FinBlocks/02-strategy/*.md
Iterations: 10

# Multi-persona pre-mortem on GTM strategy
/autoresearch:predict --pm --depth deep
Goal: Pre-mortem on FinBlocks go-to-market plan
```

---

## PM Skills — Core (68 skills)

**Source:** `rmahabal/pm-skills` (8 plugin packs, v1.0.1)

### Product Discovery (13 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| Analyze Feature Requests | `/analyze-feature-requests` | Prioritize customer requests by impact/effort |
| Brainstorm Experiments (Existing) | `/brainstorm-experiments-existing` | Design A/B tests and validation experiments |
| Brainstorm Experiments (New) | `/brainstorm-experiments-new` | Lean startup pretotypes and XYZ hypotheses |
| Brainstorm Ideas (Existing) | `/brainstorm-ideas-existing` | Multi-perspective ideation (PM/Designer/Engineer) |
| Brainstorm Ideas (New) | `/brainstorm-ideas-new` | Feature ideas for new product in discovery |
| Identify Assumptions (Existing) | `/identify-assumptions-existing` | VUVF risk assessment for feature ideas |
| Identify Assumptions (New) | `/identify-assumptions-new` | 8-category risk assessment for new products |
| Interview Script | `/interview-script` | Mom Test customer interview scripts |
| Metrics Dashboard | `/metrics-dashboard` | North Star + input + health metrics design |
| Opportunity Solution Tree | `/opportunity-solution-tree` | Connect outcomes → opportunities → solutions |
| Prioritize Assumptions | `/prioritize-assumptions` | Impact x Risk matrix for testing decisions |
| Prioritize Features | `/prioritize-features` | Rank features by impact/effort/risk/strategy |
| Summarize Interview | `/summarize-interview` | Structure interview transcript into JTBD template |

### Product Strategy (13 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| Ansoff Matrix | `/ansoff-matrix` | 4 growth strategy evaluation |
| Business Model Canvas | `/business-model` | 9-block business model |
| Lean Canvas | `/lean-canvas` | 9-block rapid hypothesis testing |
| Monetization Strategy | `/monetization-strategy` | 3-5 revenue model brainstorm |
| PESTLE Analysis | `/pestle-analysis` | Macro-environment assessment |
| Porter's Five Forces | `/porters-five-forces` | Industry competitiveness analysis |
| Pricing Strategy | `/pricing-strategy` | Pricing models + WTP + elasticity |
| Product Name | `/product-name` | 5 name ideas with rationale |
| Product Strategy Canvas | `/product-strategy` | 9-section strategic plan |
| Product Vision | `/product-vision` | Inspiring vision statement |
| Startup Canvas | `/startup-canvas` | Strategy + business model for new product |
| SWOT Analysis | `/swot-analysis` | Strengths/weaknesses/opportunities/threats |
| Value Proposition | `/value-proposition` | 6-part JTBD value prop |

### Execution (18 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| Brainstorm OKRs | `/brainstorm-okrs` | Team OKRs aligned with company objectives |
| Create PRD | `/create-prd` | 8-section Product Requirements Document |
| Dummy Dataset | `/dummy-dataset` | Realistic test data (CSV/JSON/SQL) |
| Job Stories | `/job-stories` | JTBD format: When/I want/So I can |
| Outcome Roadmap | `/outcome-roadmap` | Feature → outcome roadmap transformation |
| Prioritization Frameworks | `/prioritization-frameworks` | Reference guide to 9 frameworks (RICE, ICE, etc.) |
| Release Notes | `/release-notes` | User-friendly changelog from tech docs |
| Retro | `/retro` | Start/Stop/Continue or 4Ls retrospective |
| Sprint Plan | `/sprint-plan` | Capacity + story selection + dependencies |
| Summarize Meeting | `/summarize-meeting` | Structured notes from transcript |
| Test Scenarios | `/test-scenarios` | QA test plans from user stories |
| User Stories | `/user-stories` | 3 C's framework with INVEST criteria |
| WWAs | `/wwas` | Why-What-Acceptance backlog items |

### Market Research (7 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| Competitor Analysis | `/competitor-analysis` | 5 competitors with positioning + gaps |
| Customer Journey Map | `/customer-journey-map` | End-to-end journey with touchpoints |
| Market Segments | `/market-segments` | 3-5 segments with demographics + JTBD |
| Market Sizing | `/market-sizing` | TAM/SAM/SOM estimation |
| Sentiment Analysis | `/sentiment-analysis` | User feedback analysis with scores |
| User Personas | `/user-personas` | 3 personas from research data |
| User Segmentation | `/user-segmentation` | 3+ segments from behavior patterns |

### Data Analytics (3 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| A/B Test Analysis | `/ab-test-analysis` | Statistical significance + ship recommendation |
| Cohort Analysis | `/cohort-analysis` | Retention curves + feature adoption |
| SQL Queries | `/sql-queries` | Natural language → SQL (BigQuery/PG/MySQL) |

### Go-to-Market (6 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| Beachhead Segment | `/beachhead-segment` | Initial market selection (4 criteria) |
| Competitive Battlecard | `/competitive-battlecard` | Sales-ready feature comparison + objection handling |
| Growth Loops | `/growth-loops` | 5 flywheel types for sustainable traction |
| GTM Motions | `/gtm-motions` | 7 motion types with tool recommendations |
| GTM Strategy | `/gtm-strategy` | Full go-to-market plan |
| Ideal Customer Profile | `/ideal-customer-profile` | ICP from research data |

### Marketing & Growth (5 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| Marketing Ideas | `/marketing-ideas` | 5 creative campaign ideas |
| North Star Metric | `/north-star-metric` | NSM + 3-5 input metrics |
| Positioning Ideas | `/positioning-ideas` | 5 positioning concepts |
| Product Name | `/product-name` | Name brainstorm |
| Value Prop Statements | `/value-prop-statements` | Segment-targeted messaging |

### Toolkit (4 skills)

| Skill | Command | Purpose |
|-------|---------|---------|
| Draft NDA | `/draft-nda` | Non-Disclosure Agreement template |
| Grammar Check | `/grammar-check` | Grammar/logic/flow error detection |
| Privacy Policy | `/privacy-policy` | Privacy policy with GDPR considerations |
| Review Resume | `/review-resume` | Resume feedback and suggestions |

---

## PM Skills — Advanced (43 skills)

**Source:** `rmahabal/product-manager-skills` (pm-skills-advanced, v0.4.0)

| Category | Skills |
|----------|--------|
| **Discovery & Research** | discovery-process, discovery-interview-prep, interview-script, jobs-to-be-done, customer-journey-map, customer-journey-mapping-workshop, proto-persona, problem-framing-canvas, problem-statement |
| **Strategy & Planning** | product-strategy-session, roadmap-planning, opportunity-solution-tree, lean-ux-canvas, positioning-statement, positioning-workshop, product-name (duplicate) |
| **Financial Analysis** | business-health-diagnostic, finance-metrics-quickref, finance-based-pricing-advisor, feature-investment-advisor, acquisition-channel-advisor, saas-economics-efficiency-metrics, saas-revenue-growth-metrics, tam-sam-som-calculator |
| **Execution** | prd-development, epic-breakdown-advisor, epic-hypothesis, user-story, user-story-mapping, user-story-mapping-workshop, user-story-splitting, prioritization-advisor, sprint-plan (not listed but similar) |
| **Communication** | press-release, eol-message, storyboard, recommendation-canvas, company-research |
| **AI & Context** | ai-shaped-readiness-advisor, context-engineering-advisor |
| **Analysis Frameworks** | pestel-analysis, pol-probe, pol-probe-advisor, swot-analysis (similar) |
| **Workshops & Facilitation** | workshop-facilitation, skill-authoring-workflow |

---

## Visual & Document Generation

**Source:** `visual-explainer@visual-explainer`

| Command | Purpose |
|---------|---------|
| `/generate-slides` | Generate presentation slides |
| `/generate-visual-plan` | Create visual project plans |
| `/generate-web-diagram` | Create web/interactive diagrams |
| `/diff-review` | Review code diffs visually |
| `/fact-check` | Fact-check content with visual evidence |
| `/plan-review` | Review plans visually |
| `/project-recap` | Generate project recap with visuals |
| `/share` | Share visual outputs |

---

## MCP Integrations

| Server | Tools Available | Usage |
|--------|----------------|-------|
| **GitHub** | Issues, PRs, code review, search, repo management | `gh` CLI or MCP tools |
| **Slack** | Send/search messages, read channels/threads, create canvases, user profiles | `mcp__*__slack_*` tools |
| **Linear** | Issue tracking, project management | Linear MCP tools |
| **Google Calendar** | Events, scheduling, free time, meeting finder | `mcp__*__gcal_*` tools |
| **Gmail** | Search, read, draft emails | `mcp__*__gmail_*` tools |
| **Claude in Chrome** | Browser automation, page reading, navigation | `mcp__Claude_in_Chrome__*` tools |
| **Claude Preview** | Dev server management, screenshots, inspection | `mcp__Claude_Preview__*` tools |

---

## Custom FinBlocks Commands

**Path:** `C:\Ravikiran\.claude\commands\`

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/session-start` | Load tracker + session log, orient | Start of every session |
| `/session-end` | Update tracker, session log, give summary | End of every session (MANDATORY) |
| `/finblocks-status` | Read PROJECT-TRACKER.md, summarize statuses | Quick status check |
| `/discovery-context` | Load P1+P2 discovery research files | Working on discovery/research |
| `/diligence-context` | Load diligence module reference files | Working on Due Diligence module |
| `/origination-context` | Load origination sub-block references | Working on Loan Origination |
| `/platform-context` | Load platform/shared-component files | Working on architecture/entity master |
| `/batch-catalog` | Start Ralph loop for catalog DOCX generation | Batch producing catalog documents |

---

## Installed Plugin Summary

| Plugin | Version | Type | Status |
|--------|---------|------|--------|
| pm-product-discovery@pm-skills | 1.0.1 | Marketplace | Active |
| pm-product-strategy@pm-skills | 1.0.1 | Marketplace | Active |
| pm-execution@pm-skills | 1.0.1 | Marketplace | Active |
| pm-market-research@pm-skills | 1.0.1 | Marketplace | Active |
| pm-data-analytics@pm-skills | 1.0.1 | Marketplace | Active |
| pm-go-to-market@pm-skills | 1.0.1 | Marketplace | Active |
| pm-marketing-growth@pm-skills | 1.0.1 | Marketplace | Active |
| pm-toolkit@pm-skills | 1.0.1 | Marketplace | Active |
| pm-skills-advanced@product-manager-skills | 0.4.0 | Marketplace | Active |
| github@claude-plugins-official | - | Official | Active |
| slack@claude-plugins-official | - | Official | Active |
| linear@claude-plugins-official | - | Official | Active |
| ralph-loop@claude-plugins-official | - | Official | Active |
| visual-explainer@visual-explainer | - | Marketplace | Active |
| autoresearch (forked) | 1.8.2 | Manual/Fork | Customized |

---

## Decision Matrix: Which Tool When?

| Task | Best Tool | Why |
|------|-----------|-----|
| **Generate 5 catalog docs** | `/ralph-loop` | Task-list batch work |
| **Iterate spec quality to target** | `/autoresearch` | Metric-driven improvement loop |
| **Review spec from multiple perspectives** | `/autoresearch:predict --pm` | PM persona swarm analysis |
| **Explore loan origination edge cases** | `/autoresearch:scenario --domain finserv` | FinServ-specific dimensions |
| **Ship a completed PRD** | `/autoresearch:ship --type product-spec` | PM-specific checklist |
| **Quick competitor analysis** | `/competitor-analysis` | Structured PM skill |
| **Pricing model evaluation** | `/pricing-strategy` or `/finance-based-pricing-advisor` | PM skill (basic vs advanced) |
| **Create presentation slides** | `/generate-slides` | Visual explainer |
| **Check project status** | `/finblocks-status` | Custom command |
| **Start a work session** | `/session-start` | Custom command (mandatory) |
| **Brainstorm features** | `/brainstorm-ideas-existing` | PM discovery skill |
| **Write user stories** | `/user-stories` or `/user-story` | PM skill (basic vs advanced) |
| **Market sizing** | `/market-sizing` or `/tam-sam-som-calculator` | PM skill (basic vs advanced) |
| **Interview preparation** | `/interview-script` or `/discovery-interview-prep` | PM skill (basic vs advanced) |
| **Build OKRs** | `/brainstorm-okrs` | PM execution skill |
| **Document codebase** | `/autoresearch:learn` | Autonomous doc engine |

# Workflow Overview: Vibe Coding

## Introduction

This workflow transforms non-coders into effective application builders through systematic collaboration with AI. You bring domain knowledge and product vision; AI handles implementation. The workflow provides structure, quality gates, and traceability from idea to production.

**Core Innovation:** Systematic progression through PRD → Production-Aware Roadmap → Incremental Versions → Production Validation, with AI doing the coding while you make product decisions.

---

## The Complete Process Flow

```
┌─────────────────────────────────────────────────────────┐
│ Phase 0: Project Initialization                         │
│ Create project structure, initialize git                │
└────────────────┬────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────────────────┐
│ Phase 1: Product Definition                             │
│ • Create PRD (with ChatGPT)                             │
│ • Create Production-Aware Roadmap (with ChatGPT)        │
│   - Review production standards                         │
│   - Build roadmap with standards integrated             │
└────────────────┬────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────────────────┐
│ Phase 2: Version Execution (Repeat for v0.1 → v1.0)    │
│ • Create Mission Order (with ChatGPT)                   │
│ • Pass to Claude Code                                   │
│ • Claude creates Zen Plan → ChatGPT validates          │
│ • Implementation (hive-mind agents)                     │
│ • Automated UAT                                         │
│ • User UAT (if GUI)                                     │
│ • Status Report                                         │
│ • Update Lessons Learned                                │
│ • Mark version complete                                 │
└────────────────┬────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────────────────────┐
│ Phase 3: Production Deployment                          │
│ • Validate production readiness (all standards met)     │
│ • Deploy v1.0                                           │
│ • Monitor and iterate                                   │
└─────────────────────────────────────────────────────────┘
```

---

## Phase 0: Project Initialization

### Purpose
Set up project structure and tooling before defining product.

### Actions

**1. Create project directory:**
```bash
mkdir my-project
cd my-project
```

**2. Create standard folder structure:**
```bash
mkdir -p docs/versions docs/archive src tests config
```

**3. Initialize git:**
```bash
git init
git checkout -b main
```

**4. Initialize with Claude Code (optional):**
```bash
npx claude-flow@alpha hive-mind spawn \
  "Initialize project structure and setup" \
  --project ./my-project \
  --auto-spawn \
  --verbose \
  --claude \
  --monitor
```

This creates `.claude/` directory with agent configuration.

### Deliverables
- Empty project structure
- Git repository initialized
- Ready for product definition

**Time Investment:** 15-30 minutes

---

## Phase 1: Product Definition

### Purpose
Define what you're building and break it into achievable versions with production standards baked in from the start.

### Step 1.1: Create PRD

**Tool:** `prd-template.md` + ChatGPT

**Process:**
1. Open `prd-template.md`
2. Upload to ChatGPT
3. Prompt: "I'm building [description]. Help me create a PRD using this template. Ask me questions section-by-section."
4. Work through 8 required sections (+ optional sections if needed)
5. Save as `docs/prd.md`

**Deliverable:** Complete Product Requirements Document

**Time Investment:** 2-4 hours

---

### Step 1.2: Create Production-Aware Roadmap

**Tools:** 
- `roadmap-template.md`
- `production-readiness-checklist.md`
- ChatGPT

**Process:**
1. Upload ALL THREE documents to ChatGPT:
   - Your completed `docs/prd.md`
   - `roadmap-template.md`
   - `production-readiness-checklist.md`

2. Prompt: "Based on this PRD, help me create a production-aware roadmap. First, review the production checklist with me to identify which standards need early architectural decisions. Then create a roadmap that breaks the PRD into logical versions, ensuring production requirements are addressed incrementally, not bolted on at the end."

3. ChatGPT walks you through TWO integrated parts:
   
   **Part A: Production Standards Review (30-45 minutes)**
   - Which checklist items apply to your project?
   - Which need early architectural decisions?
   - Which require incremental building vs end-stage addition?
   - Domain-specific priorities (e.g., fintech needs auth early)
   
   **Part B: Roadmap Creation (1-2 hours)**
   - Break PRD into logical versions (typically 6-10)
   - Account for production standards in version planning
   - Ensure security, performance, observability built incrementally
   - Validate dependencies and complexity distribution

4. Review and approve final roadmap
5. Save as `docs/roadmap.md`

**What ChatGPT Does:**
- Explains technical checklist items in plain language
- Maps PRD requirements to production standards
- Identifies which versions should address which standards
- Creates roadmap with production awareness built-in
- Prevents "surprise requirements" at v0.9

**What You Learn:**
- Production standards relevant to your domain
- Which architectural decisions to make early
- What to build incrementally vs add later
- Risk areas requiring special attention

**Example Insights:**
- "Authentication should be in v0.2, not v0.9 - fintech requires this early"
- "Performance budgets inform v0.3 database design - can't retrofit later"
- "Structured logging needed from v0.1 for debugging distributed systems"
- "GDPR compliance affects data model from v0.1 - must architect for it now"

**Deliverable:** Production-aware roadmap (v0.1 through v1.0) with standards integrated into version planning

**Time Investment:** 3-4 hours (combined step, single pass, no rework)

---

## Phase 2: Version Execution

### Overview
Repeat this phase for each version (v0.1, v0.2, ... v1.0). Each iteration delivers working, tested software.

---

### Step 2.1: Create Mission Order

**Tool:** `mission-order-standard.md` + ChatGPT

**Process:**
1. Upload `docs/roadmap.md` and `mission-order-standard.md` to ChatGPT
2. Prompt: "Create a Mission Order for version [X.X] following the standard. Use the roadmap entry for this version as the basis."
3. Review generated Mission Order:
   - Scope correct?
   - DoD items testable?
   - Dependencies clear?
   - Environment config addressed?
4. Save as `docs/versions/vX.X/mission-order.md`

**Approval Gate:** You must approve Mission Order before passing to Claude Code

**Git Action:** Commit Mission Order
```bash
git add docs/versions/vX.X/mission-order.md
git commit -m "[vX.X] docs: Add mission order"
```

**Time Investment:** 1-2 hours per version

---

### Step 2.2: Pass to Claude Code

**Process:**
1. Ensure Claude Code has access to project directory
2. Provide Mission Order to Claude Code
3. Claude Code spawns hive-mind agents
4. Agents coordinate via hooks

**What Happens:**
- Claude creates Zen Plan (auto-saved to `docs/versions/vX.X/zen-plan.md`)
- Zen Plan passed to ChatGPT for validation
- ChatGPT approves or requests changes
- If approved, implementation begins

**Your Role:** Monitor progress, answer questions if agents get stuck

---

### Step 2.3: Implementation (Automated)

**Who:** Claude Code + hive-mind agents

**What They Do:**
- Implement features per Execution Tasks
- Write unit and integration tests
- Create documentation
- Follow efficiency patterns (batching, concurrency)
- Commit code per git directives

**Your Role:** Minimal - let agents work. Check in occasionally.

**Time Investment:** Minutes of your time; hours of agent work

---

### Step 2.4: Code Validation (Automated)

**Who:** ChatGPT via Zen MCP

**What It Checks:**
- Router registration (routes actually exist)
- Component imports (files actually imported)
- Event handlers (buttons actually wired)
- Environment configuration (no hardcoded secrets)
- Common integration mistakes

**If GUI in scope, automated UAT checks:**
- All routes return 200
- Components render in DOM
- Button handlers registered
- No console errors on page load

**Deliverable:** `docs/versions/vX.X/uat-automated.md` with inline results

---

### Step 2.5: User UAT (Manual)

**When:** Only if GUI in scope

**Tool:** `docs/versions/vX.X/uat-user.md` (created by agents)

**Your Actions:**
1. Open application
2. Follow UAT scenarios
3. Validate visuals, user flows, error messages
4. Note issues inline in UAT document
5. Troubleshoot with Claude until resolved
6. Add approval notes when satisfied

**Git Action:** Commit UAT with approval
```bash
git add docs/versions/vX.X/uat-*.md
git commit -m "[vX.X] test: Complete UAT with approval"
```

**Time Investment:** 1-3 hours depending on version complexity

---

### Step 2.6: Status Report & Completion

**Who:** Claude generates, you review

**What It Contains:**
- DoD completion status
- What was delivered vs planned
- Known issues and limitations
- Deployment readiness
- File inventory and metrics

**Your Actions:**
1. Review Status Report for accuracy
2. Request corrections if needed
3. Approve when satisfied

**Update Lessons Learned:**
- What worked
- What could improve
- Recommendations for next version

**Git Actions:** Mark version complete
```bash
git add docs/versions/vX.X/status-report.md docs/lessons-learned.md
git commit -m "[vX.X] docs: Mark vX.X complete with status report and lessons"

# Merge feature branch to main
git checkout main
git merge --no-ff feature/vX.X/brief-name
git tag -a vX.X -m "Release vX.X: [description]"
git push origin main --tags
```

**Time Investment:** 30 minutes - 1 hour

---

## Phase 3: Production Deployment

### Purpose
Validate that all production standards were met incrementally and deploy v1.0.

### Step 3.1: Validate Production Readiness

**Tool:** `production-readiness-checklist.md`

**Purpose:** This is a **validation gate**, not a discovery phase. All items should already be built incrementally across versions. You're confirming everything is complete, not finding surprise requirements.

**Process:**
1. Go through all 114 checks across 7 categories
2. Mark each as pass/fail
3. Calculate category scores
4. Identify any gaps (should be minimal if roadmap was followed)

**Categories:**
- Security (20 checks) - Must pass 100% of critical items
- Performance (16 checks) - Must pass 75%
- Reliability (16 checks) - Must pass 88%
- Observability (16 checks) - Must pass 63%
- Documentation (15 checks) - Must pass 80%
- Operations (16 checks) - Must pass 81%
- Legal/Compliance (15 checks) - Must pass 100% of applicable

**Expected Outcome:**
Because production standards were reviewed in Phase 1 and built incrementally across versions, most items should already pass. Any failures indicate either:
- Implementation gaps (need to fix before v1.0)
- Roadmap oversights (lessons for next project)

**Decision:**
- Ready: All minimums met, no blockers
- Conditional: Minor gaps with workarounds
- Blocked: Critical issues must be resolved

**Time Investment:** 2-4 hours for validation (not extensive rework)

---

### Step 3.2: Deploy

**Process:**
1. Follow deployment procedure from technical handbook
2. Verify health checks
3. Monitor for issues
4. Execute rollback plan if needed

**Post-Deployment:**
- Within 24 hours: Validate metrics, check errors
- Within 1 week: Collect feedback, verify stability

---

## Tool Roles

### You (The Developer)
**Responsibilities:**
- Define product vision (PRD)
- Make architectural decisions (roadmap)
- Approve mission orders
- Execute user UAT
- Make go/no-go decisions
- Provide domain expertise

**Time per version:** 4-8 hours over 1-2 weeks

---

### ChatGPT
**Responsibilities:**
- Help create PRD (guided questions)
- Guide production standards review
- Generate production-aware roadmap from PRD
- Create mission orders from roadmap
- Validate Zen Plans before implementation
- Validate completed code before UAT
- Review status reports

**Strengths:** Strategic thinking, external validation, catches design flaws, explains technical concepts

---

### Claude Code
**Responsibilities:**
- Receive mission orders
- Create Zen Plans
- Spawn hive-mind agents
- Coordinate implementation
- Run automated UAT
- Generate status reports

**Strengths:** Parallel execution, agent coordination, implementation

---

## Approval Gates

| Phase | Gate | Decision Maker | Criteria |
|-------|------|----------------|----------|
| PRD Complete | Approve PRD | You | Vision clear, success measurable |
| Roadmap Complete | Approve Roadmap | You | Versions logical, production-aware |
| Mission Order Created | Pass to Claude | You | Scope correct, DoD testable |
| Zen Plan Validated | Approve Plan | ChatGPT | Approach sound, risks identified |
| Code Complete | Automated UAT Pass | Claude Code | All DoD items pass |
| GUI Validated | User UAT Pass | You | Experience acceptable |
| Version Complete | Mark Complete | You | Status Report accurate |
| Production Ready | Deploy | You | Standards validated, no blockers |

---

## Key Principles

### 1. Incremental Value
Every version delivers working software. v0.3 is useful even if v0.4 never happens.

### 2. Quality Gates
Nothing proceeds without approval. Catching issues early prevents expensive rework.

### 3. Traceability
Every line of code traces back to a DoD item, which traces to a roadmap entry, which traces to the PRD.

### 4. Learning Loops
Lessons learned from each version inform future versions. The workflow improves as you use it.

### 5. AI Does Implementation, You Make Decisions
You're not writing code - you're making product decisions. AI handles the technical execution.

### 6. Production Standards Built-In
Production requirements integrated from day 1, not retrofitted at v0.9. Architecture decisions informed by deployment needs.

---

## Document Usage Guide

**When starting a project:**
1. `prd-template.md` - Create PRD
2. `roadmap-template.md` + `production-readiness-checklist.md` - Create production-aware roadmap

**Each version:**
1. `mission-order-standard.md` - Create mission order
2. `technical-handbook.md` - Agents reference (you don't)

**Before v1.0:**
1. `production-readiness-checklist.md` - Validate all standards met

**Ongoing:**
1. `lessons-learned-template.md` - Update after each version
2. `status-report-template.md` - Agents use for status reports

---

## Success Patterns

**What makes this workflow effective:**
- Clear separation: you decide, AI implements
- Multiple validation layers prevent issues
- Incremental delivery reduces risk
- Learning captured and applied
- Full traceability from vision to code
- Production standards baked in from start

**Common pitfalls to avoid:**
- Skipping approval gates
- Vague DoD items
- Ignoring lessons learned
- Unclear scope definition
- Weak automated UAT
- Treating production checklist as end-stage surprise

---

## Time Investment Summary

**Per Project (one-time):**
- PRD creation: 2-4 hours
- Production-aware roadmap creation: 3-4 hours
- **Total: 5-8 hours**

**Per Version (repeated 6-10 times):**
- Mission order: 1-2 hours
- UAT execution: 1-3 hours
- Review and approval: 1 hour
- **Total per version: 3-6 hours**

**Before Production:**
- Production validation: 2-4 hours

**Grand total for complete MVP (v0.1 → v1.0):**
- **32-64 hours of your time** over 2-6 months
- Agents handle 100+ hours of implementation work

---

## Next Steps

1. Read `README.md` if you haven't already
2. Start with `prd-template.md` for your first project
3. Reference `technical-handbook.md` only if you need technical details
4. Follow this workflow overview for the complete process

The workflow is designed to minimize your cognitive load while maximizing output quality. Let AI handle complexity while you focus on product vision.

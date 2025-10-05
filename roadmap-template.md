# Roadmap Template

## Overview
This template helps you break down a Product Requirements Document (PRD) into logical, buildable versions with production standards integrated from the start. Each version should deliver incremental value while stacking toward the complete MVP.

**Note:** This template is used together with `production-readiness-checklist.md` to create a production-aware roadmap where security, performance, observability, and other production requirements are built incrementally, not retrofitted at the end.

---

## Roadmap Structure

### Version Naming
Use semantic versioning for clarity:
- `v0.X` - Foundation building (pre-MVP iterations)
- `v1.0` - Complete MVP
- `v1.X` - Post-MVP enhancements

### Version Entry Format

Each version should follow this structure:

```markdown
## vX.X – [Brief Name]

**Metadata:**
- **Dependencies:** [List of prior versions that must be complete]
- **Scope:** [Backend, Frontend, CLI, Infrastructure, Documentation]
- **Complexity:** [Low | Medium | High]
- **Risk Level:** [Low | Medium | High]
- **PRD Alignment:** [Reference to PRD section(s)]
- **Production Standards:** [Which production requirements addressed in this version]

**Objective:** [One sentence describing what this version achieves]

**Key Features:**
- Feature 1: [Brief description]
- Feature 2: [Brief description]
- Feature 3: [Brief description]

**Definition of Done:**
[How you know this version is complete - testable outcomes]
```

---

## Example Version Entry

```markdown
## v0.3 – Historical Data Ingestion

**Metadata:**
- **Dependencies:** v0.2 (broker interface must exist)
- **Scope:** Backend, Documentation
- **Complexity:** Medium
- **Risk Level:** Low
- **PRD Alignment:** Section 4.2 (Data Management)
- **Production Standards:** Structured logging (observability), data validation (reliability)

**Objective:** Provide reliable historical datasets for testing and backtesting.

**Key Features:**
- Historical OHLCV ingestion pipeline (multi-ticker)
- Corporate actions handling (splits/dividends)
- Trading calendar and timezone support
- Symbol master with ticker mapping

**Definition of Done:**
Historical data can be ingested, stored, and queried consistently with adjustments applied.
```

---

## Metadata Field Definitions

**Dependencies:**
- List version numbers that must be complete before this version starts
- Example: "v0.2, v0.3" or "None" for first version

**Scope:**
- Backend / API: Server-side logic, databases, APIs
- Frontend / GUI: User interface, web pages, forms
- CLI / Tooling: Command-line interfaces, scripts
- Infrastructure / Deployment: Docker, configs, deployment
- Documentation / Playbooks: User guides, setup docs

**Complexity:**
- **Low:** Straightforward implementation, well-understood patterns
- **Medium:** Some unknowns, requires research or new patterns
- **High:** Multiple unknowns, complex integrations, risky implementation

**Risk Level:**
- **Low:** Failure won't block other work, easy to rollback
- **Medium:** Some dependencies, moderate rework if it fails
- **High:** Critical path, many dependencies, hard to rollback

**PRD Alignment:**
- Reference the PRD section this version supports
- Example: "Section 4.3 (Safety Requirements)" or "Sections 2, 4.1"

**Production Standards:**
- List which production requirements from the checklist are addressed in this version
- Examples: "Authentication (security)", "API response time budgets (performance)", "Structured logging (observability)"
- Early versions should address foundational requirements (auth, logging, config management)
- Later versions build on these foundations

---

## Version Planning Guidelines

### How Many Versions?

**Typical MVP breakdown: 6-10 versions**

- Too few (<5): Each version too complex, risky
- Too many (>12): Overhead of planning/UAT outweighs value
- Sweet spot: 6-10 versions building incrementally

### Version Sizing

Each version should be:
- **Completable in 1-3 weeks** for solo developer
- **Independently testable** with its own UAT
- **Incrementally valuable** - delivers something usable

### Dependency Management

**Good dependency chains:**
```
v0.1 → v0.2 → v0.3 → v0.4
         ↓
        v0.5 → v0.6
```

v0.2 enables both v0.3 and v0.5, which can run in parallel.

**Bad dependency chains:**
```
v0.1 → v0.2 → v0.3 → v0.4 → v0.5 → v0.6 → v0.7 → v0.8
```

Every version depends on the previous = no flexibility, high risk.

### Risk Distribution

Don't stack all high-risk versions at the end:
- ✅ Spread high-risk versions: v0.2 (high), v0.4 (medium), v0.6 (high)
- ❌ Cluster risk: v0.1-0.4 (low), v0.5-0.8 (all high)

Tackle risky unknowns early so you can adjust the roadmap if needed.

---

## Using This Template with ChatGPT

### Generate Production-Aware Roadmap from PRD

**IMPORTANT:** Upload THREE documents together:
1. Your completed PRD
2. This roadmap template
3. `production-readiness-checklist.md`

Then use this prompt:

```
Based on this PRD, help me create a production-aware roadmap. 

First, review the production-readiness-checklist with me:
- Which checklist items apply to my project?
- Which need early architectural decisions?
- Which should be built incrementally vs added at the end?

Then create a roadmap that:
- Breaks the product into 6-10 logical versions
- Builds incrementally toward the MVP
- Integrates production standards from the start
- Has clear dependencies
- Distributes complexity and risk across versions
- Uses the metadata format from the roadmap template
```

### Example ChatGPT Interaction

**ChatGPT:** "Let's start by reviewing production standards for your financial trading app. Looking at the security category, authentication is critical for fintech. I recommend adding this in v0.2, not waiting until v0.9. For observability, structured logging should start in v0.1 so you can debug from day one..."

[After standards review]

**ChatGPT:** "Now let's create your roadmap. Based on your PRD and the production standards we discussed:

v0.1 - Core Infrastructure
- Production Standards: Structured logging, config management, basic security
- Rationale: Foundation for debugging and secure development

v0.2 - Authentication & Authorization  
- Production Standards: User auth, API security, session management
- Rationale: Must be architected from start, can't retrofit

v0.3 - Data Management
- Production Standards: Data validation, backup procedures
- Rationale: Data integrity critical for finance...

[continues through v1.0]"

### Validate Dependency Chain

Once you have a draft roadmap:

```
Review this roadmap's dependency chain. Are there any:
- Circular dependencies?
- Unnecessary sequential dependencies that could be parallel?
- Missing dependencies that would cause issues?
```

### Assess Risk Distribution

```
Analyze the risk distribution across these versions. 
Are high-risk items appropriately spaced? 
Should any high-risk versions be moved earlier?
```

### Refine Version Scope

If a version seems too large:

```
Version [X.X] seems too complex. Help me split it into two versions 
while maintaining clear deliverables for each.
```

---

## Roadmap Evolution

Roadmaps change as you learn:

**After each version:**
- Update remaining versions based on what you learned
- Adjust complexity/risk assessments
- Add new versions if needed
- Remove versions if scope changes

**Mark changes clearly:**
```markdown
## v0.5 – Live Data Integration

**Status:** ⚠️ SCOPE CHANGED (was v0.4, moved due to v0.3 learnings)

**Metadata:**
...
```

**Keep a changelog:**
```markdown
## Roadmap Changelog
- 2024-XX-XX: Split v0.6 into v0.6 and v0.7 (complexity too high)
- 2024-XX-XX: Moved v0.5 earlier (v0.3 revealed need for live data sooner)
- 2024-XX-XX: Initial roadmap created
```

---

## Common Roadmap Patterns

### Foundation → Features → Integration

**v0.1-0.2:** Core infrastructure and data models
**v0.3-0.5:** Key features built on foundation  
**v0.6-0.8:** Integration, polish, edge cases
**v1.0:** Complete MVP

### Vertical Slices

Each version delivers a complete user workflow end-to-end:

**v0.1:** User can create and save basic item
**v0.2:** User can edit and delete item
**v0.3:** User can search and filter items
**v0.4:** User can export items

### Production-Aware Risk-First

Tackle both technical unknowns AND production requirements early:

**v0.1:** Core infrastructure + logging + config management
**v0.2:** Authentication/authorization (can't retrofit)
**v0.3:** Riskiest business logic integration  
**v0.4-0.7:** Features with observability/monitoring built-in
**v0.8-0.9:** Performance optimization, edge cases
**v1.0:** Final production validation

---

## Anti-Patterns to Avoid

**❌ Production as Afterthought:**
Build all features first, add auth/logging/monitoring at v0.9. Massive retrofitting required.
Better: Auth in v0.2, logging in v0.1, monitoring throughout

**❌ "Big Bang" Roadmap:****
Build everything, test at the end. No incremental validation.

**❌ Technology-Driven Versions:**
v0.1 = Database, v0.2 = API, v0.3 = Frontend
Better: Each version has full stack for a feature

**❌ Sequential Waterfall:**
Each version 100% dependent on previous, no parallelization

**❌ Vague Completion Criteria:**
"v0.4 is done when it works" vs. "v0.4 complete when API returns data in <500ms"

**❌ Ignoring Learning:**
Roadmap created on day 1, never updated despite discoveries

---

## Roadmap as Living Document

Your roadmap should evolve:
- Update after each version completion
- Adjust based on UAT learnings
- Reprioritize based on user feedback
- Don't be afraid to add/remove/reorder versions

The roadmap serves you, not vice versa.

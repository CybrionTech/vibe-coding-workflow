# Vibe Coding Workflow

A systematic development workflow designed for non-coders building applications with AI assistance (Claude Code, ChatGPT, and other LLM tools).

## Overview

This workflow enables solo developers with infrastructure/application knowledge (but limited coding experience) to build production-quality software through structured collaboration with AI agents.

**Start Here:** Read [workflow-overview.md](workflow-overview.md) to understand the complete process.

---

## Core Documents

### You Interact With These (5 + README)

**1. [workflow-overview.md](workflow-overview.md)** - **START HERE**
- The complete process from idea to production
- Phase-by-phase breakdown
- Tool roles and approval gates
- Time investment estimates

**2. [mission-order-standard.md](mission-order-standard.md)**
- Rules for creating version execution plans
- Use with ChatGPT for each version

**3. [prd-template.md](prd-template.md)**
- Product Requirements Document structure
- Use once at project start with ChatGPT

**4. [roadmap-template.md](roadmap-template.md)**
- Version planning and decomposition
- Use once after PRD with ChatGPT

**5. [production-readiness-checklist.md](production-readiness-checklist.md)**
- v1.0 deployment gate (114 checks)
- Review early, complete before production

### Agents Reference These (3)

**6. [technical-handbook.md](technical-handbook.md)**
- Technical implementation details
- Git workflow, dependency management
- Agents read this, you rarely need to

**7. [lessons-learned-template.md](lessons-learned-template.md)**
- Structure for ongoing learning log

**8. [status-report-template.md](status-report-template.md)**
- Structure for version completion docs

---

## Quick Start

1. Read **[workflow-overview.md](workflow-overview.md)** - understand the process
2. Create PRD using `prd-template.md` + ChatGPT
3. Create Production-Aware Roadmap using `roadmap-template.md` + `production-readiness-checklist.md` + ChatGPT
5. For each version:
   - Create Mission Order using `mission-order-standard.md` + ChatGPT
   - Pass to Claude Code
   - Execute UAT
   - Mark complete

---

## Philosophy

**You focus on product decisions. AI handles implementation.**

- ChatGPT validates plans and completed code
- Claude Code implements with hive-mind agent coordination
- You make go/no-go decisions at approval gates
- Standards prevent common failure patterns
- Templates reduce decision fatigue

---

## When to Use This Workflow

- Building MVPs as a solo developer
- Limited coding background but strong domain knowledge
- Need systematic approach with quality gates
- Want traceable requirements → implementation → validation
- Building applications that require rigor (financial, healthcare, regulated domains)

---

## Standard Project Structure

```
project-root/
├── docs/
│   ├── prd.md
│   ├── roadmap.md
│   ├── lessons-learned.md
│   ├── versions/
│   │   ├── v0.1/
│   │   │   ├── mission-order.md
│   │   │   ├── uat-automated.md
│   │   │   ├── uat-user.md (if GUI)
│   │   │   ├── status-report.md
│   │   │   └── zen-plan.md (auto-generated)
│   │   └── v0.2/ ...
│   └── archive/
├── src/
├── tests/
├── config/
└── .claude/ (auto-generated)
```

---

## Document Usage

| Document | When | Purpose |
|----------|------|---------|
| workflow-overview.md | First | Understand complete process |
| prd-template.md | Project start | Define product vision |
| roadmap-template.md + production-readiness-checklist.md | After PRD | Create production-aware roadmap |
| mission-order-standard.md | Each version | Create execution plan |
| production-readiness-checklist.md | Before v1.0 | Validate standards met |
| technical-handbook.md | Never (agents use) | Technical reference |

---

## Time Investment

**Per Project (one-time):** 5-8 hours
- PRD: 2-4 hours
- Production-aware roadmap: 3-4 hours

**Per Version (6-10 times):** 3-6 hours each
- Mission order: 1-2 hours
- UAT: 1-3 hours
- Review: 1 hour

**Total for MVP:** 32-64 hours of your time over 2-6 months
- Agents handle 100+ hours of implementation

---

## Version History

- v1.0 - Initial workflow based on vibe-trader project learnings

---

## Contributing

This workflow is based on real-world experience. Improvements welcome based on your project needs.

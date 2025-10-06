# Workflow Walkthrough: From Idea to Shipped Product

## What You're About to Experience

This walkthrough shows you what it's like to build software using the Vibe Coding Workflow. You won't follow along step-by-step - instead, you'll understand the journey from idea to shipped product, and why each phase matters.

By the end, you'll understand:
- Why production-aware planning saves weeks of rework
- How the PVDD loop prevents "almost done" syndrome  
- What it feels like to ship with confidence
- How AI becomes your implementation partner

**The scenario:** Building a simple todo app. We'll walk through creating a roadmap with multiple versions (v0.1 through v1.0), then see how you'd execute each version using mission orders.

**Time to read:** 10 minutes

---

## The Traditional Approach (and Why It Fails)

**Typical solo dev project:**
1. "I'll build a todo app to learn [framework]"
2. Start coding immediately
3. Build features as you think of them
4. Realize you forgot error handling
5. Add authentication as an afterthought
6. "Deploy" = push to GitHub, hope it works
7. Never actually finish

**The problems:**
- No clear "done" definition
- Features stacked without planning
- Production concerns bolted on at the end
- Scope creep kills momentum

**The Vibe Coding Workflow approach:**
You make product decisions. AI implements. Quality gates ensure you ship.

---

## Phase 1: Know What You're Building (PRD)

**The moment:** You have an idea.

Instead of opening your code editor, you open your LLM and upload `prd-template.md`. You describe what you want to build.

**What happens:**
Your LLM asks questions you wouldn't have asked yourself:
- "Who's this for and what problem does it solve?"
- "How do you know when it's successful?"
- "What's explicitly OUT of scope?"

**The result:** Your fuzzy idea becomes a concrete specification. Not a 50-page document - a focused PRD that answers the important questions.

**What you learn:** Defining success criteria BEFORE building prevents endless tweaking. When your PRD says "todos persist across browser sessions," you know exactly what "done" looks like.

**Time investment:** 30 minutes that saves hours of rework.

---

## Phase 2: Plan for Production, Not Prototyping (Roadmap)

**The moment:** You have a clear PRD. Now you need to break it into buildable chunks.

You upload your PRD along with `roadmap-template.md` and `production-readiness-checklist.md` to your LLM.

**The conversation:**
Your LLM reviews the 114-item production checklist with you. Most don't apply to your todo app. But some do:
- Input validation (security)
- Error handling (reliability)
- Browser compatibility (deployment)

**The insight:** These aren't "v0.9 problems" - they're architectural decisions that affect how you build from day 1.

**What emerges:** A roadmap breaking the project into logical versions:

**v0.1 - Core Foundation**
- Basic add/display todos
- In-memory only (no persistence yet)
- DoD: Can add and see todos, basic UI works

**v0.2 - Persistence**  
- Add localStorage
- Error handling for storage failures
- DoD: Todos persist across sessions, errors handled gracefully

**v0.3 - Task Management**
- Mark complete/incomplete
- Delete todos
- DoD: Full CRUD operations work

**v0.4 - Polish & Production**
- Input validation (XSS prevention)
- Cross-browser testing
- README and documentation
- DoD: Production-ready, all standards met

**v1.0 - Release**
Final validation and tagging.

**The key point:** Each version is independently valuable. If you stop at v0.2, you have a working (if basic) todo app. This incremental approach prevents "it's 90% done" syndrome.

**The shift:** You're not just planning features. You're planning to ship something production-ready incrementally.

**Time investment:** 30 minutes that prevents retrofitting authentication and error handling later.

---

## Phase 3: Specify Each Version (Mission Orders)

**The moment:** You have a roadmap. Now you need to execute version by version.

**For each version** (v0.1, v0.2, v0.3, v1.0), you create a mission order.

You upload `mission-order-standard.md` to your LLM along with your roadmap, then ask it to create the mission order for the current version.

**What it generates:**
- Specific execution tasks for THIS version
- The DoD items from the roadmap entry
- Git workflow directives
- Dependencies on previous versions

**Example - Mission Order for v0.1:**
- Objectives: Build core foundation
- Dependencies: None (first version)
- Execution tasks:
  - Create basic HTML structure
  - Implement add todo function
  - Implement display todos function
  - Basic styling
- DoD items:
  - Can add todos via input field
  - Todos display in list
  - Basic UI works

**The pattern:** 
1. Create mission order for v0.1
2. Implement v0.1, test, complete
3. Create mission order for v0.2
4. Implement v0.2, test, complete
5. Repeat for each version

Each mission order builds on the previous version's work. Each version is independently shippable.

**The shift:** You're not building everything at once. You're shipping incrementally, learning from each version, adjusting the roadmap as needed.

**Time investment:** 15 minutes per version to create crystal-clear specifications.

---

## Phase 4: AI Implements, You Decide (PVDD Loop)

**The moment:** Mission order approved. Time for implementation.

You initialize Claude Flow and pass Claude Code the context:
- Read the PRD (understand the vision)
- Read the roadmap (understand the overall plan)
- Read the current version's mission order (understand this version's specifications)
- Execute using the PVDD loop

**What happens:**

**Plan:** Claude creates a Zen Plan - its detailed implementation strategy for this version

**Verify:** The plan gets validated by another LLM (via Zen MCP) - catches issues before any code is written

**Develop:** Claude implements according to the validated plan

**Deploy:** Automated validation runs, UAT documentation is generated

**Your role:** Monitor progress. Answer questions if Claude gets stuck. Review commits.

**What this feels like:**
You're collaborating at the product level while AI handles implementation details. You're not debugging syntax errors - you're validating that the right thing is being built.

**Time investment:** 30-60 minutes per version, mostly watching agents work.

---

## Phase 5: Validate What Matters (UAT)

**The moment:** Implementation complete for this version. Time to validate.

Claude has generated `uat-automated.md` with test scenarios based on the DoD items for this version.

**What you do:**
Claude has generated specific test scenarios in the UAT document based on the DoD items. You run through each one, following the provided instructions.

For v0.1, the UAT document might include scenarios like:
- "Add a todo with text 'Buy milk', verify it appears in the list"
- "Add 3 different todos, verify all 3 display correctly"
- "Verify UI renders properly without errors"

You execute these tests and mark each as PASS/FAIL in the document.

**When bugs appear:** Document the issue, Claude fixes it, you re-test. The bug gets fixed before moving to the next version.

**The shift:** UAT isn't a formality. It's proof that what you specified actually got built correctly.

**Time investment:** 10-20 minutes per version of focused testing.

---

## Phase 6: Complete Version, Start Next (Iteration)

**The moment:** All DoD items pass UAT for this version.

You ask your LLM to generate completion documentation for this version:
- Status report showing what was delivered
- Update lessons learned with insights from this version

**The git workflow:**
```bash
git merge --no-ff feature/v0.2/persistence
git tag -a v0.2 -m "Release v0.2: Add localStorage persistence"
```

**Then:** Start the next version. Create mission order for v0.3, repeat the cycle.

**The pattern:**
v0.1 complete → v0.2 complete → v0.3 complete → v0.4 complete → v1.0 complete

Each version is:
- Independently valuable
- Fully tested
- Properly documented
- Tagged in git

**The shift:** You're not building for months before shipping. You're shipping working software every few days or weeks.

**Time investment:** 15 minutes per version to document and commit.

---

## What Makes This Different

**Traditional approach:**
- Code first, plan later
- Production concerns are afterthoughts
- "Done" is ambiguous
- Testing is "it runs on my machine"

**Vibe Coding Workflow:**
- Plan with production in mind from day 1
- Clear definition of done before any code
- AI implements, you validate against business requirements
- Ship incrementally, learn continuously

**The mindset shift:**
You're not a coder trying to ship. You're a product thinker leveraging AI to implement systematically.

---

## The Ethos

**1. Production-Aware from Day 1**
Don't retrofit security and error handling. Architect for them from the start.

**2. Quality Gates, Not Hope**
Nothing proceeds without approval. Mission order approved before implementation. Plan validated before coding. UAT passed before moving to next version.

**3. Decisions Over Syntax**
You make product decisions. AI handles implementation mechanics.

**4. Traceability Matters**
Every line of code traces to a DoD item. Every DoD item traces to the roadmap. Every roadmap entry traces to the PRD.

**5. Learning Compounds**
Lessons from v0.1 improve v0.2. Lessons from v0.2 improve v0.3. The process gets better with each version.

---

## What This Enables

**For a simple project like this todo app:**
- 4-8 hours total from idea to shipped v1.0
- 4 versions building incrementally
- Each version independently useful
- Complete documentation

**For real projects:**
- Same process, just more versions (6-10 typical)
- Ship incrementally, validate constantly
- Maintain quality at scale

**The unlock:** Domain expertise + AI implementation + systematic workflow = shipped software.

---

## Your Turn

Understand the mindset:

1. **Define success before building** (PRD)
2. **Plan for production from day 1** (Production-aware roadmap with multiple versions)
3. **Execute version by version** (Mission order → Implement → UAT → Complete)
4. **Validate against requirements** (UAT for each version)
5. **Ship incrementally** (Each version tagged and documented)

The templates guide you. The workflow prevents rework. AI handles implementation. You make the decisions that matter.

**Start with:** `prd-template.md` and your idea. The rest follows naturally.

---

## What Happens Next

After reading this walkthrough, you understand the experience of the workflow.

**To actually use it:**
1. Review `workflow-overview.md` for complete process details
2. Use `prd-template.md` to define your project
3. Create your production-aware roadmap (multiple versions)
4. Execute version by version
5. Ship v1.0

You now understand WHY each step exists, not just WHAT the steps are.

---

**Ready to try it?** Start with a small idea. Follow the workflow. Ship something real.

**Ready to go deeper?** See `workflow-overview.md` for the complete reference.

---

**Version:** 1.0
**Last Updated:** 2025-10-05
**Purpose:** Understand the workflow mindset
**Next:** Use `workflow-overview.md` for implementation details

🎯 **Now you understand the journey. Go build something.**

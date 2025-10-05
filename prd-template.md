# Product Requirements Document Template

## Overview
This template guides creation of a comprehensive Product Requirements Document (PRD) for any application. Use this with ChatGPT to develop your PRD through guided questions.

---

## 1. Product Vision

**What is this product when complete (v1.0)?**

Describe the end state of your MVP in 2-3 sentences. What does the fully functional product look like?

---

## 2. User Context

**Who uses this product?**

Identify your primary user(s). For personal projects, this might be "myself" - that's fine.

**What problem does it solve?**

Articulate the core problem or pain point this product addresses. What's broken or missing that this fixes?

**What's the user's current workaround?**

How do users handle this problem today without your product? Understanding the current state helps define success.

---

## 3. Success Criteria

**How do you know the MVP is done?**

Define 3-5 measurable outcomes that indicate v1.0 is complete and successful.

Examples:
- User can complete [workflow] end-to-end without manual intervention
- System processes [X] items per minute with <1% error rate
- User completes core task in under [Y] minutes

**What would make this product a failure?**

Identify the anti-goals. What outcomes would mean this product didn't solve the problem?

---

## 4. Core Capabilities

**What must this product do?**

List the essential features/capabilities required for MVP. Focus on "must have" not "nice to have."

1. Capability 1
   - Sub-feature A
   - Sub-feature B
2. Capability 2
   - Sub-feature A
   - Sub-feature B
3. Capability 3

Keep this list focused. If you have more than 10 core capabilities, you're probably describing multiple products.

---

## 5. Technical Constraints

**Platform/Environment:**
- Where does this run? (web app, desktop, mobile, CLI, etc.)
- What technologies are required or preferred?
- What existing systems must it integrate with?

**Performance Requirements:**
- Response time expectations
- Scalability needs (concurrent users, data volume)
- Availability requirements (uptime %)

**Security/Privacy:**
- Data sensitivity levels
- Authentication/authorization needs
- Compliance requirements (if any)

---

## 6. Domain-Specific Requirements

*(Include this section only if your product operates in a regulated or specialized domain)*

**Regulatory/Compliance:**
- Industry regulations that apply
- Audit trail requirements
- Data retention policies

**Safety/Risk Management:**
- Safety-critical features
- Risk mitigation requirements
- Fail-safe behaviors

**Domain Expertise:**
- Specialized knowledge required
- Domain-specific validation rules
- Industry standards to follow

---

## 7. Development Constraints

**Your Skill Level:**
- Technical background (what you know)
- Learning limitations (what you can't/won't learn for this project)
- Acceptable complexity level

**Time Budget:**
- Available hours per week
- Target completion timeline
- Milestone deadlines (if any)

**Maintainability:**
- Who will maintain this long-term?
- Code complexity tolerance
- Documentation requirements

**Tooling Dependencies:**
- AI assistance requirements (ChatGPT, Claude Code, etc.)
- Development tools that must be used
- Limitations of your development environment

---

## 8. Out of Scope

**What will v1.0 explicitly NOT do?**

List features, use cases, or capabilities that are intentionally excluded from the MVP. This prevents scope creep.

Examples:
- Multi-user support (v1.0 is single-user only)
- Mobile app (v1.0 is web-only)
- Real-time sync (v1.0 uses batch processing)
- Advanced analytics (v1.0 provides basic reporting only)

---

## Optional Sections

### 9. API/Integration Specifications *(Optional - for systems with external integrations)*

**REST API Endpoints:**
```
GET /api/resource/{id}
POST /api/resource
```

**WebSocket Topics:**
```
subscribe: data:symbol:AAPL
message: {type: "bar", data: {...}}
```

**Data Structures:**
```javascript
{
  field1: "type",
  field2: "type"
}
```

Include this section if your product has well-defined API contracts that inform implementation.

---

### 10. Visual Design Guidelines *(Optional - if GUI in scope)*

**Color Scheme:**
- Primary: #hexcode
- Secondary: #hexcode
- Success/Error/Warning states

**Typography:**
- Headers: font-family, size, weight
- Body: font-family, size
- Monospace (for code/data): font-family

**Spacing:**
- Card padding, margins
- Grid system (if any)

**Component Library:**
- Use [library name] or build custom

Include this section for GUI-heavy applications where visual consistency matters.

---

### 11. Mock Data Structures *(Optional - for prototyping)*

**Sample Data for Testing:**
```javascript
const mockUsers = [
  {id: 1, name: "Test User", email: "test@example.com"},
  {id: 2, name: "Demo User", email: "demo@example.com"}
];

const mockConfig = {
  apiUrl: "http://localhost:8000",
  timeout: 5000
};
```

Include mock data structures if prototyping before backend is ready, or for testing scenarios.

---

## Using This Template with ChatGPT

### Initial PRD Generation

Upload this template to ChatGPT and use this prompt:

```
I'm building [brief product description]. Help me create a PRD using this template. 
Ask me questions section-by-section to fill in the details. Start with Product Vision.
```

ChatGPT will guide you through each section with targeted questions.

### Refining Sections

If a section needs more detail:

```
The [section name] needs more clarity. Help me articulate [specific aspect] 
in a way that's concrete and testable.
```

### Validating Completeness

Once you have a draft:

```
Review this PRD draft. What's missing or unclear for a solo developer building [product type]? 
Are the success criteria measurable? Is the scope realistic?
```

### Converting PRD to Roadmap

After PRD is complete:

```
Based on this PRD, help me create a roadmap that breaks this into 6-8 logical versions. 
Each version should deliver incremental value and stack on the previous version.
```

---

## Tips for Effective PRDs

**Be Specific:**
- "Fast response time" → "API responds in <500ms for 95% of requests"
- "User-friendly" → "User completes core task in <3 clicks"

**Stay Focused:**
- If your Core Capabilities section has 15 items, you're building too much
- Ruthlessly cut "nice to have" features
- Remember: You can always build v2.0

**Know Your Constraints:**
- Be honest about your skill level in Development Constraints
- Don't commit to technologies you can't maintain
- Factor in your actual available time

**Define Success Early:**
- Success Criteria should be testable from day one
- If you can't measure success, you can't validate your MVP
- Anti-goals help you stay focused on what matters

---

## PRD Maintenance

PRDs are living documents:
- Update as you learn during development
- Mark sections that change with version number
- Keep a changelog at the bottom

**Changelog Format:**
```
## Changelog
- v1.1 (2024-XX-XX): Updated Success Criteria based on v0.3 learnings
- v1.0 (2024-XX-XX): Initial PRD
```

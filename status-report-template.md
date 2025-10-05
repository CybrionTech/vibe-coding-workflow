# Status Report Template

## Overview
This template provides structure for documenting version completion, deliverables, outcomes, and deployment readiness. Status Reports are created only after UAT is completed and approved.

---

## Header

```markdown
# [Version] Status Report: [Version Name]

**Version:** [vX.X]
**Date:** [Completion Date]
**Status:** [âœ… COMPLETE | ðŸŸ¡ CONDITIONAL | ðŸ"´ INCOMPLETE]
**Report Author:** [Name/Role]
**Related Documents:**
- Mission Order: [`docs/versions/vX.X/mission-order.md`]
- UAT Automated: [`docs/versions/vX.X/uat-automated.md`]
- UAT User: [`docs/versions/vX.X/uat-user.md`] (if GUI)
- Zen Plan: [`docs/versions/vX.X/zen-plan.md`]
```

---

## 1. Executive Summary

**Brief overview (3-5 sentences):**
- What was delivered
- Current status (complete/conditional/incomplete)
- Key achievements
- Known limitations
- Deployment recommendation

---

## 2. DoD Completion Status

### Scorecard

| DoD # | Item | Status | Evidence | Notes |
|-------|------|--------|----------|-------|
| DoD-1 | [Description] | âœ… PASS | [UAT section] | [Any notes] |
| DoD-2 | [Description] | ðŸŸ¡ CONDITIONAL | [UAT section] | [Pending item] |
| DoD-3 | [Description] | ðŸ"´ FAIL | [UAT section] | [Issue] |

**Overall DoD Status:** X/Y Complete (Z%)

---

## 3. Implementation Summary

### What Was Delivered

**Code Deliverables:**
- Feature 1: [Description + file paths]
- Feature 2: [Description + file paths]
- Feature 3: [Description + file paths]

**Test Deliverables:**
- Unit tests: [Count] tests, [Coverage]%
- Integration tests: [Count] scenarios
- UAT scenarios: [Count] validated

**Documentation Deliverables:**
- [Doc 1]: [Path]
- [Doc 2]: [Path]

### What Was Deferred

**Out of Scope (Planned):**
- Item 1: [Reason for deferral]
- Item 2: [Reason for deferral]

**Discovered During Development:**
- Item 3: [Why deferred, target version]

---

## 4. File Inventory

### Source Files Created/Modified

| Path | Lines | Purpose |
|------|-------|---------|
| `src/feature.js` | 245 | Core feature implementation |
| `src/utils.js` | 89 | Helper utilities |
| `tests/feature.test.js` | 156 | Feature tests |

**Total Source Lines:** [Count]
**Total Test Lines:** [Count]
**Test/Code Ratio:** [Ratio]

### Configuration Files

| Path | Purpose |
|------|---------|
| `config/app.yaml` | Application configuration |
| `.env.example` | Environment variables template |

---

## 5. Quality Metrics

### Test Coverage

| Component | Coverage | Target | Status |
|-----------|----------|--------|--------|
| Feature A | 95% | >90% | âœ… Exceeds |
| Feature B | 88% | >85% | âœ… Meets |
| Overall | 92% | >85% | âœ… Excellent |

### Performance Metrics

| Metric | Value | Target | Status |
|--------|-------|--------|--------|
| API Response Time | 245ms | <500ms | âœ… Under target |
| Page Load Time | 1.2s | <2s | âœ… Fast |
| Memory Usage | 180MB | <300MB | âœ… Efficient |

### Code Quality

| Metric | Value | Notes |
|--------|-------|-------|
| Linter Warnings | 0 | Clean |
| Type Errors | 0 | Fully typed |
| Complexity Score | 8.5/10 | Maintainable |

---

## 6. UAT Results Summary

### Automated UAT

**Execution Date:** [Date]
**Executor:** Claude Code agents
**Duration:** [Time]

**Results:**
- Total Tests: [Count]
- Passed: [Count]
- Failed: [Count]
- Skipped: [Count]

**Pass Rate:** [Percentage]%

**Key Findings:**
- Finding 1
- Finding 2

### User UAT (if applicable)

**Execution Date:** [Date]
**Executor:** [User name]
**Duration:** [Time]

**Results:**
- Total Scenarios: [Count]
- Passed: [Count]
- Issues Found: [Count]

**User Feedback:**
- Feedback 1
- Feedback 2

---

## 7. Known Issues & Limitations

### Critical Issues (Blockers)

None / [List if any]

### Non-Critical Issues

| Issue | Severity | Workaround | Target Fix |
|-------|----------|------------|------------|
| [Description] | Low | [Workaround] | v[X.X] |

### Acknowledged Limitations

- Limitation 1: [Description + why acceptable]
- Limitation 2: [Description + why acceptable]

---

## 8. Dependencies & Integration

### External Dependencies

| Dependency | Version | Status | Notes |
|------------|---------|--------|-------|
| Library A | 2.1.0 | âœ… Stable | No issues |
| Service B | API v3 | ðŸŸ¡ Rate limited | Free tier |

### Integration Points

**Validated:**
- Integration with Feature X: âœ… Working
- Integration with Service Y: âœ… Working

**Pending:**
- Integration with Feature Z: Deferred to v[X.X]

---

## 9. Deployment Readiness

### Pre-Deployment Checklist

- [âœ…] All DoD items passed
- [âœ…] UAT approved
- [âœ…] Documentation complete
- [âœ…] Configuration validated
- [âœ…] Secrets properly managed
- [ ] Production environment prepared (if applicable)

### Deployment Recommendation

**Status:** [READY | READY WITH CONDITIONS | NOT READY]

**Recommendation:**
[Detailed recommendation with any conditions]

**Deployment Steps:**
1. Step 1
2. Step 2
3. Step 3

### Rollback Plan

**If deployment fails:**
1. Rollback step 1
2. Rollback step 2
3. Restore from backup

---

## 10. Lessons Learned Preview

**Top 3 Insights:**
1. [What worked well]
2. [What could improve]
3. [Recommendation for next version]

*(Full details in `docs/lessons-learned.md`)*

---

## 11. Next Steps

### Immediate Actions

- [ ] Merge feature branch to main
- [ ] Tag release v[X.X]
- [ ] Update lessons-learned.md
- [ ] Deploy to [environment]

### Preparing for v[X.X+1]

- [ ] Review roadmap for next version
- [ ] Create Mission Order for v[X.X+1]
- [ ] Address deferred items if prioritized

---

## Approval Signatures

**Created By:** [Agent/Person]
**Reviewed By:** [User Name]
**Approval Date:** [Date]

**Status:** [APPROVED | APPROVED WITH CONDITIONS | REJECTED]

**Conditions (if any):**
- Condition 1
- Condition 2

---

## Appendices

### A. Performance Benchmarks

Detailed performance test results...

### B. Security Scan Results

Security audit findings...

### C. Detailed Test Results

Complete test execution logs...

---

## Changelog

| Date | Version | Changes |
|------|---------|---------|
| [Date] | 1.0 | Initial status report |


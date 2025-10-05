# Technical Handbook

## Overview

This handbook contains technical implementation details that Claude Code agents reference during development. Users rarely need to read this - it's for agents to follow best practices.

**Contents:**
1. Project Structure
2. Efficiency Patterns  
3. Git Workflow
4. Dependency Management
5. Environment Configuration
6. PVDD Technical Details

---

## 1. Project Structure

Standard folder organization:

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

**File Organization Rules:**
- NEVER save working files to root
- Use `/src` for source code
- Use `/tests` for test files
- Use `/docs` for documentation
- Use `/config` for configuration

---

## 2. Efficiency Patterns

### Concurrent Execution ("1 MESSAGE = ALL OPERATIONS")

**Golden Rule:** Batch ALL related operations in ONE message.

**TodoWrite** - Batch 5-10+ todos:
```javascript
TodoWrite { todos: [
  {id: "1", content: "Task 1", status: "in_progress"},
  {id: "2", content: "Task 2", status: "pending"},
  // ... 8 more todos
]}
```

**File Operations** - Batch reads/writes/edits:
```javascript
[Single Message]:
  Read "file1.js"
  Read "file2.js"
  Write "newfile.js"
  Edit "file3.js"
```

**Agent Spawning** - Use Task tool for ALL agents:
```javascript
[Single Message]:
  Task("Backend Dev", "Build API...", "backend-dev")
  Task("Frontend Dev", "Build UI...", "coder")
  Task("Tester", "Write tests...", "tester")
```

### Agent Coordination Protocol

**Before Work:**
```bash
npx claude-flow@alpha hooks pre-task --description "[task]"
```

**During Work:**
```bash
npx claude-flow@alpha hooks post-edit --file "[file]" --memory-key "swarm/[agent]/[step]"
npx claude-flow@alpha hooks notify --message "[progress]"
```

**After Work:**
```bash
npx claude-flow@alpha hooks post-task --task-id "[task]"
```

---

## 3. Git Workflow

### Branch Strategy

**Main branch:** Always deployable, protected
**Feature branches:** `feature/{version}/{brief-name}`
**Hotfix branches:** `hotfix/{version}/{issue}`

### Merge Requirements

Before merging to main:
- [ ] All DoD items passed
- [ ] Automated UAT complete
- [ ] User UAT approved (if GUI)
- [ ] Status Report created
- [ ] Lessons Learned updated
- [ ] No merge conflicts

### Merge Process

```bash
# Update feature branch
git checkout feature/v0.3/historical-data
git merge origin/main
npm test

# Merge to main
git checkout main
git merge --no-ff feature/v0.3/historical-data
git tag -a v0.3 -m "Release v0.3: [description]"
git push origin main --tags

# Cleanup
git branch -d feature/v0.3/historical-data
```

### Commit Message Format

```
[{version}] {type}: {brief description}

{detailed description}

Objectives completed:
- Objective 1
- Objective 2

DoD items: DoD-X, DoD-Y
Files modified: {count}
```

**Commit types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `test`: Adding/updating tests
- `refactor`: Code restructure
- `perf`: Performance improvement
- `chore`: Maintenance
- `security`: Security fixes

### Hotfix Process

```bash
# Emergency fix
git checkout main
git checkout -b hotfix/v0.3/critical-bug

# Fix, test, merge
git checkout main
git merge --no-ff hotfix/v0.3/critical-bug
git tag -a v0.3.1 -m "Hotfix: [description]"
git push origin main --tags

# Apply to active feature branch
git checkout feature/v0.4/backtest-engine
git merge main
```

---

## 4. Dependency Management

### Lock Files

**Always commit:**
- `package-lock.json` (Node.js)
- `requirements.txt` / `Pipfile.lock` (Python)
- `Gemfile.lock` (Ruby)
- `composer.lock` (PHP)

**Never** add lock files to `.gitignore`.

### Update Timing

**Within version:** Avoid updates except security patches
**Between versions:** Safe to update dependencies
**Before production:** Comprehensive audit required

### Update Process

```bash
# Check for updates
npm outdated

# Security scan
npm audit

# Update selectively
npm update <package-name>

# Test
npm test

# Commit
git commit -m "[v0.4] chore: Update dependencies

Security updates:
- express 4.17.1 → 4.18.2 (CVE-2022-XXXX)

Breaking changes: None
Tests passing: Yes"
```

### Security Response

**Critical/High:** Fix immediately
**Medium:** Schedule for current/next version
**Low:** Batch with regular updates

```bash
npm audit
npm audit fix

# If breaking change needed
npm install <package>@<safe-version>
npm test

git commit -m "[v0.X] security: Fix CVE-XXXX"
```

### Dependency Selection

**Before adding dependency:**
1. Actively maintained? (commits in 6 months)
2. Popular/well-used?
3. Good documentation?
4. License compatible?
5. What transitive dependencies?
6. Can implement in <100 lines?

**Version constraints:**
```json
{
  "express": "~4.18.0",     // Patch only
  "lodash": "^4.17.21",      // Minor + patch
  "react": "18.2.0"          // Exact (critical)
}
```

---

## 5. Environment Configuration

### Externalize All Config

**Required:**
- All environment-specific values in `.env` files
- No hardcoded credentials in code
- No hardcoded URLs in code
- `.env.example` with placeholders

### Environment Types

**Development:** Local machine
**Staging:** Pre-production testing
**Production:** Live system

### Configuration Management

```bash
# .env.example (commit this)
DATABASE_URL=postgresql://localhost/myapp
API_KEY=your_api_key_here
NODE_ENV=development

# .env (NEVER commit this)
DATABASE_URL=postgresql://user:pass@prod-db/myapp
API_KEY=actual_secret_key_here
NODE_ENV=production
```

### Secrets Management

**Never:**
- Commit secrets to git
- Hardcode API keys
- Share .env files
- Log sensitive data

**Always:**
- Use environment variables
- Rotate secrets regularly
- Validate config on startup
- Document required variables

---

## 6. PVDD Technical Details

### Plan Phase

**Agent responsibilities:**
- Review Mission Order
- Create Zen Plan
- Identify risks and assumptions
- Cross-check against DoD
- Pass to ChatGPT for validation

### Verify Phase

**ChatGPT validates:**
- Technical approach sound?
- Risks identified?
- Dependencies clear?
- DoD items testable?

If issues found, revise Zen Plan.

### Develop Phase

**Agent responsibilities:**
- Implement per Execution Tasks
- Write tests continuously
- Follow efficiency patterns
- Commit per git directives
- Run automated UAT

**ChatGPT code validation:**
- Router registration
- Component imports
- Event handler wiring
- Environment config (no hardcoded secrets)

### Deploy Phase

**Agent responsibilities:**
- Run user UAT (if applicable)
- Generate Status Report
- Update Lessons Learned
- Merge to main and tag

---

## Common Technical Issues

### Frontend Integration Failures

**Symptoms:** Routes 404, buttons don't work, components missing

**Root Causes:**
- Routes not registered in backend
- Components not imported
- Event handlers not wired
- Build configuration incorrect

**Prevention:**
- Frontend smoke tests in DoD
- ChatGPT code validation
- Automated UAT checks

### Dependency Conflicts

**Symptoms:** Build fails, runtime errors, version mismatches

**Root Causes:**
- Lock files not committed
- Breaking changes in updates
- Incompatible peer dependencies

**Prevention:**
- Always commit lock files
- Update between versions only
- Test after any dependency change

### Environment Configuration Issues

**Symptoms:** Works locally, fails in production

**Root Causes:**
- Hardcoded environment values
- Missing environment variables
- .env not deployed

**Prevention:**
- Externalize all config
- Validate config on startup
- Document required variables

---

## Agent Best Practices

**Code Organization:**
- Keep modules under 500 lines
- Clear separation of concerns
- Consistent naming conventions
- Comprehensive error handling

**Testing:**
- Write tests before/during implementation
- Aim for >85% coverage
- Test edge cases
- Include integration tests

**Documentation:**
- Clear code comments where needed
- Update README with changes
- Document configuration requirements
- Maintain API documentation

**Git Hygiene:**
- Commit frequently with clear messages
- Never commit broken code
- Run tests before committing
- Push to remote daily

---

This handbook is living documentation. Update as new patterns emerge or issues are discovered.

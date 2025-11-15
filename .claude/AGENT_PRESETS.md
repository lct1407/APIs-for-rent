# Agent Presets & Workflows

This document defines recommended agent configurations and workflows for common development scenarios in the RentAPI project.

## 🎯 Agent Roles

### 1. Backend Developer Agent

**Focus**: FastAPI, Python, PostgreSQL, Redis, Celery

**Skills**:
- api-testing
- database-migration
- security-audit

**Commands**:
- /test-backend
- /migrate
- /security-check

**Typical Workflows**:

**Adding a new API endpoint**:
1. Create endpoint in `backend/app/api/v1/`
2. Define Pydantic schemas in `backend/app/schemas/`
3. Create service logic in `backend/app/services/`
4. Use **api-testing** skill to write comprehensive tests
5. Run `/test-backend` to verify
6. Run `/security-check` to ensure security
7. Use `/api-docs` to update documentation

**Modifying database schema**:
1. Update SQLAlchemy models in `backend/app/models/`
2. Use **database-migration** skill to create migration
3. Run `/migrate` to apply changes
4. Update tests to reflect schema changes
5. Run `/test-backend` to verify

### 2. Frontend Developer Agent

**Focus**: React, TypeScript, Tailwind CSS, Vite

**Skills**:
- frontend-testing

**Commands**:
- /test-frontend
- /code-review

**Typical Workflows**:

**Adding a new component**:
1. Create component in `client/src/components/`
2. Follow existing patterns (shadcn/ui style)
3. Use **frontend-testing** skill to write tests
4. Run `/test-frontend` to verify
5. Run `/code-review` for quality check

**Adding a new page**:
1. Create page in `client/src/pages/`
2. Add route in `client/src/App.tsx`
3. Add to sidebar navigation if needed
4. Write tests for the page
5. Test responsive design
6. Run `/test-frontend`

### 3. Full-Stack Developer Agent

**Focus**: End-to-end features

**Skills**:
- api-testing
- frontend-testing
- database-migration

**Commands**:
- /test-backend
- /test-frontend
- /migrate
- /dev-start

**Typical Workflows**:

**Implementing a new feature**:
1. Design database schema changes
2. Use **database-migration** skill for schema
3. Create backend API endpoints
4. Use **api-testing** skill for backend tests
5. Create frontend components
6. Use **frontend-testing** skill for frontend tests
7. Run `/test-backend` and `/test-frontend`
8. Integration test the full feature
9. Run `/code-review`

### 4. DevOps/Deployment Agent

**Focus**: Infrastructure, deployment, monitoring

**Skills**:
- deployment
- security-audit

**Commands**:
- /deploy-check
- /security-check
- /quick-fix

**Typical Workflows**:

**Preparing for deployment**:
1. Run `/security-check` for vulnerabilities
2. Use **security-audit** skill for comprehensive review
3. Fix any critical issues
4. Run `/deploy-check` for readiness
5. Use **deployment** skill for deployment
6. Monitor post-deployment
7. Have `/quick-fix` ready for issues

### 5. QA/Testing Agent

**Focus**: Quality assurance, testing, bug fixing

**Skills**:
- api-testing
- frontend-testing
- security-audit

**Commands**:
- /test-backend
- /test-frontend
- /security-check
- /code-review

**Typical Workflows**:

**Pre-release testing**:
1. Run `/test-backend` for all backend tests
2. Run `/test-frontend` for all frontend tests
3. Use **api-testing** skill to add missing tests
4. Use **frontend-testing** skill to add missing tests
5. Run `/security-check` for vulnerabilities
6. Perform manual testing
7. Document bugs and fixes

### 6. UI/UX Designer Agent

**Focus**: Beautiful, creative interfaces, user experience

**Skills**:
- ui-ux-design
- frontend-testing

**Commands**:
- /ui-review
- /generate-component
- /design-tokens
- /test-frontend

**Typical Workflows**:

**Creating new components**:
1. Use **ui-ux-design** skill for design patterns
2. Use `/generate-component` for beautiful implementations
3. Test with `/test-frontend`
4. Review with `/ui-review` for consistency

**Redesigning existing UI**:
1. Run `/ui-review` to audit current design
2. Use `/design-tokens` to review design system
3. Use **ui-ux-design** skill for modern patterns
4. Implement improvements
5. Test accessibility and responsiveness
6. Run `/ui-review` again to verify

### 7. Maintenance Agent

**Focus**: Bug fixes, updates, refactoring

**Skills**:
- All skills

**Commands**:
- /quick-fix (most used!)
- /test-backend
- /test-frontend
- /code-review

**Typical Workflows**:

**Fixing a bug**:
1. Reproduce the bug
2. Use `/quick-fix` for common issues
3. Write failing test first
4. Fix the bug
5. Verify test passes
6. Run `/code-review`
7. Deploy fix

**Updating dependencies**:
1. Update package versions
2. Run `/test-backend` and `/test-frontend`
3. Run `/security-check` for new vulnerabilities
4. Test manually
5. Document breaking changes

## 🔄 Common Workflows

### Daily Development Startup

```
/dev-start
```

Expected output:
- Status of all services (Backend, Frontend, PostgreSQL, Redis)
- URLs to access services
- Commands to start each service

### Pre-Commit Workflow

```
1. /test-backend
2. /test-frontend
3. /code-review
4. If all pass → commit
```

### Pre-Deployment Workflow

```
1. /test-backend
2. /test-frontend
3. /security-check
4. /deploy-check
5. If readiness > 90% → deploy
```

### Troubleshooting Workflow

```
1. /quick-fix  (diagnose and fix common issues)
2. If not fixed → describe issue to Claude
3. Claude uses appropriate skill for complex debugging
```

### Feature Development Workflow

```
1. Plan feature with Claude
2. Database changes → database-migration skill
3. Backend API → api-testing skill
4. Frontend UI → frontend-testing skill
5. /test-backend
6. /test-frontend
7. /code-review
8. /security-check (if security-sensitive)
9. Commit and push
```

## 🎨 Agent Personality Traits

### Backend Developer Agent
- **Personality**: Methodical, security-conscious, performance-focused
- **Communication**: Technical, precise, includes code examples
- **Priorities**: 1) Security, 2) Performance, 3) Scalability

### Frontend Developer Agent
- **Personality**: User-focused, design-conscious, accessibility-aware
- **Communication**: Visual, includes UI/UX considerations
- **Priorities**: 1) User experience, 2) Accessibility, 3) Performance

### UI/UX Designer Agent
- **Personality**: Creative, detail-oriented, empathetic to user needs
- **Communication**: Visual examples, design patterns, aesthetic focus
- **Priorities**: 1) Beauty & Delight, 2) Usability, 3) Accessibility

### DevOps Agent
- **Personality**: Reliability-focused, automation-oriented, proactive
- **Communication**: Checklist-driven, includes monitoring
- **Priorities**: 1) Reliability, 2) Security, 3) Automation

### QA Agent
- **Personality**: Detail-oriented, skeptical, thorough
- **Communication**: Test-case focused, includes edge cases
- **Priorities**: 1) Coverage, 2) Edge cases, 3) User scenarios

## 📋 Skill Combination Patterns

### Pattern 1: New Feature (Full Stack)
```
database-migration → api-testing → frontend-testing → security-audit
```

### Pattern 2: Security Review
```
security-audit → api-testing (security tests) → code-review
```

### Pattern 3: Performance Optimization
```
api-testing (load tests) → database-migration (indexes) → deployment (monitoring)
```

### Pattern 4: Bug Fix
```
api-testing (reproduce) → code-review → api-testing (verify)
```

## 🚀 Advanced Workflows

### CI/CD Pipeline Simulation

Simulate what your CI/CD pipeline should do:

```bash
# 1. Linting
cd backend && black . && flake8
cd client && npm run lint

# 2. Type checking
cd backend && mypy app/
cd client && tsc --noEmit

# 3. Tests
/test-backend
/test-frontend

# 4. Security
/security-check

# 5. Build
cd client && npm run build

# 6. Deployment check
/deploy-check

# If all pass → deploy
```

### Comprehensive Code Review

For major PRs or releases:

```
1. /code-review (initial review)
2. /test-backend (verify tests)
3. /test-frontend (verify tests)
4. /security-check (security review)
5. Manual testing
6. Performance testing
7. /api-docs (verify documentation)
8. Final approval
```

### Onboarding New Developer

Help new developers get started:

```
1. Read CLAUDE.md (project guide)
2. Read .claude/README.md (this guide)
3. /dev-start (set up environment)
4. /quick-fix (resolve any issues)
5. Run example workflows
6. Practice with /test-backend, /test-frontend
```

## 🎯 Task-to-Agent Mapping

| Task | Recommended Agent | Primary Skills/Commands |
|------|-------------------|-------------------------|
| Add new API endpoint | Backend Developer | api-testing, /test-backend |
| Add new React component | Frontend Developer | frontend-testing, /test-frontend |
| Design beautiful UI component | UI/UX Designer | ui-ux-design, /generate-component |
| UI/UX audit and improvements | UI/UX Designer | /ui-review, ui-ux-design |
| Design system updates | UI/UX Designer | /design-tokens, ui-ux-design |
| Database schema change | Backend Developer | database-migration, /migrate |
| Security vulnerability fix | DevOps + Backend | security-audit, /security-check |
| Deploy to production | DevOps | deployment, /deploy-check |
| Fix broken tests | QA Agent | /test-backend, /test-frontend |
| Environment setup | Maintenance | /dev-start, /quick-fix |
| Code review | Any agent | /code-review |
| Bug investigation | Maintenance | /quick-fix, relevant testing skill |
| Performance optimization | Backend Developer | api-testing, database-migration |
| Accessibility improvements | UI/UX Designer | ui-ux-design, /ui-review |
| Documentation update | Any agent | /api-docs |

## 💡 Pro Tips

1. **Chain commands**: `Can you /test-backend, then /code-review, then /security-check?`

2. **Context matters**: Provide context before using skills
   ```
   I'm adding a payment processing endpoint. Can you use the api-testing skill to help me write comprehensive tests, especially for security?
   ```

3. **Iterative development**: Use skills iteratively
   ```
   database-migration (create schema)
   → /test-backend (verify)
   → api-testing (write tests)
   → /test-backend (run tests)
   → /security-check (verify security)
   ```

4. **Ask for recommendations**:
   ```
   I need to add user notifications. Which agent preset should I use?
   ```

5. **Combine human + AI strengths**:
   - Human: Design decisions, user requirements, business logic
   - AI Agent: Implementation, testing, security checks, best practices

## 📊 Agent Performance Metrics

Track these metrics to optimize agent usage:

- **Time saved**: Compare manual vs. agent-assisted tasks
- **Bug prevention**: Bugs caught by agents vs. bugs in production
- **Test coverage**: Coverage improvement with testing skills
- **Security issues**: Vulnerabilities found by security-audit skill
- **Deployment success rate**: Success rate after using deploy-check

## 🔮 Future Agent Enhancements

Planned improvements:

1. **Performance Testing Agent**: Load testing, optimization
2. **Documentation Agent**: Auto-generate docs from code
3. **Migration Agent**: Major version upgrades, framework migrations
4. **Monitoring Agent**: Real-time monitoring, alerting
5. **Code Generation Agent**: Boilerplate generation, scaffolding

---

**Last Updated**: 2025-11-15
**Version**: 1.1.0
**Maintained By**: Claude Code AI Assistant

## Quick Reference

**Most Used Commands**:
- `/dev-start` - Start development
- `/test-backend` - Test backend
- `/test-frontend` - Test frontend
- `/quick-fix` - Fix common issues
- `/code-review` - Review code
- `/ui-review` - Review UI/UX design
- `/generate-component` - Generate beautiful components

**Most Used Skills**:
- `api-testing` - Backend testing
- `database-migration` - Schema changes
- `ui-ux-design` - Beautiful interfaces
- `security-audit` - Security review
- `deployment` - Production deployment

**Most Common Workflow**:
```
Feature → database-migration → api-testing → ui-ux-design → frontend-testing
→ /test-backend → /test-frontend → /ui-review → /code-review → Deploy
```

# Claude Code Configuration

This directory contains skills, commands, and agent presets for the RentAPI project.

## 📁 Directory Structure

```
.claude/
├── skills/              # Specialized skills for complex tasks
│   ├── api-testing.md
│   ├── database-migration.md
│   ├── deployment.md
│   ├── frontend-testing.md
│   ├── security-audit.md
│   └── ui-ux-design.md
├── commands/            # Slash commands for quick tasks
│   ├── api-docs.md
│   ├── code-review.md
│   ├── deploy-check.md
│   ├── design-tokens.md
│   ├── dev-start.md
│   ├── generate-component.md
│   ├── migrate.md
│   ├── quick-fix.md
│   ├── security-check.md
│   ├── test-backend.md
│   ├── test-frontend.md
│   └── ui-review.md
└── README.md           # This file
```

## 🎯 Skills

Skills are specialized capabilities that Claude can use for complex, multi-step tasks. They provide detailed instructions and best practices.

### Available Skills

#### 1. **api-testing**
Test FastAPI endpoints with comprehensive coverage.

**When to use**: Testing API endpoints, verifying responses, debugging API issues

**Key features**:
- Happy path and error case testing
- Authentication and authorization testing
- Input validation testing
- Rate limiting testing
- Coverage reporting

**Example usage**:
```
Can you test the webhook endpoints using the api-testing skill?
```

#### 2. **database-migration**
Manage Alembic database migrations for PostgreSQL schema changes.

**When to use**: Creating migrations, modifying database schema, managing database versions

**Key features**:
- Auto-generate migrations from model changes
- Manual migration creation
- Migration testing (upgrade/downgrade)
- Data migration support
- Safety checks

**Example usage**:
```
I need to add a new column to the users table. Can you help me create a migration?
```

#### 3. **frontend-testing**
Test React/TypeScript components with Vitest and React Testing Library.

**When to use**: Testing React components, hooks, or frontend functionality

**Key features**:
- Component testing patterns
- Hook testing
- User interaction testing
- Async operation testing
- Coverage reporting

**Example usage**:
```
Can you help me write tests for the UserDashboard component?
```

#### 4. **deployment**
Deploy the rental API platform to production environments.

**When to use**: Deploying to staging/production, setting up infrastructure, configuring deployment pipelines

**Key features**:
- Pre-deployment checklist
- Multiple deployment options (Docker, PaaS, VPS)
- Environment configuration
- Database backup strategy
- Zero-downtime deployment
- Rollback procedures

**Example usage**:
```
I want to deploy this to production using Docker. Can you help?
```

#### 5. **security-audit**
Perform comprehensive security audits on the rental API platform.

**When to use**: Identifying security vulnerabilities, checking best practices, performing security reviews

**Key features**:
- Authentication & authorization audit
- Input validation & injection prevention
- API security review
- Data protection audit
- Dependency vulnerability scanning
- Payment security review

**Example usage**:
```
Can you perform a security audit on the authentication system?
```

#### 6. **ui-ux-design**
Create beautiful, creative, and user-friendly interfaces with modern design principles.

**When to use**: Designing new components, improving UI aesthetics, ensuring accessibility, creating delightful user experiences

**Key features**:
- Modern UI patterns (glassmorphism, neumorphism, gradients)
- Advanced component patterns (hero sections, pricing cards, dashboards)
- Typography & hierarchy best practices
- Accessibility (a11y) compliance
- Responsive design strategies
- Dark mode excellence
- Beautiful form design
- Micro-interactions & animations
- Design system tokens

**Example usage**:
```
Can you help me create a beautiful pricing card with gradient accents?
Can you use the ui-ux-design skill to redesign our dashboard with modern UI trends?
```

## ⚡ Slash Commands

Slash commands are quick shortcuts for common development tasks. They're faster than skills and provide immediate results.

### Available Commands

| Command | Description | Usage |
|---------|-------------|-------|
| `/test-backend` | Run backend tests with pytest | Quick test runs |
| `/test-frontend` | Run frontend tests with Vitest | Quick test runs |
| `/migrate` | Run database migrations | Before starting dev |
| `/dev-start` | Start development environment | Daily startup |
| `/security-check` | Run security audit tools | Pre-commit checks |
| `/deploy-check` | Pre-deployment checklist | Before deployment |
| `/api-docs` | Generate/update API docs | Documentation updates |
| `/code-review` | Review recent changes | Pre-commit review |
| `/quick-fix` | Troubleshoot common issues | When things break |
| `/ui-review` | Review UI for design quality | Design audits |
| `/generate-component` | Generate beautiful React components | Component creation |
| `/design-tokens` | Review/update design system tokens | Design system |

### How to Use Commands

Simply type the slash command in your conversation with Claude:

```
/test-backend
```

Or with context:

```
I just made changes to the auth endpoints. Can you /test-backend and make sure everything still works?
```

## 🤖 When to Use Skills vs Commands

**Use Skills when**:
- Task is complex and multi-step
- Need detailed analysis and recommendations
- Implementing new features
- Learning best practices
- Need comprehensive documentation

**Use Commands when**:
- Quick status checks
- Running standard workflows
- Troubleshooting
- Pre-deployment verification
- Daily development tasks

## 📝 Examples

### Example 1: Testing Workflow

```
Developer: I just added a new webhook endpoint. Can you test it?

Claude: I'll use the api-testing skill to comprehensively test your webhook endpoint.

[Claude uses api-testing skill]
- Tests happy path (valid webhook payload)
- Tests authentication requirements
- Tests signature validation
- Tests error cases (invalid payload, missing fields)
- Tests rate limiting
- Provides coverage report
```

### Example 2: Database Changes

```
Developer: I need to add a new table for tracking API usage analytics

Claude: I'll use the database-migration skill to help you create this migration.

[Claude uses database-migration skill]
1. Creates new SQLAlchemy model
2. Generates Alembic migration
3. Reviews migration for safety
4. Tests upgrade and downgrade
5. Provides migration file and SQL
```

### Example 3: Quick Status Check

```
Developer: /dev-start

Claude: Let me check the status of your development environment...

[Claude runs dev-start command]
✅ Backend: Ready to start (port 8000)
✅ Frontend: Ready to start (port 5173)
✅ PostgreSQL: Running
✅ Redis: Running

To start:
Terminal 1: cd backend && source venv/bin/activate && uvicorn app.main:app --reload
Terminal 2: cd client && npm run dev
```

### Example 4: Pre-deployment Check

```
Developer: /deploy-check

Claude: Running pre-deployment checklist...

[Claude runs deploy-check command]

Backend Checks:
✅ All tests passing
✅ No pending migrations
✅ Environment variables documented
⚠️  DEBUG=True (should be False in production)
❌ CORS origins include "*" (should be explicit list)

Overall Readiness: 70%
Recommendation: Fix critical issues before deploying
```

## 🔧 Customization

### Adding New Skills

1. Create a new markdown file in `.claude/skills/`
2. Follow the template structure:
   - Description
   - When to use
   - Instructions (numbered steps)
   - Code examples
   - Output format

### Adding New Commands

1. Create a new markdown file in `.claude/commands/`
2. Add frontmatter with description:
   ```yaml
   ---
   description: Brief description of what this command does
   ---
   ```
3. Add instructions for Claude to execute

## 🎓 Best Practices

1. **Be specific**: When using skills, provide context about what you're trying to achieve
2. **Use commands for speed**: Commands are faster for routine tasks
3. **Chain workflows**: You can combine multiple commands/skills
4. **Review outputs**: Always review generated code and suggestions
5. **Iterate**: Use feedback from one skill/command to inform the next step

## 📚 Related Documentation

- **CLAUDE.md**: Main AI assistant guide for the project
- **README.md**: User-facing project documentation
- **backend/README.md**: Backend-specific documentation
- **client/README.md**: Frontend-specific documentation

## 🆘 Need Help?

If you're unsure which skill or command to use, just ask Claude:

```
I need to add a new feature that allows users to export their data. What should I use?
```

Claude will recommend the appropriate skills and commands based on your needs.

## 📊 Skill Coverage Matrix

| Area | Skill | Commands |
|------|-------|----------|
| **Backend API** | api-testing | test-backend |
| **Frontend** | frontend-testing | test-frontend |
| **UI/UX Design** | ui-ux-design | ui-review, generate-component, design-tokens |
| **Database** | database-migration | migrate |
| **Security** | security-audit | security-check |
| **Deployment** | deployment | deploy-check, dev-start |
| **General** | - | api-docs, code-review, quick-fix |

---

**Last Updated**: 2025-11-15
**Version**: 1.1.0
**Maintained By**: Claude Code AI Assistant

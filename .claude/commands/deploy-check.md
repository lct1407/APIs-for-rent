---
description: Pre-deployment checklist and readiness check
---

Verify the application is ready for deployment.

Run through the deployment checklist:

## Backend Checks
1. [ ] All tests passing: `cd backend && pytest`
2. [ ] No pending migrations: `alembic current`
3. [ ] Environment variables documented in .env.example
4. [ ] DEBUG=False configured for production
5. [ ] CORS origins properly configured
6. [ ] Secret keys are strong and from environment
7. [ ] Database connection uses SSL
8. [ ] Redis connection configured
9. [ ] Payment provider keys configured
10. [ ] Email SMTP configured

## Frontend Checks
1. [ ] Build succeeds: `cd client && npm run build`
2. [ ] No console.log in production code
3. [ ] API URL points to production
4. [ ] Environment variables configured
5. [ ] Assets optimized
6. [ ] No hardcoded values

## Security Checks
1. [ ] No secrets in git history
2. [ ] Dependencies have no critical vulnerabilities
3. [ ] Rate limiting configured
4. [ ] HTTPS enforced
5. [ ] Security headers configured

## Infrastructure Checks
1. [ ] Database backup strategy in place
2. [ ] Monitoring configured
3. [ ] Logging configured
4. [ ] Health check endpoint working
5. [ ] Rollback procedure documented

Execute checks and provide:
- ✅ Passed checks
- ❌ Failed checks with remediation steps
- ⚠️ Warnings
- Overall readiness score (0-100%)
- Go/No-Go recommendation for deployment

---
description: Run security audit on the codebase
---

Perform a comprehensive security audit using automated tools and manual checks.

Execute the following security scans:

1. **Backend Security**:
   ```bash
   cd backend

   # Check for hardcoded secrets
   grep -r "sk_live" . --exclude-dir=venv
   grep -r "api_key.*=" . --exclude-dir=venv

   # Run Bandit (if installed)
   bandit -r app/ || echo "Install bandit: pip install bandit"

   # Check dependencies
   safety check || echo "Install safety: pip install safety"
   ```

2. **Frontend Security**:
   ```bash
   cd client

   # Check for vulnerable dependencies
   npm audit

   # Check for dangerous patterns
   grep -r "dangerouslySetInnerHTML" src/
   grep -r "eval(" src/
   ```

3. **Configuration Checks**:
   - Verify .env is in .gitignore
   - Check for secrets in git history
   - Verify CORS configuration
   - Check JWT secret configuration

Provide a security report with:
- Critical issues found
- High priority issues
- Recommendations
- Security score (0-100)
- Action items to improve security

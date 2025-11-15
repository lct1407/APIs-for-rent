---
description: Perform code review on recent changes
---

Review recent code changes for quality, security, and best practices.

Check the following:

1. **Get recent changes**:
   ```bash
   git diff main..HEAD
   # or
   git log -1 --stat
   ```

2. **Code Quality Review**:
   - [ ] Follows project conventions (see CLAUDE.md)
   - [ ] Proper TypeScript types (frontend)
   - [ ] Type hints used (Python backend)
   - [ ] No unnecessary complexity
   - [ ] DRY principle followed
   - [ ] Proper error handling
   - [ ] Meaningful variable names

3. **Security Review**:
   - [ ] No hardcoded secrets
   - [ ] Input validation present
   - [ ] SQL injection prevention
   - [ ] XSS prevention
   - [ ] Proper authentication checks
   - [ ] Authorization implemented

4. **Testing Review**:
   - [ ] Tests added for new features
   - [ ] Tests updated for changes
   - [ ] Edge cases covered
   - [ ] Error cases tested

5. **Documentation Review**:
   - [ ] Code comments where needed
   - [ ] JSDoc/docstrings added
   - [ ] README updated if needed
   - [ ] API docs updated

6. **Performance Review**:
   - [ ] No N+1 queries
   - [ ] Proper database indexes
   - [ ] Unnecessary re-renders avoided (React)
   - [ ] Caching utilized where appropriate

Provide:
- Summary of changes reviewed
- Issues found (Critical/High/Medium/Low)
- Specific recommendations
- Approval status (Approve / Request Changes)

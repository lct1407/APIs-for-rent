# Security Audit Skill

**Description**: Perform comprehensive security audits on the rental API platform

**When to use**: When you need to identify security vulnerabilities, check for best practices, or perform security reviews

## Instructions

When invoked, you should perform a comprehensive security audit across multiple areas:

## 1. Authentication & Authorization Audit

### Check JWT Implementation
```bash
cd backend

# Review JWT configuration
grep -r "SECRET_KEY" app/
grep -r "ALGORITHM" app/
grep -r "ACCESS_TOKEN_EXPIRE" app/

# Verify:
# ✓ SECRET_KEY is strong and not hardcoded
# ✓ Token expiration is reasonable (15-30 mins for access, 7 days for refresh)
# ✓ Token blacklisting is implemented
# ✓ Refresh token rotation is enabled
```

**What to look for**:
- [ ] SECRET_KEY is loaded from environment (never hardcoded)
- [ ] SECRET_KEY is at least 32 characters, random
- [ ] Access tokens expire within 30 minutes
- [ ] Refresh tokens have rotation mechanism
- [ ] JWT tokens include proper claims (exp, iat, sub)
- [ ] Token blacklist/revocation is implemented

### Check Password Security
```python
# Review password hashing in app/core/security.py

# Verify:
# ✓ Using bcrypt or argon2 (NOT md5, sha1, sha256)
# ✓ Proper salt generation
# ✓ Cost factor is appropriate (bcrypt: 12+)
```

**What to look for**:
- [ ] Passwords hashed with bcrypt/argon2
- [ ] Salt is unique per password
- [ ] Password validation enforces complexity
- [ ] Passwords never logged or stored in plain text
- [ ] Password reset tokens expire quickly (15-30 mins)

### Check 2FA Implementation
```bash
# Review 2FA implementation
grep -r "totp" app/core/
grep -r "two_factor" app/

# Verify:
# ✓ TOTP secrets properly generated and stored
# ✓ Backup codes are hashed
# ✓ Rate limiting on 2FA verification
```

**What to look for**:
- [ ] TOTP secrets are properly encrypted
- [ ] Backup codes are generated and hashed
- [ ] 2FA verification has rate limiting
- [ ] Recovery mechanism exists for lost 2FA

### Check Authorization
```python
# Review RBAC implementation in app/core/permissions.py

# Verify:
# ✓ Permissions checked on every protected endpoint
# ✓ No privilege escalation vulnerabilities
# ✓ Admin-only endpoints properly protected
```

**What to look for**:
- [ ] Every protected route has permission check
- [ ] Users can't escalate their own privileges
- [ ] Role validation happens server-side, not client-side
- [ ] Admin endpoints require admin role
- [ ] API keys have proper scope restrictions

## 2. Input Validation & Injection Prevention

### SQL Injection Check
```bash
# Search for raw SQL queries
grep -r "execute.*text" app/
grep -r "raw_sql" app/
grep -r "conn.execute" app/

# Verify all use parameterized queries
```

**What to look for**:
- [ ] All queries use SQLAlchemy ORM or parameterized queries
- [ ] No string concatenation in SQL queries
- [ ] User input never directly in SQL
- [ ] Alembic migrations use proper parameterization

### XSS Prevention (Frontend)
```bash
cd client

# Check for dangerous patterns
grep -r "dangerouslySetInnerHTML" src/
grep -r "innerHTML" src/
grep -r "eval(" src/

# Should find ZERO instances
```

**What to look for**:
- [ ] No `dangerouslySetInnerHTML` usage
- [ ] No `eval()` or `Function()` with user input
- [ ] User input sanitized before display
- [ ] CSP headers configured

### Command Injection Check
```bash
# Search for system command execution
grep -r "os.system" app/
grep -r "subprocess" app/
grep -r "exec(" app/
grep -r "eval(" app/

# Should find ZERO instances or verify proper sanitization
```

**What to look for**:
- [ ] No os.system() or subprocess with user input
- [ ] No eval() or exec() with user input
- [ ] File paths validated and sanitized
- [ ] Webhook URLs validated

### API Input Validation
```python
# Review Pydantic schemas in app/schemas/

# Verify:
# ✓ All fields have type validation
# ✓ String fields have max_length
# ✓ Email fields validated
# ✓ URL fields validated
# ✓ Enums used for fixed choices
```

**What to look for**:
- [ ] All API inputs have Pydantic schemas
- [ ] String lengths are limited
- [ ] Emails validated with regex/validator
- [ ] URLs validated before use
- [ ] File uploads have size limits and type checks

## 3. API Security

### Rate Limiting
```bash
# Check rate limiting implementation
grep -r "rate_limit" app/
grep -r "RateLimiter" app/

# Review app/core/middleware.py
```

**What to look for**:
- [ ] Rate limiting on authentication endpoints
- [ ] Per-API-key rate limiting
- [ ] Per-user rate limiting
- [ ] Token bucket algorithm implemented
- [ ] Rate limits stored in Redis
- [ ] 429 responses for exceeded limits

### CORS Configuration
```python
# Review CORS in app/main.py

# Verify:
# ✓ ALLOWED_ORIGINS is not "*" in production
# ✓ Credentials allowed only for trusted origins
# ✓ Methods restricted to needed ones
```

**What to look for**:
- [ ] ALLOWED_ORIGINS is explicit list, not "*"
- [ ] No wildcard origins in production
- [ ] allow_credentials only with specific origins
- [ ] Unnecessary HTTP methods disabled

### API Key Security
```bash
# Review API key implementation
cat app/models/api_key.py
cat app/api/v1/api_keys.py

# Verify:
# ✓ API keys are hashed in database
# ✓ Keys are cryptographically random
# ✓ Keys have scopes/permissions
# ✓ Keys can be revoked
# ✓ Keys have IP whitelist option
```

**What to look for**:
- [ ] API keys hashed before storage (like passwords)
- [ ] Keys generated with secrets.token_urlsafe()
- [ ] Key prefix for identification (sk_)
- [ ] Keys have expiration dates
- [ ] Key rotation supported
- [ ] IP whitelist enforced

## 4. Data Protection

### Sensitive Data Exposure
```bash
# Check for secrets in code
grep -r "sk_live" .
grep -r "api_key.*=" .
grep -r "password.*=" .
grep -r "secret.*=" .

# Should find ZERO hardcoded secrets
```

**What to look for**:
- [ ] No hardcoded API keys
- [ ] No passwords in code
- [ ] No secrets in git history
- [ ] Environment variables for all secrets
- [ ] .env not committed to git
- [ ] Secrets not logged

### Database Security
```python
# Check database configuration
cat backend/app/database.py
cat backend/app/config.py

# Verify:
# ✓ SSL mode enabled for production
# ✓ Connection pooling configured
# ✓ Credentials from environment
```

**What to look for**:
- [ ] Database connections use SSL in production
- [ ] Database credentials from environment
- [ ] Connection pool limits set
- [ ] Database user has minimal permissions
- [ ] Backups configured and tested

### Encryption at Rest
```bash
# Check for encryption of sensitive fields
grep -r "encrypt" app/models/
grep -r "Encrypted" app/

# Verify sensitive fields are encrypted:
# - TOTP secrets
# - Payment data
# - API keys
```

**What to look for**:
- [ ] TOTP secrets encrypted
- [ ] Payment tokens encrypted
- [ ] Webhook secrets hashed
- [ ] API keys hashed
- [ ] PII encrypted if stored

## 5. Dependency Security

### Check for Vulnerable Dependencies
```bash
# Backend
cd backend
pip install safety
safety check

# Check for outdated packages
pip list --outdated

# Frontend
cd ../client
npm audit
npm outdated
```

**What to look for**:
- [ ] No critical vulnerabilities in dependencies
- [ ] Regular dependency updates
- [ ] Automated security scanning (Dependabot, Snyk)
- [ ] Package lock files committed

### Verify Dependency Sources
```bash
# Check requirements.txt for suspicious packages
cat backend/requirements.txt

# Check package.json
cat client/package.json
```

**What to look for**:
- [ ] All packages from trusted sources (PyPI, npm)
- [ ] No typosquatting packages
- [ ] Version pinning in production
- [ ] Hash checking for packages

## 6. Error Handling & Logging

### Error Exposure
```python
# Check error handling
grep -r "raise.*Exception" app/api/
grep -r "DEBUG" app/

# Verify:
# ✓ DEBUG=False in production
# ✓ Generic error messages to users
# ✓ Detailed errors only in logs
```

**What to look for**:
- [ ] DEBUG mode disabled in production
- [ ] Error messages don't expose stack traces
- [ ] Error messages don't reveal system info
- [ ] Sensitive data not in error messages
- [ ] 500 errors return generic message

### Logging Security
```bash
# Check logging configuration
grep -r "logger" app/
cat app/core/logging.py  # if exists

# Verify logs don't contain:
# - Passwords
# - API keys
# - Credit card numbers
# - Personal data (unless necessary)
```

**What to look for**:
- [ ] Passwords never logged
- [ ] API keys never logged
- [ ] Credit card numbers never logged
- [ ] Sensitive fields masked in logs
- [ ] Logs have proper retention policy
- [ ] Log access is restricted

## 7. Session & Cookie Security

### Cookie Configuration
```python
# Review cookie settings in app/main.py and app/core/security.py

# Verify:
# ✓ HttpOnly flag set
# ✓ Secure flag set (HTTPS only)
# ✓ SameSite attribute set
```

**What to look for**:
- [ ] Cookies have HttpOnly flag
- [ ] Cookies have Secure flag in production
- [ ] SameSite=Lax or Strict
- [ ] Session cookies expire
- [ ] CSRF protection implemented

## 8. File Upload Security

### File Upload Validation
```bash
# Search for file upload endpoints
grep -r "UploadFile" app/
grep -r "File(" app/

# Check validation
```

**What to look for**:
- [ ] File size limits enforced
- [ ] File type validation (not just extension)
- [ ] Uploaded files scanned for malware
- [ ] Files stored outside web root
- [ ] Unique filenames to prevent overwrite
- [ ] No script execution in upload directory

## 9. WebSocket Security

### WebSocket Authentication
```python
# Review WebSocket implementation
cat app/websocket/manager.py
cat app/api/v1/websocket.py

# Verify:
# ✓ Authentication required
# ✓ Authorization per channel
# ✓ Rate limiting
```

**What to look for**:
- [ ] WebSocket connections require authentication
- [ ] JWT tokens validated for WS
- [ ] Users can only access authorized channels
- [ ] Message size limits
- [ ] Rate limiting on messages

## 10. Payment Security

### Payment Data Handling
```bash
# Check payment implementation
grep -r "stripe" app/services/
grep -r "paypal" app/services/
grep -r "card_number" app/

# Should NEVER store full card numbers
```

**What to look for**:
- [ ] No storage of full credit card numbers
- [ ] No storage of CVV codes
- [ ] Using Stripe/PayPal tokenization
- [ ] PCI DSS compliance measures
- [ ] Payment webhooks verified
- [ ] Webhook signatures validated

## Security Audit Checklist

### Critical (Must Fix Immediately)
- [ ] SQL injection vulnerabilities
- [ ] XSS vulnerabilities
- [ ] Command injection vulnerabilities
- [ ] Hardcoded secrets
- [ ] Authentication bypass
- [ ] Authorization bypass
- [ ] Sensitive data exposure

### High Priority (Fix Within Days)
- [ ] Missing rate limiting
- [ ] Weak password requirements
- [ ] Missing 2FA
- [ ] Vulnerable dependencies
- [ ] Missing input validation
- [ ] Improper error handling
- [ ] Missing CSRF protection

### Medium Priority (Fix Within Weeks)
- [ ] Missing security headers
- [ ] Weak session configuration
- [ ] Missing audit logging
- [ ] Suboptimal CORS configuration
- [ ] Missing API key rotation
- [ ] Insufficient monitoring

### Low Priority (Improvements)
- [ ] Security documentation
- [ ] Security testing automation
- [ ] Additional encryption
- [ ] Enhanced monitoring
- [ ] Security training

## Automated Security Tools

Run these tools for automated security scanning:

```bash
# Backend
cd backend

# Bandit - Python security linter
pip install bandit
bandit -r app/

# Safety - dependency vulnerability scanner
pip install safety
safety check

# Semgrep - static analysis
pip install semgrep
semgrep --config=auto app/

# Frontend
cd ../client

# npm audit - dependency scanner
npm audit

# ESLint security plugin
npm install --save-dev eslint-plugin-security
# Add to eslint.config.js
```

## Manual Security Testing

### Test Authentication
```bash
# Test with invalid token
curl -H "Authorization: Bearer invalid_token" \
  http://localhost:8000/api/v1/users/me

# Test without token
curl http://localhost:8000/api/v1/users/me

# Test with expired token
# (create expired token and test)

# Test token in wrong endpoint
# (use user token on admin endpoint)
```

### Test Authorization
```bash
# Test privilege escalation
# (user trying to access admin endpoints)

# Test horizontal privilege escalation
# (user A accessing user B's data)

# Test role manipulation
# (user trying to change own role)
```

### Test Input Validation
```bash
# Test SQL injection
curl -X POST http://localhost:8000/api/v1/items \
  -d '{"name": "'; DROP TABLE users; --"}'

# Test XSS
curl -X POST http://localhost:8000/api/v1/items \
  -d '{"name": "<script>alert(1)</script>"}'

# Test oversized input
curl -X POST http://localhost:8000/api/v1/items \
  -d '{"name": "'$(python -c 'print("A"*10000))')"}'
```

## Output

Provide a comprehensive security report with:

1. **Executive Summary**:
   - Overall security posture
   - Critical issues count
   - Risk level assessment

2. **Detailed Findings**:
   - Issue description
   - Severity (Critical/High/Medium/Low)
   - Location in code
   - Proof of concept (if applicable)
   - Remediation steps

3. **Compliance Status**:
   - OWASP Top 10 compliance
   - PCI DSS compliance (if handling payments)
   - GDPR compliance (if handling EU data)

4. **Recommendations**:
   - Immediate action items
   - Security improvements
   - Best practices to implement

5. **Security Score**:
   - Overall score (0-100)
   - Breakdown by category

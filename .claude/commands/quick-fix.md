---
description: Quick troubleshooting for common issues
---

Diagnose and fix common development issues.

Run diagnostics and provide solutions:

## 1. Check Services Status

```bash
# Backend running?
curl http://localhost:8000/health 2>/dev/null || echo "❌ Backend not running"

# Frontend running?
curl http://localhost:5173 2>/dev/null || echo "❌ Frontend not running"

# PostgreSQL running?
pg_isready 2>/dev/null || echo "❌ PostgreSQL not running"

# Redis running?
redis-cli ping 2>/dev/null || echo "❌ Redis not running"
```

## 2. Check Dependencies

```bash
# Backend dependencies
cd backend
if [ ! -d "venv" ]; then
  echo "❌ Virtual environment not found"
else
  source venv/bin/activate
  pip check || echo "⚠️  Dependency issues"
fi

# Frontend dependencies
cd ../client
if [ ! -d "node_modules" ]; then
  echo "❌ node_modules not found"
else
  npm ls 2>&1 | grep -i "missing" && echo "⚠️  Missing dependencies"
fi
```

## 3. Check Environment Variables

```bash
# Backend .env
if [ ! -f "backend/.env" ]; then
  echo "❌ backend/.env not found"
  echo "💡 Copy from .env.example: cp backend/.env.example backend/.env"
fi

# Frontend .env
if [ ! -f "client/.env" ]; then
  echo "⚠️  client/.env not found (optional)"
fi
```

## 4. Common Issues & Fixes

### Issue: Import errors
**Fix**:
```bash
cd backend && pip install -r requirements.txt
cd client && npm install
```

### Issue: Database connection errors
**Fix**:
```bash
# Check DATABASE_URL in .env
# Verify PostgreSQL is running: systemctl status postgresql
# Test connection: psql $DATABASE_URL -c "SELECT 1"
```

### Issue: Migration errors
**Fix**:
```bash
cd backend
alembic current  # Check current version
alembic upgrade head  # Run migrations
# If issues: alembic downgrade -1 && alembic upgrade head
```

### Issue: Port already in use
**Fix**:
```bash
# Backend (port 8000)
lsof -ti:8000 | xargs kill -9

# Frontend (port 5173)
lsof -ti:5173 | xargs kill -9
```

### Issue: CORS errors
**Fix**:
- Check ALLOWED_ORIGINS in backend/.env
- Verify frontend URL is in the list
- Restart backend server

### Issue: Authentication not working
**Fix**:
- Check SECRET_KEY in backend/.env
- Verify JWT token format
- Check token expiration
- Clear localStorage and re-login

## 5. Reset Everything (Nuclear Option)

```bash
# Stop all services
# Kill processes on ports 8000, 5173

# Backend reset
cd backend
deactivate  # Exit venv
rm -rf venv
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
alembic upgrade head

# Frontend reset
cd ../client
rm -rf node_modules package-lock.json
npm install

# Database reset (⚠️ DESTRUCTIVE)
# dropdb rentapi && createdb rentapi
# cd backend && alembic upgrade head
# python scripts/seed_data.py
```

Provide:
- Diagnostic results
- Issues found
- Fix commands executed
- Status after fixes
- Next steps if issues persist

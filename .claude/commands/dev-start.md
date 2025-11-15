---
description: Start the development environment (backend + frontend)
---

Start both the backend and frontend development servers.

Provide instructions or execute:

1. **Backend**:
   - Navigate to backend directory
   - Check if virtual environment exists
   - Activate venv if exists, otherwise suggest creating one
   - Show command: `uvicorn app.main:app --reload --host 0.0.0.0 --port 8000`

2. **Frontend**:
   - Navigate to client directory
   - Check if node_modules exists
   - Show command: `npm run dev`

3. **Optional services** (if needed):
   - PostgreSQL: Check if running
   - Redis: Check if running
   - Celery worker: `celery -A app.core.celery_app worker --loglevel=info`
   - Celery beat: `celery -A app.core.celery_app beat --loglevel=info`

Provide:
- Status of all services
- URLs to access:
  - Backend API: http://localhost:8000
  - API Docs: http://localhost:8000/docs
  - Frontend: http://localhost:5173
- Any missing dependencies or configuration
- Instructions to start each service

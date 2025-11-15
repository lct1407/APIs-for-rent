# Deployment Skill

**Description**: Deploy the rental API platform to production environments

**When to use**: When you need to deploy to staging/production, set up infrastructure, or configure deployment pipelines

## Instructions

When invoked, you should:

1. **Pre-deployment checklist**:

   **Backend**:
   - [ ] All tests passing (`pytest`)
   - [ ] Database migrations ready (`alembic upgrade head`)
   - [ ] Environment variables configured
   - [ ] SECRET_KEY is strong and unique
   - [ ] DEBUG=False in production
   - [ ] CORS origins properly configured
   - [ ] Payment provider keys configured (Stripe, PayPal)
   - [ ] Email SMTP configured
   - [ ] Redis connection configured
   - [ ] PostgreSQL connection configured

   **Frontend**:
   - [ ] Build succeeds (`npm run build`)
   - [ ] Environment variables set (VITE_API_URL)
   - [ ] API endpoints point to production
   - [ ] No console.log statements in production
   - [ ] Assets optimized

2. **Deployment options**:

   ### Option A: Docker Deployment

   **Backend Dockerfile** (`backend/Dockerfile`):
   ```dockerfile
   FROM python:3.11-slim

   WORKDIR /app

   # Install system dependencies
   RUN apt-get update && apt-get install -y \
       postgresql-client \
       && rm -rf /var/lib/apt/lists/*

   # Install Python dependencies
   COPY requirements.txt .
   RUN pip install --no-cache-dir -r requirements.txt

   # Copy application code
   COPY . .

   # Run migrations and start server
   CMD alembic upgrade head && \
       uvicorn app.main:app --host 0.0.0.0 --port 8000
   ```

   **Frontend Dockerfile** (`client/Dockerfile`):
   ```dockerfile
   FROM node:18-alpine AS builder

   WORKDIR /app

   COPY package*.json ./
   RUN npm ci

   COPY . .
   RUN npm run build

   FROM nginx:alpine

   COPY --from=builder /app/dist /usr/share/nginx/html
   COPY nginx.conf /etc/nginx/conf.d/default.conf

   EXPOSE 80

   CMD ["nginx", "-g", "daemon off;"]
   ```

   **docker-compose.yml**:
   ```yaml
   version: '3.8'

   services:
     postgres:
       image: postgres:15
       environment:
         POSTGRES_DB: rentapi
         POSTGRES_USER: rentapi
         POSTGRES_PASSWORD: ${DB_PASSWORD}
       volumes:
         - postgres_data:/var/lib/postgresql/data
       ports:
         - "5432:5432"

     redis:
       image: redis:7-alpine
       ports:
         - "6379:6379"
       volumes:
         - redis_data:/data

     backend:
       build: ./backend
       ports:
         - "8000:8000"
       environment:
         DATABASE_URL: postgresql+asyncpg://rentapi:${DB_PASSWORD}@postgres:5432/rentapi
         REDIS_URL: redis://redis:6379/0
         SECRET_KEY: ${SECRET_KEY}
         STRIPE_SECRET_KEY: ${STRIPE_SECRET_KEY}
         PAYPAL_CLIENT_ID: ${PAYPAL_CLIENT_ID}
       depends_on:
         - postgres
         - redis

     celery_worker:
       build: ./backend
       command: celery -A app.core.celery_app worker --loglevel=info
       environment:
         DATABASE_URL: postgresql+asyncpg://rentapi:${DB_PASSWORD}@postgres:5432/rentapi
         REDIS_URL: redis://redis:6379/0
         CELERY_BROKER_URL: redis://redis:6379/1
       depends_on:
         - postgres
         - redis

     celery_beat:
       build: ./backend
       command: celery -A app.core.celery_app beat --loglevel=info
       environment:
         DATABASE_URL: postgresql+asyncpg://rentapi:${DB_PASSWORD}@postgres:5432/rentapi
         REDIS_URL: redis://redis:6379/0
         CELERY_BROKER_URL: redis://redis:6379/1
       depends_on:
         - postgres
         - redis

     frontend:
       build: ./client
       ports:
         - "80:80"
       depends_on:
         - backend

   volumes:
     postgres_data:
     redis_data:
   ```

   **Deploy with Docker**:
   ```bash
   # Build and start services
   docker-compose up -d

   # Check logs
   docker-compose logs -f backend

   # Run migrations
   docker-compose exec backend alembic upgrade head

   # Seed data (optional)
   docker-compose exec backend python scripts/seed_data.py
   ```

   ### Option B: Platform as a Service (Render, Railway, Fly.io)

   **Render deployment**:

   1. Create `render.yaml`:
   ```yaml
   services:
     - type: web
       name: rentapi-backend
       env: python
       buildCommand: pip install -r requirements.txt
       startCommand: |
         alembic upgrade head &&
         uvicorn app.main:app --host 0.0.0.0 --port $PORT
       envVars:
         - key: DATABASE_URL
           fromDatabase:
             name: rentapi-db
             property: connectionString
         - key: REDIS_URL
           fromDatabase:
             name: rentapi-redis
             property: connectionString
         - key: SECRET_KEY
           generateValue: true
         - key: PYTHON_VERSION
           value: 3.11.0

     - type: web
       name: rentapi-frontend
       env: static
       buildCommand: cd client && npm install && npm run build
       staticPublishPath: client/dist
       routes:
         - type: rewrite
           source: /*
           destination: /index.html

     - type: worker
       name: celery-worker
       env: python
       buildCommand: pip install -r requirements.txt
       startCommand: celery -A app.core.celery_app worker --loglevel=info

     - type: worker
       name: celery-beat
       env: python
       buildCommand: pip install -r requirements.txt
       startCommand: celery -A app.core.celery_app beat --loglevel=info

   databases:
     - name: rentapi-db
       plan: starter
       databaseName: rentapi
       user: rentapi

     - name: rentapi-redis
       plan: starter
   ```

   2. Deploy:
   ```bash
   # Connect to Render
   render login

   # Deploy
   render up
   ```

   ### Option C: VPS (DigitalOcean, AWS EC2, Linode)

   **Server setup**:
   ```bash
   # Update system
   sudo apt update && sudo apt upgrade -y

   # Install dependencies
   sudo apt install -y python3.11 python3-pip postgresql redis-server nginx

   # Install Node.js
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt install -y nodejs

   # Clone repository
   git clone <repo-url> /var/www/rentapi
   cd /var/www/rentapi

   # Backend setup
   cd backend
   python3.11 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt

   # Run migrations
   alembic upgrade head

   # Frontend setup
   cd ../client
   npm install
   npm run build

   # Set up systemd service for backend
   sudo nano /etc/systemd/system/rentapi.service
   ```

   **systemd service** (`/etc/systemd/system/rentapi.service`):
   ```ini
   [Unit]
   Description=RentAPI FastAPI Application
   After=network.target

   [Service]
   User=www-data
   WorkingDirectory=/var/www/rentapi/backend
   Environment="PATH=/var/www/rentapi/backend/venv/bin"
   EnvironmentFile=/var/www/rentapi/backend/.env
   ExecStart=/var/www/rentapi/backend/venv/bin/uvicorn app.main:app --host 0.0.0.0 --port 8000
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

   **Nginx configuration** (`/etc/nginx/sites-available/rentapi`):
   ```nginx
   server {
       listen 80;
       server_name your-domain.com;

       # Frontend
       location / {
           root /var/www/rentapi/client/dist;
           try_files $uri $uri/ /index.html;
       }

       # Backend API
       location /api/ {
           proxy_pass http://127.0.0.1:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }

       # WebSocket
       location /api/v1/ws/ {
           proxy_pass http://127.0.0.1:8000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection "upgrade";
       }
   }
   ```

   **Enable and start services**:
   ```bash
   # Enable services
   sudo systemctl enable rentapi
   sudo systemctl start rentapi

   # Enable nginx
   sudo ln -s /etc/nginx/sites-available/rentapi /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl reload nginx

   # Set up SSL with Let's Encrypt
   sudo apt install certbot python3-certbot-nginx
   sudo certbot --nginx -d your-domain.com
   ```

3. **Environment variables setup**:

   Create production `.env` files:

   **Backend `.env`**:
   ```bash
   # Database
   DATABASE_URL=postgresql+asyncpg://user:pass@host:5432/dbname

   # Redis
   REDIS_URL=redis://host:6379/0

   # Security
   SECRET_KEY=<generate-strong-random-key>
   ALGORITHM=HS256
   ACCESS_TOKEN_EXPIRE_MINUTES=30
   DEBUG=False

   # CORS
   ALLOWED_ORIGINS=https://yourdomain.com

   # Payment
   STRIPE_SECRET_KEY=sk_live_...
   STRIPE_PUBLISHABLE_KEY=pk_live_...
   PAYPAL_CLIENT_ID=...
   PAYPAL_CLIENT_SECRET=...

   # Email
   MAIL_SERVER=smtp.sendgrid.net
   MAIL_PORT=587
   MAIL_USERNAME=apikey
   MAIL_PASSWORD=<sendgrid-api-key>

   # Celery
   CELERY_BROKER_URL=redis://host:6379/1
   CELERY_RESULT_BACKEND=redis://host:6379/2
   ```

   **Frontend `.env.production`**:
   ```bash
   VITE_API_URL=https://api.yourdomain.com
   ```

4. **Database backup strategy**:

   **Automated backups**:
   ```bash
   # Create backup script
   cat > /usr/local/bin/backup-db.sh << 'EOF'
   #!/bin/bash
   BACKUP_DIR=/var/backups/rentapi
   DATE=$(date +%Y%m%d_%H%M%S)

   mkdir -p $BACKUP_DIR

   # Backup PostgreSQL
   pg_dump -U rentapi rentapi | gzip > $BACKUP_DIR/rentapi_$DATE.sql.gz

   # Keep only last 7 days
   find $BACKUP_DIR -name "*.sql.gz" -mtime +7 -delete
   EOF

   chmod +x /usr/local/bin/backup-db.sh

   # Add to crontab (daily at 2 AM)
   echo "0 2 * * * /usr/local/bin/backup-db.sh" | sudo crontab -
   ```

5. **Monitoring and logging**:

   **Set up logging**:
   ```bash
   # Backend logs
   sudo journalctl -u rentapi -f

   # Nginx logs
   sudo tail -f /var/log/nginx/access.log
   sudo tail -f /var/log/nginx/error.log

   # Application logs
   tail -f /var/www/rentapi/backend/logs/app.log
   ```

   **Health check endpoint**:
   ```bash
   # Test health
   curl https://your-domain.com/health

   # Set up monitoring with UptimeRobot or similar
   ```

6. **Zero-downtime deployment**:

   ```bash
   #!/bin/bash
   # deploy.sh

   cd /var/www/rentapi

   # Pull latest code
   git pull origin main

   # Backend
   cd backend
   source venv/bin/activate
   pip install -r requirements.txt
   alembic upgrade head

   # Reload without downtime
   sudo systemctl reload rentapi

   # Frontend
   cd ../client
   npm install
   npm run build

   # Reload nginx
   sudo nginx -t && sudo systemctl reload nginx

   echo "Deployment complete!"
   ```

## Post-deployment verification

1. **Check services**:
   ```bash
   # Backend health
   curl https://your-domain.com/health

   # API docs
   curl https://your-domain.com/docs

   # Test authentication
   curl -X POST https://your-domain.com/api/v1/auth/login \
     -H "Content-Type: application/json" \
     -d '{"email":"admin@example.com","password":"Admin123!@#"}'
   ```

2. **Monitor logs**:
   ```bash
   # Check for errors
   sudo journalctl -u rentapi --since "10 minutes ago"

   # Check Celery workers
   celery -A app.core.celery_app inspect active
   ```

3. **Performance testing**:
   ```bash
   # Load test with Apache Bench
   ab -n 1000 -c 10 https://your-domain.com/api/v1/health
   ```

## Rollback procedure

If deployment fails:

```bash
# Rollback git
git revert HEAD
git push

# Rollback database
alembic downgrade -1

# Restart services
sudo systemctl restart rentapi
```

## Output

Provide:
1. Deployment method used
2. All services deployed and their URLs
3. Health check results
4. Any warnings or issues encountered
5. Post-deployment verification steps
6. Rollback instructions if needed

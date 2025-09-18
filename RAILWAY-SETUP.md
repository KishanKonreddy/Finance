`DEPLOYMENT.md` file:

````markdown
# 🚄 Railway Deployment Guide  

## Steps to deploy on Railway  

### 1. Create a project on Railway  
- Go to [Railway](https://railway.app)  
- Create a new app from GitHub  
- Select this repository  

### 2. Configure Environment Variables  
In Railway, add the following environment variables:  

#### Required Variables:  
```env
# Database (Railway PostgreSQL)
DATABASE_URL=postgresql://username:password@host:port/database

# OpenAI (REQUIRED)
OPENAI_API_KEY=sk-your-openai-api-key-here

# Twilio WhatsApp API
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886

# Stripe
STRIPE_SECRET_KEY=sk_live_your_stripe_secret_key
STRIPE_PUBLISHABLE_KEY=pk_live_your_stripe_publishable_key
STRIPE_WEBHOOK_SECRET=whsec_your_webhook_secret

# JWT
JWT_SECRET_KEY=your-super-secret-jwt-key-here

# Railway specific
PORT=8000
RAILWAY_ENVIRONMENT=production
````

### 3. Add PostgreSQL Database

* In Railway, click **Add Service**
* Select **PostgreSQL**
* Railway will automatically generate the `DATABASE_URL`

### 4. Build Configuration

Railway will automatically detect and use:

* `Dockerfile` → for multi-stage build configuration
* `Procfile` → as a fallback start command
* `railway.json` → for additional configurations

### 5. Domains and URLs

* Railway will assign a default `.railway.app` domain
* You can configure a custom domain in the settings

---

## Deployment Architecture

```
Railway App
├── Backend (FastAPI) - Port 8000
├── Frontend (Static files) - Served by FastAPI
├── PostgreSQL - Database
└── Environment Variables
```

---

## File Structure for Railway

```
├── nixpacks.toml          # Build configuration
├── Procfile               # Start command
├── railway.json           # Railway config
├── backend/
│   ├── requirements.txt   # Python dependencies
│   └── railway_start.py   # Startup script
└── frontend/
    ├── package.json       # Node.js dependencies
    └── dist/              # Static build (generated)
```

---

## Troubleshooting

### Error: "Nixpacks build failed"

* Check that `nixpacks.toml` exists at the project root
* Verify dependencies are correct

### Error: "Frontend not loading"

* Check that the frontend build completed successfully
* Verify routes in `railway_start.py`

### Error: "Database connection"

* Verify `DATABASE_URL`
* Ensure PostgreSQL service is active

---

## URLs after deployment

* **App**: `https://your-app.railway.app`
* **API Docs**: `https://your-app.railway.app/docs` (FastAPI Swagger)
* **Health Check**: `https://your-app.railway.app/health`



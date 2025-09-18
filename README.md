
# 📱 Finance

Personal finance management via **WhatsApp**, built with **FastAPI, React, PostgreSQL, CrewAI, Twilio WhatsApp API, and Stripe**.  

---

## 🚀 Features  

### 🔹 Backend (FastAPI + PostgreSQL)  
- RESTful API with FastAPI  
- PostgreSQL with SQLAlchemy + Alembic migrations  
- Twilio WhatsApp webhook for message processing  
- CrewAI agents for parsing, categorization & financial advice  
- Stripe integration for premium plans ($5/month)  
- Automatic weekly & monthly reports  
- OTP authentication via WhatsApp  

### 🔹 Frontend (React + TypeScript + Tailwind)  
- Responsive dashboard with financial summary  
- Interactive charts (expenses by category)  
- OTP login via WhatsApp  
- Subscription management with Stripe Checkout  
- Filterable transaction list  
- Premium automated reports  

### 🔹 Plans  
- **Free** → 50 transactions/month  
- **Premium ($5/month)** → Unlimited transactions + auto reports  

---

## 📋 Prerequisites  
- Docker & Docker Compose  
- Node.js 18+ (local dev)  
- Python 3.11+ (local dev)  
- Accounts:  
  - Twilio (WhatsApp API)  
  - Stripe (payments)  
  - OpenAI (CrewAI)  

---

## ⚙️ Setup  

### 1. Clone repo  
```bash
git clone <repository-url>
cd control-finances
````

### 2. Configure `.env`

```bash
cp .env.example .env
```

Fill with your credentials:

```env
DATABASE_URL=postgresql://finances_user:finances_password@postgres:5432/finances_db
TWILIO_ACCOUNT_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886
STRIPE_SECRET_KEY=sk_test_key
STRIPE_PUBLISHABLE_KEY=pk_test_key
STRIPE_WEBHOOK_SECRET=whsec_secret
JWT_SECRET_KEY=super-secret-key
OPENAI_API_KEY=sk-your-api-key
```

### 3. Run with Docker

```bash
docker-compose up --build
# or in background
docker-compose up -d --build
```

---

## 🔄 Database Migrations

```bash
cd backend
alembic revision --autogenerate -m "migration description"
alembic upgrade head
```

---

## 📱 Usage

### Register via WhatsApp OTP

1. Open frontend → `http://localhost:3000`
2. Enter phone number
3. Receive OTP in WhatsApp
4. Verify OTP to login

### Record transactions in WhatsApp

```
Spent ₡5000 on lunch
₡10000 gas
Received ₡50000 salary
Income ₡25000 project
```

### Dashboard

* Balance, income, expenses
* Transaction filters
* Premium reports
* Subscription management

### Auto Reports (Premium)

* Weekly → Sunday 8 PM
* Monthly → 1st of month 9 AM

---

## 🧪 Testing

**Backend**

```bash
cd backend
pytest
```

**Frontend**

```bash
cd frontend
npm test
```

---

## 📊 API Endpoints

**Users**

* `POST /users/` → Create user
* `GET /users/{id}` → Get user
* `PUT /users/{id}` → Update user

**Transactions**

* `POST /transactions/` → Create
* `GET /transactions/user/{id}` → List
* `GET /transactions/user/{id}/balance` → Balance
* `GET /transactions/user/{id}/expenses-by-category` → Expenses by category

**WhatsApp**

* `POST /whatsapp/webhook` → Twilio webhook
* `POST /whatsapp/send-otp` → Send OTP
* `POST /whatsapp/verify-otp` → Verify OTP

**Reports**

* `GET /reports/user/{id}` → List reports
* `POST /reports/generate/weekly/{id}` → Weekly report
* `POST /reports/generate/monthly/{id}` → Monthly report

**Stripe**

* `POST /stripe/create-checkout-session` → Checkout
* `POST /stripe/webhook` → Webhook
* `GET /stripe/subscription-status/{id}` → Subscription status

---

## 🤖 CrewAI Agents

* **ParserAgent** → Extracts amount, type & description
* **CategorizerAgent** → Auto-categorizes expenses/income
* **AdvisorAgent** → Generates financial advice

---

## 📅 Scheduler Jobs

* Weekly reports → Sunday 8 PM
* Monthly reports → 1st of month 9 AM
* OTP cleanup → Hourly

---

## 🏗️ Project Structure

```
control-finances/
├── backend/
│   ├── app/
│   │   ├── agents/      # CrewAI agents
│   │   ├── core/        # Config & schemas
│   │   ├── models/      # DB models
│   │   ├── routers/     # API routes
│   │   ├── services/    # Business logic
│   │   └── main.py      # FastAPI app
│   ├── alembic/         # Migrations
│   ├── Dockerfile
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── components/  # React components
│   │   ├── pages/       # Pages
│   │   ├── utils/       # Helpers/API
│   │   └── App.tsx
│   ├── public/
│   ├── Dockerfile
│   └── package.json
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## 🚀 Deployment

### Production env

```env
DATABASE_URL=postgresql://user:password@host:5432/db
TWILIO_WHATSAPP_NUMBER=whatsapp:+1234567890
# ... etc
```

### Build

```bash
docker build -t finances-backend ./backend
docker build -t finances-frontend ./frontend
```

### Deploy

```bash
docker-compose -f docker-compose.prod.yml up -d
```

---

## 🔧 Troubleshooting

**Database connection failed**

```bash
docker-compose ps
docker-compose logs postgres
```

**Twilio webhook not working**

```bash
ngrok http 8000   # expose backend to internet
```

**CrewAI agents not working**

```bash
echo $OPENAI_API_KEY
docker-compose logs backend
```

---

## 📝 Notes

* TypeScript frontend
* Async SQLAlchemy skipped (MVP simplification)
* Redis → for OTP improvements
* Celery → for advanced async tasks
* Tests → extend with more scenarios

---

## 🤝 Contributing

1. Fork this repo
2. Create feature branch → `git checkout -b feature/NewFeature`
3. Commit → `git commit -m "Add NewFeature"`
4. Push → `git push origin feature/NewFeature`
5. Open Pull Request

---


✅ **MVP ready to use!**
Set up Twilio, Stripe, and OpenAI → then run:

```bash
docker-compose up --build
```



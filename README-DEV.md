
# 🚀 Development Guide  

## Commands for Development with Hot Reload  

### Option 1: Automatic Script  
```bash
./dev-start.sh
````

### Option 2: Direct Command

```bash
docker-compose -f docker-compose.dev.yml up --build
```

### Option 3: Individual Services

```bash
# Backend + Database only
docker-compose -f docker-compose.dev.yml up postgres backend

# Frontend only
docker-compose -f docker-compose.dev.yml up frontend

# Rebuild frontend only
docker-compose -f docker-compose.dev.yml up --build frontend
```

---

## Development URLs

* **Frontend**: [http://localhost:5173](http://localhost:5173) (Vite dev server with HMR)
* **Backend**: [http://localhost:8000](http://localhost:8000) (FastAPI with auto-reload)
* **Database**: localhost:5432

---

## Development Environment Features

✅ **Frontend Hot Reload**: Changes in `src/` are applied automatically
✅ **Backend Hot Reload**: Python code reloads automatically
✅ **Vite HMR**: Hot Module Replacement for React
✅ **TypeScript**: Real-time compilation
✅ **Tailwind CSS**: Automatic style reload
✅ **shadcn/ui**: Ready-to-use components

---

## Watched File Structure

### Frontend (Hot Reload)

```
frontend/
├── src/               # ← Watched
├── public/            # ← Watched
├── index.html         # ← Watched
├── vite.config.ts     # ← Watched
├── tailwind.config.js # ← Watched
└── tsconfig*.json     # ← Watched
```

### Backend (Hot Reload)

```
backend/
└── app/               # ← Watched (entire directory)
```

---

## Environment Variables

Copy `.env.example` to `.env` and configure:

```bash
cp .env.example .env
```

---

## Useful Commands

```bash
# View logs in real time
docker-compose -f docker-compose.dev.yml logs -f

# Full rebuild
docker-compose -f docker-compose.dev.yml up --build --force-recreate

# Stop all containers
docker-compose -f docker-compose.dev.yml down

# Clean volumes
docker-compose -f docker-compose.dev.yml down -v
```

---

## For Production

Use the original file:

```bash
docker-compose up --build
```

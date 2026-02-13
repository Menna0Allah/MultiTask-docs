# Quickstart

This quickstart is sanitized for public sharing and focused on local development.

## Prerequisites

- Python 3.11+
- Node.js 18+
- PostgreSQL
- Git

## 1) Clone Repository

```bash
git clone <your-private-multitask-repo>
cd <repo-root>
```

## 2) Backend Setup

```bash
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
python manage.py migrate
python manage.py runserver
```

Expected API base: `http://127.0.0.1:8000/api`

## 3) Frontend Setup

```bash
cd frontend
npm install
copy .env.example .env
npm run dev
```

Expected frontend URL: `http://127.0.0.1:5173` (or Vite-assigned local URL).

## 4) Environment Variables

### Frontend `.env.example`

```env
VITE_API_URL=http://127.0.0.1:8000/api
VITE_WS_URL=ws://127.0.0.1:8000/ws
VITE_APP_NAME=Multitask
VITE_MEDIA_URL=http://127.0.0.1:8000/media
VITE_GOOGLE_CLIENT_ID=your_google_client_id
VITE_STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key
```

### Backend `.env.example`

```env
DEBUG=True
SECRET_KEY=replace_with_local_secret
DATABASE_URL=postgres://user:pass@localhost:5432/multitask
STRIPE_SECRET_KEY=replace_with_stripe_secret
STRIPE_WEBHOOK_SECRET=replace_with_webhook_secret
GOOGLE_GEMINI_API_KEY=replace_with_gemini_key
EMAIL_HOST=smtp.gmail.com
EMAIL_HOST_USER=your_email
EMAIL_HOST_PASSWORD=your_app_password
```

## 5) Smoke Test Checklist

1. Register a new user and verify login works.
2. Browse `/tasks` and open a task detail page.
3. Open `/dashboard` after authentication.
4. Test messaging and notification visibility.
5. Confirm wallet/transactions pages load for authenticated users.

## Common Setup Issues

- Database connection errors: confirm `DATABASE_URL` and local PostgreSQL service.
- Token/auth issues: check frontend API URL and backend CORS/JWT config.
- WebSocket failures: verify `VITE_WS_URL` and running Channels service.

## UI Verification

| Milestone | Preview |
|---|---|
| Landing page loaded | ![Home](../assets/screenshots/start-hero-page.png) |
| Login available | ![Login](../assets/screenshots/login-page.png) |
| Dashboard accessible | ![Dashboard](../assets/screenshots/dashboard-page.png) |

## Public Documentation Rule

- Keep placeholders and examples only.
- Never commit production credentials or private tokens.

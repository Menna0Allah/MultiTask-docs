# Quickstart

This quickstart is sanitized for public sharing and local development.

## Prerequisites
- Python 3.11+
- Node.js 18+
- PostgreSQL
- Git

## 1) Clone and Prepare
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

## 3) Frontend Setup
```bash
cd frontend
npm install
copy .env.example .env
npm run dev
```

## 4) Required Environment Variables
Frontend `.env.example`:
```env
VITE_API_URL=http://127.0.0.1:8000/api
VITE_WS_URL=ws://127.0.0.1:8000/ws
VITE_APP_NAME=Multitask
VITE_MEDIA_URL=http://127.0.0.1:8000/media
VITE_GOOGLE_CLIENT_ID=your_google_client_id
VITE_STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key
```

Backend `.env.example`:
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

## Public Docs Rule
- Keep only sample keys and placeholder values in this documentation repo.
- Never commit production credentials.

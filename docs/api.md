# API

Base URL: `http://localhost:8000/api`

This page documents the public backend surface by domain. It mirrors the canonical inventory in `DOCUMENTATION.md`.

## Auth
Purpose: identity, session lifecycle, and profile management.

Main endpoints:
- `POST /auth/register/`
- `POST /auth/login/`
- `POST /auth/token/refresh/`
- `POST /auth/logout/`
- `GET|PUT /auth/profile/`
Additional endpoints:
- `POST /auth/token/`
- `POST /auth/profile/change-password/`
- `GET /auth/users/`
- `GET /auth/users/<username>/`
- `GET /auth/check-username/`
- `GET /auth/check-email/`
- `POST /auth/resend-verification/`
- `POST /auth/verify-email/`
- `POST /auth/password-reset/`
- `POST /auth/password-reset/confirm/`
- `DELETE /auth/delete-account/`
- `POST /auth/google/login/`
- `GET|POST /auth/portfolio/`
- `GET|PUT|DELETE /auth/portfolio/<id>/`
- `GET /auth/users/<username>/portfolio/`

Auth rules:
- Public for registration/login/token refresh.
- JWT required for profile and logout.

Example:
```http
POST /api/auth/login/
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "StrongPass123"
}
```
```json
{
  "access": "<jwt_access>",
  "refresh": "<jwt_refresh>",
  "user": {"username": "sara", "is_client": true, "is_freelancer": true}
}
```

## Tasks
Purpose: task listing, creation, applications, status transitions, and reviews.

Main endpoints:
- `GET /tasks/`
- `POST /tasks/create/`
- `POST /tasks/{id}/apply/`
- `POST /tasks/applications/{id}/accept/`
- `POST /tasks/{id}/complete/`
Additional endpoints:
- `GET /tasks/categories/`
- `GET /tasks/my-tasks/`
- `GET /tasks/<id>/`
- `PUT|PATCH /tasks/<id>/update/`
- `DELETE /tasks/<id>/delete/`
- `POST /tasks/<id>/cancel/`
- `GET /tasks/<id>/applications/`
- `GET /tasks/my-applications/`
- `POST /tasks/applications/<id>/reject/`
- `POST /tasks/<id>/review/`
- `GET /tasks/<id>/reviews/`
- `GET /tasks/users/<username>/reviews/`
- `GET /tasks/statistics/`
- `GET /tasks/my-statistics/`
- `GET /tasks/saved/`
- `POST /tasks/<id>/save/`
- `GET /tasks/<id>/saved/`
- `DELETE /tasks/saved/<id>/`

Auth rules:
- Browsing is public.
- Creating/applying/updating lifecycle requires JWT and role/ownership checks.

Example:
```http
POST /api/tasks/42/apply/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "proposal": "I can deliver in 3 days",
  "bid_amount": "120.00"
}
```
```json
{
  "application_id": 308,
  "status": "pending",
  "task_id": 42
}
```

## Messaging
Purpose: conversations, messages, read state, and message stats.

Main endpoints:
- `GET /messaging/conversations/`
- `POST /messaging/conversations/create/`
- `GET /messaging/conversations/{id}/messages/`
- `POST /messaging/conversations/{id}/messages/send/`
Additional endpoints:
- `GET /messaging/conversations/<id>/`
- `POST /messaging/conversations/<id>/mark-read/`
- `GET /messaging/statistics/`

Auth rules:
- JWT required for all messaging routes.
- Conversation access is participant-scoped.

Example:
```http
POST /api/messaging/conversations/99/messages/send/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "content": "Draft uploaded. Please review."
}
```
```json
{
  "message_id": 771,
  "conversation_id": 99,
  "sender": "freelancer_user",
  "content": "Draft uploaded. Please review.",
  "created_at": "2026-02-10T16:32:00Z"
}
```

## Payments
Purpose: connected account onboarding, escrow operations, wallet, and withdrawals.

Main endpoints:
- `POST /payments/connect/create/`
- `POST /payments/connect/onboarding/`
- `POST /payments/intents/create/`
- `POST /payments/escrow/{id}/release/`
- `GET /payments/wallet/transactions/`
Additional endpoints:
- `GET /payments/connect/status/`
- `GET /payments/escrow/<id>/`
- `POST /payments/escrow/<id>/refund/`
- `GET /payments/wallet/`
- `GET /payments/withdrawals/`
- `POST /payments/withdrawals/create/`
- `GET /payments/payment-methods/`
- `POST /payments/payment-methods/create/`
- `DELETE /payments/payment-methods/<id>/delete/`
- `POST /payments/payment-methods/<id>/set-default/`
- `POST /payments/webhooks/stripe/`

Auth rules:
- JWT required for all payment operations except webhook receiver.
- Webhooks (`/payments/webhooks/stripe/`) are provider-authenticated.

Example:
```http
POST /api/payments/intents/create/
Authorization: Bearer <access_token>
Content-Type: application/json

{
  "task_id": 42,
  "amount": "200.00",
  "currency": "usd"
}
```
```json
{
  "intent_id": "pi_...",
  "client_secret": "pi_..._secret_...",
  "status": "requires_payment_method"
}
```

## Recommendations
Purpose: personalized task ranking and freelancer discovery.

Main endpoints:
- `GET /recommendations/tasks/`
- `GET /recommendations/freelancers/`
- `GET|PUT /recommendations/preferences/`
- `POST /recommendations/onboarding/`
Additional endpoints:
- `GET /recommendations/service-offerings/`
- `GET /recommendations/freelancers/<task_id>/`
- `GET /recommendations/onboarding/status/`
- `GET /recommendations/skills/`
- `GET /recommendations/skills/my/`
- `POST /recommendations/skills/update/`
- `GET /recommendations/categories/`

## Chatbot
Purpose: AI chatbot sessions, messaging, and task extraction.

Main endpoints:
- `GET /chatbot/sessions/`
- `GET /chatbot/sessions/<id>/`
- `POST /chatbot/sessions/<id>/end/`
- `POST /chatbot/chat/`
- `POST /chatbot/sessions/<id>/extract-task/`
- `POST /chatbot/suggest-category/`
- `POST /chatbot/messages/<id>/rate/`
- `GET /chatbot/status/`
- `GET /chatbot/statistics/`

Auth rules:
- JWT required for personalized feeds and preferences.
- Some catalog endpoints are public.

Example:
```http
GET /api/recommendations/tasks/
Authorization: Bearer <access_token>
```
```json
{
  "results": [
    {"task_id": 56, "match_score": 0.91, "reason": "Python + API integration history"}
  ]
}
```
## Notifications
Purpose: notification inbox and preferences.

Main endpoints:
- `GET /notifications/`
- `GET /notifications/unread-count/`
- `POST /notifications/<id>/read/`
- `DELETE /notifications/<id>/delete/`
- `POST /notifications/mark-all-read/`
- `DELETE /notifications/clear-all/`
- `GET|PUT /notifications/preferences/`

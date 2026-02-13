# API Reference

Base URL: `http://localhost:8000/api`

This page summarizes the public backend surface by domain, with authentication expectations and representative examples.

## Authentication and Session

### Purpose

Identity, account lifecycle, profile updates, and token refresh.

### Key Endpoints

- `POST /auth/register/`
- `POST /auth/login/`
- `POST /auth/token/refresh/`
- `POST /auth/logout/`
- `GET|PUT /auth/profile/`

### Additional Endpoints

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

### Access Rules

- Public: register, login, verify, password reset, username/email checks.
- JWT required: profile, logout, portfolio management, account deletion.

### Example

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
  "user": {
    "username": "sara",
    "is_client": true,
    "is_freelancer": true
  }
}
```

## Tasks and Applications

### Purpose

Marketplace listing, task creation, applications, acceptance, completion, cancellation, reviews, and saved tasks.

### Key Endpoints

- `GET /tasks/`
- `POST /tasks/create/`
- `POST /tasks/<id>/apply/`
- `POST /tasks/applications/<id>/accept/`
- `POST /tasks/<id>/complete/`

### Additional Endpoints

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

### Access Rules

- Public: browse tasks, categories, details.
- JWT + role checks: create/apply/accept/reject/complete/cancel/review.
- Ownership checks apply to update/delete and application review actions.

### Example

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

### Purpose

Conversation lifecycle, message creation, read state, and messaging statistics.

### Key Endpoints

- `GET /messaging/conversations/`
- `POST /messaging/conversations/create/`
- `GET /messaging/conversations/<id>/messages/`
- `POST /messaging/conversations/<id>/messages/send/`

### Additional Endpoints

- `GET /messaging/conversations/<id>/`
- `POST /messaging/conversations/<id>/mark-read/`
- `GET /messaging/statistics/`

### Access Rules

- JWT required for all messaging endpoints.
- Access is restricted to conversation participants.

## Notifications

### Purpose

Notification inbox, unread counters, deletion, and preference management.

### Endpoints

- `GET /notifications/`
- `GET /notifications/unread-count/`
- `POST /notifications/<id>/read/`
- `DELETE /notifications/<id>/delete/`
- `POST /notifications/mark-all-read/`
- `DELETE /notifications/clear-all/`
- `GET|PUT /notifications/preferences/`

### Access Rules

- JWT required for all notification operations.

## Payments

### Purpose

Connected account onboarding, payment intents, escrow release/refund, wallet ledger, and withdrawals.

### Key Endpoints

- `POST /payments/connect/create/`
- `POST /payments/connect/onboarding/`
- `POST /payments/intents/create/`
- `POST /payments/escrow/<id>/release/`
- `GET /payments/wallet/transactions/`

### Additional Endpoints

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

### Access Rules

- JWT required for user payment actions.
- `POST /payments/webhooks/stripe/` is provider-authenticated.

## Recommendations

### Purpose

Task ranking, freelancer discovery, and preference/profile tuning.

### Endpoints

- `GET /recommendations/tasks/`
- `GET /recommendations/freelancers/`
- `GET|PUT /recommendations/preferences/`
- `POST /recommendations/onboarding/`
- `GET /recommendations/service-offerings/`
- `GET /recommendations/freelancers/<task_id>/`
- `GET /recommendations/onboarding/status/`
- `GET /recommendations/skills/`
- `GET /recommendations/skills/my/`
- `POST /recommendations/skills/update/`
- `GET /recommendations/categories/`

### Access Rules

- Personalized feeds and preferences require JWT.
- Some taxonomy/catalog endpoints may be public.

## Chatbot

### Purpose

Assistant sessions, chat exchange, suggested categories, and structured task extraction.

### Endpoints

- `GET /chatbot/sessions/`
- `GET /chatbot/sessions/<id>/`
- `POST /chatbot/sessions/<id>/end/`
- `POST /chatbot/chat/`
- `POST /chatbot/sessions/<id>/extract-task/`
- `POST /chatbot/suggest-category/`
- `POST /chatbot/messages/<id>/rate/`
- `GET /chatbot/status/`
- `GET /chatbot/statistics/`

## Integration Notes

- Prefer token refresh flow over forcing relogin on access expiration.
- Treat payment updates as asynchronous and webhook-confirmed.
- Re-fetch canonical resources after realtime events to ensure consistency.

## UI Evidence

| API Domain | Preview |
|---|---|
| Auth | ![Login](../assets/screenshots/login-page.png) |
| Tasks | ![Task detail](../assets/screenshots/first-part-specific-task-page.png) |
| Messaging | ![Messages](../assets/screenshots/messages-conversation-page.png) |
| Notifications | ![Notifications](../assets/screenshots/notifications-page.png) |
| Payments | ![Wallet](../assets/screenshots/wallet-page.png) |
| Recommendations | ![Recommendations](../assets/screenshots/first-part-recommendations-page.png) |

## Related Pages

- [Features](features.md)
- [Realtime](realtime.md)
- [Payments](payments.md)
- [Security](security.md)

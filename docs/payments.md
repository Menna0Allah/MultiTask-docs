# Payments

This page documents the escrow-centered payment model, connected-account onboarding, and payout flow.

## Payment Model

MultiTask uses an escrow-style lifecycle:

1. Client accepts a freelancer.
2. Client funds payment intent for the task.
3. Funds remain in escrow context while work is delivered.
4. Client confirms completion.
5. Platform releases eligible funds.
6. Freelancer withdraws available balance.

## Provider Integration

Stripe Connect is currently used for:

- Freelancer connected account onboarding.
- Payment intent creation and tracking.
- Escrow release and refund operations.
- Webhook-driven payment status synchronization.

## Commercial Split

- Platform fee: 15%
- Freelancer share: 85%

## API Touchpoints

- `POST /payments/connect/create/`
- `POST /payments/connect/onboarding/`
- `GET /payments/connect/status/`
- `POST /payments/intents/create/`
- `GET /payments/escrow/<id>/`
- `POST /payments/escrow/<id>/release/`
- `POST /payments/escrow/<id>/refund/`
- `GET /payments/wallet/`
- `GET /payments/wallet/transactions/`
- `GET /payments/withdrawals/`
- `POST /payments/withdrawals/create/`
- `POST /payments/webhooks/stripe/`

## Operational Controls

- Treat payment status as asynchronous until webhook confirmation.
- Keep release and refund actions explicit and auditable.
- Restrict payment actions by role and task ownership constraints.
- Record transaction events in wallet history for user transparency.

## Current Scope and Limitations

- Stripe is the active milestone provider.
- Regional optimization is in progress.
- Egypt-focused provider support is planned for broader local compatibility.

## UI Evidence

| Payment Surface | Preview |
|---|---|
| Wallet | ![Wallet](../assets/screenshots/wallet-page.png) |
| Transactions | ![Transactions](../assets/screenshots/transactions-page.png) |
| Payment details | ![Payment details](../assets/screenshots/payment-details-to-specific-task-page.png) |

## Related Pages

- [API](api.md)
- [Security](security.md)
- [Features](features.md)

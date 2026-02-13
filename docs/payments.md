# Payments

## Model
MultiTask uses an escrow-style flow: funds are authorized/held, delivery is completed, then release occurs after client confirmation.

## Stripe Connect Role
Stripe Connect is used for:
- Connected account onboarding for freelancers.
- Payout routing.
- Payment intents and transaction lifecycle.
- Webhook-driven status synchronization.

## Payment Flow
1. Client accepts freelancer application.
2. Client funds payment intent linked to the task.
3. Funds are held in escrow context.
4. Freelancer completes delivery.
5. Client marks task complete.
6. Platform triggers escrow release.
7. Freelancer withdraws according to payout availability.

## Fees
- Platform fee: 15%
- Freelancer receives: 85%

## Current Limitations
- Regional optimization is still in progress.
- Stripe is the active provider for current milestone delivery.
- Egypt-focused provider support is planned for better local compatibility.

## Operational Notes
- Refund and release paths are explicit backend actions.
- Payment events should be treated as asynchronous and webhook-confirmed.
- Webhook endpoint: `/payments/webhooks/stripe/` (provider-authenticated).

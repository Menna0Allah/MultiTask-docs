# Features

## Role Logic
- `is_client=true`: can create and manage tasks, hire, and release payment.
- `is_freelancer=true`: can apply, deliver, receive payouts, and maintain portfolio.
- `both=true`: can use both pipelines in one account.

## Client Features
- Post tasks with category, budget, and delivery scope.
- Review incoming applications and accept/reject candidates.
- Track task status from posting to completion.
- Discover freelancers and compare profiles.
- Fund escrow and release payment after approved delivery.
- Rate and review completed freelancer work.

## Freelancer Features
- Browse open opportunities and apply with proposals.
- Track applications and accepted work from one dashboard.
- Deliver work and coordinate updates with clients.
- Receive escrow releases and withdraw eligible earnings.
- Build profile and portfolio to improve win rate.
- Get personalized task recommendations.

## Shared Features
- Secure authentication and account management.
- Real-time messaging and notification center.
- Saved tasks and profile personalization.
- Wallet visibility and transaction history.

## Navigation Visibility
- Public: home, categories, tasks, how-it-works, legal pages.
- Authenticated client paths: post task, freelancers, payment controls.
- Authenticated freelancer paths: recommendations, payout setup.
- Shared authenticated paths: dashboard, messages, notifications, profile.

## Route Summary (Derived)
Public routes include:
- `/`, `/login`, `/register`, `/forgot-password`, `/reset-password`, `/verify-email`
- `/categories`, `/how-it-works`, `/privacy`, `/terms`, `/contact`, `/faq`, `/about`
- `/tasks`, `/tasks/:id`, `/users/:username`

Protected routes include:
- `/dashboard`, `/tasks/create`, `/tasks/:id/edit`, `/my-tasks`, `/saved-tasks`
- `/profile`, `/messages`, `/notifications`
- `/recommendations` (freelancer/both), `/freelancers` (client/both)
- `/wallet`, `/transactions`, `/payments/onboarding`

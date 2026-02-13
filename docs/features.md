# Features

This page summarizes product capabilities, access boundaries, and the practical user journeys for each account type.

## Account Model

| Account Type | `is_client` | `is_freelancer` | Primary Outcomes |
|---|---:|---:|---|
| Client | true | false | Post tasks, hire freelancers, release payments |
| Freelancer | false | true | Apply to tasks, deliver work, receive payouts |
| Both | true | true | Operate both pipelines from one account |

## Capability Matrix

| Capability | Client | Freelancer | Both |
|---|:---:|:---:|:---:|
| Browse tasks and details | Yes | Yes | Yes |
| Create and manage tasks | Yes | No | Yes |
| Apply to tasks | No | Yes | Yes |
| Review applications | Yes | No | Yes |
| Access freelancer discovery | Yes | No | Yes |
| Access recommendations feed | No | Yes | Yes |
| Messaging and notifications | Yes | Yes | Yes |
| Wallet and transactions | Yes | Yes | Yes |

## Core Journeys

### 1. Client Hiring Flow

1. Create a task with category, budget, and scope.
2. Review incoming applications.
3. Accept a freelancer and fund payment intent.
4. Evaluate delivery and mark completion.
5. Release escrow and leave review.

### 2. Freelancer Delivery Flow

1. Browse marketplace opportunities.
2. Submit proposal with bid and delivery approach.
3. Coordinate requirements through messaging.
4. Deliver work and request completion.
5. Receive payout and build profile credibility.

### 3. Shared Collaboration Flow

1. Track work through dashboard and notifications.
2. Use real-time chat for alignment.
3. Monitor progress, payment status, and history.

## Navigation Visibility

### Public Routes

- `/`, `/categories`, `/tasks`, `/tasks/:id`
- `/how-it-works`, `/faq`, `/about`, `/contact`
- `/privacy`, `/terms`, `/login`, `/register`

### Authenticated Routes

- Shared: `/dashboard`, `/messages`, `/notifications`, `/profile`, `/wallet`, `/transactions`
- Client/Both: `/tasks/create`, `/freelancers`
- Freelancer/Both: `/recommendations`, `/payments/onboarding`

## UI Evidence

| Capability Area | Preview |
|---|---|
| Task browsing | ![Tasks](../assets/screenshots/first-part-tasks-page.png) |
| Task detail and apply | ![Task detail](../assets/screenshots/first-part-specific-task-page.png) |
| Create task | ![Create task](../assets/screenshots/first-part-create-task-page.png) |
| Freelancer discovery | ![Freelancers](../assets/screenshots/first-part-freelancers-page.png) |
| Recommendations | ![Recommendations](../assets/screenshots/first-part-recommendations-page.png) |
| Dashboard workspace | ![Dashboard](../assets/screenshots/dashboard-page.png) |

## Related Pages

- [API](api.md)
- [Payments](payments.md)
- [Realtime](realtime.md)
- [UI Showcase](screenshots.md)

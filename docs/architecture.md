# Architecture

This page documents the platform at system-boundary level rather than implementation-level code details.

## Architecture Goals

- Keep frontend, API, realtime, and payment concerns separated.
- Enforce role-aware permissions at service boundaries.
- Persist critical events before fanout to ensure recoverability.
- Keep external providers (payments and AI) isolated behind backend services.

## 1) System Topology

![System architecture diagram](../assets/diagrams/system-architecture.svg)

```mermaid
flowchart LR
  U[User Browser] --> FE[React + Vite Frontend]
  FE --> API[Django REST API]
  FE --> WS[Django Channels WebSocket]
  API --> DB[(PostgreSQL)]
  API --> STRIPE[Stripe Connect]
  API --> GEMINI[Gemini API]
  WS --> DB
```

### Boundary Notes

- Frontend handles UI state and authenticated request orchestration.
- REST API owns domain rules, role checks, and transaction state.
- Channels layer handles low-latency fanout for chat and notifications.
- PostgreSQL is the system of record for durable state.

## 2) Authentication Lifecycle

![Authentication flow diagram](../assets/diagrams/auth-flow.svg)

```mermaid
flowchart TD
  A[Register or Login] --> B[Backend validates credentials]
  B --> C[Issue Access + Refresh JWT]
  C --> D[Frontend stores session tokens]
  D --> E[Protected API requests]
  E --> F{Access expired?}
  F -- No --> G[Continue]
  F -- Yes --> H[Refresh token endpoint]
  H --> I[New access token]
  I --> G
  G --> J[Logout or token invalidation]
```

## 3) Task State Machine

![Task lifecycle diagram](../assets/diagrams/task-lifecycle.svg)

```mermaid
stateDiagram-v2
  [*] --> Posted
  Posted --> Applied: Freelancer applies
  Applied --> Accepted: Client accepts
  Accepted --> InProgress: Work starts
  InProgress --> Completed: Client marks complete
  InProgress --> Cancelled: Cancellation path
  Completed --> Reviewed: Mutual review
  Reviewed --> [*]
  Cancelled --> [*]
```

## 4) Realtime Delivery Path

![Realtime messaging flow diagram](../assets/diagrams/realtime-flow.svg)

```mermaid
sequenceDiagram
  participant C as Client App
  participant W as WebSocket Gateway
  participant S as Django Services
  participant D as PostgreSQL

  C->>W: Connect (JWT-authenticated)
  W->>S: Validate identity and membership
  C->>W: Send message payload
  W->>S: Persist then fanout
  S->>D: Save message/notification
  S-->>W: Event payload
  W-->>C: Update event
```

## 5) Recommendation Path

![Recommendations flow diagram](../assets/diagrams/recommendations-flow.svg)

```mermaid
flowchart LR
  P[User skills + history + preferences] --> R[Recommendation engine]
  T[Open tasks / freelancer profiles] --> R
  R --> O[Ranked output]
  O --> UI[For You and Discovery views]
```

## 6) AI Assistant Path

![Chatbot flow diagram](../assets/diagrams/chatbot-flow.svg)

## UI Validation Points

| Domain | Preview |
|---|---|
| Dashboard shell | ![Dashboard](../assets/screenshots/dashboard-page.png) |
| Task details | ![Task detail](../assets/screenshots/first-part-specific-task-page.png) |
| Messaging | ![Messages](../assets/screenshots/messages-conversation-page.png) |
| Wallet | ![Wallet](../assets/screenshots/wallet-page.png) |

## Related Pages

- [Features](features.md)
- [API](api.md)
- [Realtime](realtime.md)
- [Payments](payments.md)
- [Security](security.md)

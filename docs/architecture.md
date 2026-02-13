# Architecture

This page explains behavior using diagrams instead of implementation-level detail.

## 1) System Architecture
![System architecture diagram](../assets/diagrams/system-architecture.svg)
```mermaid
flowchart LR
  U[User Browser] --> FE[React + Vite Frontend]
  FE --> API[Django REST API]
  FE --> WS[Django Channels WS]
  API --> DB[(PostgreSQL)]
  API --> STRIPE[Stripe Connect]
  API --> GEMINI[Gemini API]
  WS --> DB
```

## 2) Authentication Flow
![Authentication flow diagram](../assets/diagrams/auth-flow.svg)
```mermaid
flowchart TD
  A[Register or Login] --> B[Backend validates credentials]
  B --> C[Issue Access + Refresh JWT]
  C --> D[Frontend stores tokens]
  D --> E[Call protected APIs with Access token]
  E --> F{Access expired?}
  F -- No --> G[Continue]
  F -- Yes --> H[Refresh token endpoint]
  H --> I[New access token]
  I --> G
  G --> J[Logout or token invalidation event]
```

## 3) Task Lifecycle
![Task lifecycle diagram](../assets/diagrams/task-lifecycle.svg)
```mermaid
stateDiagram-v2
  [*] --> Posted
  Posted --> Applied: Freelancer applies
  Applied --> Accepted: Client accepts
  Accepted --> InProgress: Work starts
  InProgress --> Completed: Client marks complete
  InProgress --> Cancelled: Client/Freelancer cancellation path
  Completed --> Reviewed: Both parties review
  Reviewed --> [*]
  Cancelled --> [*]
```

## 4) Realtime Flow
![Realtime messaging diagram](../assets/diagrams/realtime-flow.svg)
```mermaid
sequenceDiagram
  participant C as Client App
  participant W as WebSocket Gateway
  participant S as Django Services
  participant D as PostgreSQL

  C->>W: Connect (JWT-authenticated)
  W->>S: Validate session
  C->>W: Send chat message
  W->>S: Persist + fanout
  S->>D: Save message/notification
  S-->>W: Event payload
  W-->>C: Realtime update
```

## 5) Recommendations Flow
![Recommendations diagram](../assets/diagrams/recommendations-flow.svg)
```mermaid
flowchart LR
  P[User skills + history + prefs] --> R[Recommendation engine]
  T[Open tasks / freelancer profiles] --> R
  R --> O[Ranked recommendations]
  O --> UI[For You / Freelancer discovery UI]
```

## 6) Chatbot Flow
![Chatbot flow diagram](../assets/diagrams/chatbot-flow.svg)

## Notes
- Architecture prioritizes clear API boundaries and event-driven user feedback.
- Realtime events are persisted so users can recover state after reconnect.
- Payments and recommendations are isolated domains integrated via backend services.

# MultiTask Documentation

MultiTask is a marketplace platform where clients and freelancers collaborate on scoped work with messaging, escrow-style payments, and role-aware workflows.

## Documentation Map

- [Architecture](architecture.md): system boundaries, data flow, and core diagrams.
- [Features](features.md): capabilities by user type and route visibility.
- [API](api.md): endpoint surface and integration examples.
- [Realtime](realtime.md): WebSocket channels, events, and reliability strategy.
- [Payments](payments.md): escrow lifecycle, fees, and operational checkpoints.
- [Security](security.md): auth model, controls, and hardening checklist.
- [Quickstart](quickstart.md): local setup and environment requirements.
- [UI Showcase](screenshots.md): complete screenshot walkthrough.

## Platform Pillars

- Role-flexible accounts (`client`, `freelancer`, `both`).
- End-to-end task lifecycle from posting to review.
- Real-time collaboration with chat and notification updates.
- Escrow-centered payment orchestration with Stripe Connect.
- Recommendation and assistant layers for discovery and support.

## Visual Highlights

| Area | Preview |
|---|---|
| Landing | ![Home hero](../assets/screenshots/start-hero-page.png) |
| Tasks Discovery | ![Tasks list](../assets/screenshots/first-part-tasks-page.png) |
| User Workspace | ![Dashboard](../assets/screenshots/dashboard-page.png) |
| Collaboration | ![Messages conversation](../assets/screenshots/messages-conversation-page.png) |

## System Flows

![System architecture diagram](../assets/diagrams/system-architecture.svg)
![Task lifecycle diagram](../assets/diagrams/task-lifecycle.svg)

## Intended Audience

- Product reviewers evaluating platform scope and maturity.
- Engineers onboarding into API and domain boundaries.
- Stakeholders reviewing user journeys and operational constraints.

## Repository Notes

This repository is documentation-only and safe for public sharing.
Source implementation repositories are private.

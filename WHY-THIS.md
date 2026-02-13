
# MultiTask Documentation

## Source Code Access

Original source code repository: [MultiTask](https://github.com/Menna0Allah/MultiTask.git)

Note: If you want to review the full source code, send an access request and I will accept it.

[![Docs](https://img.shields.io/badge/Docs-Live-brightgreen)](https://menna0allah.github.io/MultiTask-docs/)

Public, portfolio‑ready documentation for the MultiTask platform. This repository exists because the private source‑code repository contains sensitive information and cannot be made public. Everything here is intentionally sanitized and safe to share while still providing a complete, professional view of the product.

## Purpose of This Repo
- Provide a public, professional overview of the MultiTask system.
- Document product scope, flows, and API surface without exposing private implementation details.
- Serve as a reference for reviewers, collaborators, and anyone interested in the platform.

## Source of Truth
`README.md` and the pages in `docs/` are the maintained documentation sources in this repository.

## Repository Structure (How Everything Relates)
- `docs/`  
  Public site pages for architecture, features, API, security, and setup.
  - `docs/index.md` — Overview and high‑level product snapshots.
  - `docs/architecture.md` — Diagrams and architectural flows.
  - `docs/features.md` — User roles and feature inventory.
  - `docs/api.md` — Public API surface by domain (auth, tasks, messaging, payments, etc.).
  - `docs/realtime.md` — WebSocket behavior and realtime delivery.
  - `docs/payments.md` — Escrow model, Stripe Connect flow, limitations.
  - `docs/security.md` — Auth strategy, token handling, and security notes.
  - `docs/quickstart.md` — Sanitized setup instructions for local evaluation.
  - `docs/screenshots.md` — Full screenshot map to browse every captured UI screen.
- `assets/diagrams/`  
  SVG diagrams used in `docs/architecture.md` and `docs/index.md`. These visualize system design and flows.
- `assets/screenshots/`  
  Full UI screenshot set. Referenced in `docs/screenshots.md` and selectively in `docs/index.md`.
- `mkdocs.yml`  
  MkDocs configuration for generating the public documentation site.

## Screenshots
All screenshots are in `assets/screenshots/` and are indexed in `docs/screenshots.md`. This keeps the documentation fully browsable without accessing the private repository.

## How to Preview Locally
```bash
pip install mkdocs mkdocs-material
mkdocs serve
```

## Publish to GitHub Pages
Deployment is manual.

Setup steps:
1. Update `repo_url` in `mkdocs.yml` with your real GitHub repo URL.
2. Build the site locally with `mkdocs build`.
3. Publish the generated site manually to your preferred Pages branch or hosting target.

## Contribution / Update Rules
- Keep `README.md` and `docs/*.md` consistent.
- Add or update diagrams in `assets/diagrams/` if flows change.
- Add or update screenshots in `assets/screenshots/` and keep `docs/screenshots.md` current.

## Privacy Note
This is a public documentation repository. The private implementation repository is intentionally not published because it contains sensitive information. This repo is the safe, public reference for the MultiTask platform.

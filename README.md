# MultiTask Documentation

[![Docs](https://img.shields.io/badge/Docs-Live-brightgreen)](https://menna0allah.github.io/MultiTask-docs/)

Public, portfolio‑ready documentation for the MultiTask platform. This repository exists because the private source‑code repository contains sensitive information and cannot be made public. Everything here is intentionally sanitized and safe to share while still providing a complete, professional view of the product.

## Purpose of This Repo
- Provide a public, professional overview of the MultiTask system.
- Document product scope, flows, and API surface without exposing private implementation details.
- Serve as a reference for reviewers, collaborators, and anyone interested in the platform.

## Source of Truth
`DOCUMENTATION.md` is the canonical source. All pages in `docs/` are derived or reorganized from it and must remain consistent.

## Repository Structure (How Everything Relates)
- `DOCUMENTATION.md`  
  Canonical full documentation. If anything changes, update this file first.
- `docs/`  
  Public site pages built from the canonical document. Each page is a focused slice of `DOCUMENTATION.md`.
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
This repo is configured to deploy automatically via GitHub Actions on push to `main` or `master`.

Setup steps:
1. Update `repo_url` in `mkdocs.yml` with your real GitHub repo URL.
2. In GitHub: Settings → Pages → Source: “GitHub Actions”.
3. Push to `main` (or `master`) to trigger deployment.

## Contribution / Update Rules
- Update `DOCUMENTATION.md` first.
- Propagate changes into the relevant `docs/*.md` pages.
- Add or update diagrams in `assets/diagrams/` if flows change.
- Add or update screenshots in `assets/screenshots/` and keep `docs/screenshots.md` current.

## Privacy Note
This is a public documentation repository. The private implementation repository is intentionally not published because it contains sensitive information. This repo is the safe, public reference for the MultiTask platform.

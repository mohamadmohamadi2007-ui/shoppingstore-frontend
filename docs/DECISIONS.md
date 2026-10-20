# Frontend Decisions Log

Records decisions made while building the customer-facing storefront, with date and reasoning.
Product-level decisions (shared across repos) live in `../../docs/DECISIONS.md`; the shared roadmap is at `../../docs/ROADMAP.md`.

## 2026-10-21 — Repo created as a sibling to `shoppingstore-backend`

This repo is the customer-facing storefront: catalog browse/search/filter, cart, checkout,
customer accounts, order history, returns/exchanges, fit-based reviews — the Phase 1 scope
in `../../docs/ROADMAP.md`.

**Why:** the project uses separate repos per concern (backend / frontend / admin panel) rather
than a monorepo, per the architecture decision already made for this project.

**Consequence:** this repo talks to `shoppingstore-backend` only over its HTTP API — no shared
code or direct database access between repos. Confirm the backend's current base URL and
available endpoints before building against it; check `shoppingstore-backend`'s own
`docs/DECISIONS.md` and `app/main.py` for what's actually implemented so far (the backend is
being built incrementally as a learning project, so not all Phase 1 endpoints exist yet).

**Notes for whoever works in this repo (e.g. Emma):**
- Persian/RTL UI is a Phase 1 requirement, not an afterthought — plan layout/CSS direction from the start.
- Payment is via Shaparak-certified gateways (Zarinpal, IDPay, NextPay) + cash on delivery; auth is OTP by mobile number, not email/password.
- Workflow: branch per feature (`feature/<name>`), open a PR into `master`, merge via PR (no direct pushes to `master`) — same loop used in `shoppingstore-backend`. Keeps `master` deployable and gives a reviewable history even solo.

# Kaal-site

Static marketing and legal site for **Kaal — Focus & Task Planner**, served on GitHub Pages at [jumbarthi.com](https://jumbarthi.com).

This repository is **web content only** (HTML/CSS). It does not contain Kaal mobile or desktop app source, APIs, or architecture.

## Live site

| Item | Value |
|------|--------|
| Domain | `jumbarthi.com` (see `CNAME`) |
| Hosting | GitHub Pages |
| Default branch | `main` |
| Repo | [`rjumbarthi/Kaal-site`](https://github.com/rjumbarthi/Kaal-site) |

Root `/` redirects to `/kaal/` (meta refresh + canonical link in `index.html`).

## Site map

| Path | File | Purpose |
|------|------|---------|
| `/` | `index.html` | Apex landing; redirects to `/kaal/` |
| `/kaal/` | `kaal/index.html` | Product landing (what Kaal does, data stance, Google Calendar note, support contact) |
| `/kaal/support` | `kaal/support/index.html` | Support contact, FAQ (account, Google Calendar, restore purchase, delete, notifications) |
| `/kaal/privacy` | `kaal/privacy/index.html` | Privacy Policy |
| `/kaal/terms` | `kaal/terms/index.html` | Terms of Service |
| `/kaal/delete` | `kaal/delete/index.html` | Account & data deletion (in-app + email request) |
| `/kaal/style.css` | `kaal/style.css` | Shared stylesheet for `/kaal/*` pages |

Shared layout: top nav (Home / Support / Privacy / Terms / Delete as relevant), footer with © 2026 Kaal · Maryland, USA, and `kaal_support@jumbarthi.com`.

## Other root files

| File | Role |
|------|------|
| `CNAME` | Custom domain: `jumbarthi.com` |
| `.nojekyll` | Disables Jekyll processing on GitHub Pages (serves files as-is) |
| `.pages-rebuild` | Build stamp (e.g. `build: 2026-06-27T14:46:28Z`) — used to trigger or record Pages rebuilds |
| `app-ads.txt` | Ad publisher authorization line for Google (`pub-9013964076288950`) |

## How GitHub Pages is used

1. Content lives as static files on `main`.
2. Pages serves the site; `CNAME` maps **jumbarthi.com** to this Pages site.
3. `.nojekyll` ensures paths and assets are not rewritten by Jekyll.
4. Update content by editing HTML/CSS and pushing to `main` (or opening a PR). After deploy, verify `/`, `/kaal/`, and the legal/support routes.

There is no build step in-repo beyond static files. Fonts load from Google Fonts (`Inter`) on the Kaal pages.

## Editing

- Landing copy and feature bullets: `kaal/index.html`
- Support FAQ / contact: `kaal/support/index.html`
- Legal: `kaal/privacy/index.html`, `kaal/terms/index.html`, `kaal/delete/index.html`
- Visual style: `kaal/style.css`

Keep paths absolute under `/kaal/` (e.g. `/kaal/style.css`, `/kaal/privacy`) so they resolve correctly on the custom domain.

## Out of scope (this repo)

- Kaal Android / iOS / Windows app code and APIs
- Auth, sync, or backend architecture
- Store listing assets beyond what appears on these pages

Document app internals only when they are shipped and sourced from Engineering / Product — not from this site alone.

## Contact

Support: [kaal_support@jumbarthi.com](mailto:kaal_support@jumbarthi.com)

## CI workflows

GitHub Actions under [`.github/workflows/`](.github/workflows/):

| Workflow | Triggers | What it checks |
|----------|----------|----------------|
| **CI (PR)** (`ci-pr.yml`) | Pull requests and pushes to `main` | Required site files exist; [html-proofer](https://github.com/gjtorikian/html-proofer) validates HTML and internal links (external URLs skipped); [stylelint](https://stylelint.io/) parses `kaal/style.css`. |
| **Verify Deploy** (`verify-deploy.yml`) | Push to `main`, manual **Run workflow** | Waits for GitHub Pages to respond, then HTTP-checks the live production URLs listed below. |

To run production verification manually: **Actions → Verify Deploy → Run workflow**.

## Verify after deploy

After a Pages deploy (or DNS/CNAME change), confirm these return successfully (the **Verify Deploy** workflow checks the same URLs automatically):

1. `https://jumbarthi.com/` (redirects to `/kaal/`)
2. `https://jumbarthi.com/kaal/`
3. `https://jumbarthi.com/kaal/privacy`
4. `https://jumbarthi.com/kaal/terms`
5. `https://jumbarthi.com/kaal/support`
6. `https://jumbarthi.com/kaal/delete`

Optional quick check: `curl -sI https://jumbarthi.com/kaal/ | head -n 1` (expect `200` or a redirect chain that lands on `/kaal/`).

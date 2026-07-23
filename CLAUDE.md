# CLAUDE.md — Boglarka Wagner consultant website

Context for future work in this repo.

## What this is

A static single-page consultant website for Boglarka Wagner (IT/data consultant, SAP BW & SAP Analytics Cloud specialist, Budapest), built from her LinkedIn profile content. Hosted on GitHub Pages, deployed via GitHub Actions.

## Files

- `index.html` — the whole site (hero, about, services, experience timeline, education, contact, footer). No JS framework; one inline `<script>` block at the bottom handles the "Show earlier experience" toggle.
- `style.css` — all styling. CSS custom properties (`:root`) at the top control the color palette (currently neutral navy/blue) — change there to re-theme.
- `profile_pic.jpeg` — Bogi's headshot, used in the hero section.
- `.github/workflows/deploy.yml` — GitHub Actions workflow; deploys to GitHub Pages on every push to `main` via the official `actions/*-pages` actions. Requires repo Settings → Pages → Source = "GitHub Actions" (one-time manual step, not done via this repo).
- `README.md` — setup/handoff notes for Milan (repo creation, Pages settings, custom domain, open TODOs).

## Key content decisions

- Positioning: "SAP analytics and business intelligence" consultant — inferred from her LinkedIn skills (SAP BW, SAP Analytics Cloud, Power BI, Tableau, Python, R, SQL) since there's no separate consulting-services doc.
- Experience section shows the 5 most recent roles by default; 8 earlier roles (2005–2019, admin/ops/analyst roles predating her IT pivot) are collapsed behind a CSS max-height fade + a "Show earlier experience" button (pure CSS/JS toggle, `#timelineMore` / `toggleExperience()`).
- Company logos are pulled live client-side from **logo.dev**'s image API (`https://img.logo.dev/<domain>?token=...`). Clearbit's logo API (originally used) was discontinued — do not revert to `logo.clearbit.com`.
  - Publishable token in use: `pk_dOWesGqrRiy72tFZFEg3Vw` (client-side safe, provided by Milan).
  - Every `<img>` has a colored-initials `.logo-fallback` span behind it (`onerror` hides the img if the request fails); logo.dev also returns its own monogram fallback by default, so images essentially never break.
  - logo.dev's free tier requires attribution for commercial use → added "Company logos via Logo.dev" link in the footer. Don't remove this unless the plan is upgraded to paid.

## Git / deploy setup (as of this session)

- This repo is scoped to a **different GitHub identity than Milan's default account**, configured locally (not globally) in this repo only:
  - `git config user.name` → `milanredele`
  - `git config user.email` → `milanredele@users.noreply.github.com` (GitHub's standard noreply pattern for that username — swap if Milan uses a different commit email)
  - `remote origin` → `https://github.com/bglrka/website.git`
- Nothing has been pushed yet. Pushing will require milanredele's own GitHub auth (SSH key, PAT, or `gh auth login` under that account) — not set up here, and not something to set up without the user's direct action per credential-handling rules.
- The actual GitHub repo (`bglrka/website`) has NOT been created yet — that's on Milan to do, along with enabling Pages via Actions in repo settings.

## Open items / still needed from Milan or Bogi

- Real contact email (currently placeholder `hello@example.com` in the contact section).
- Custom domain, if she wants one instead of the default `github.io` URL — see README for the CNAME/DNS steps.
- Brand color preferences, if any (currently a neutral navy/blue chosen by default).

## Conventions if extending this site

- Keep it a single HTML/CSS file pair — no build step, so GitHub Pages can serve it as-is.
- New experience entries follow the `.entry` → `.entry-head` → `.entry-logo` + title/org markup pattern already used; add new logos as `https://img.logo.dev/<company-domain>?token=pk_dOWesGqrRiy72tFZFEg3Vw&size=80` plus a 2-letter fallback span.
- Always validate HTML/CSS changes (e.g. `python3 -c "from html.parser import HTMLParser; HTMLParser().feed(open('index.html').read())"` and a brace-count check on the CSS) before considering an edit done.

# Boglarka Wagner — consultant website

Static single-page site (`index.html` + `style.css`), deployed to GitHub Pages via GitHub Actions (`.github/workflows/deploy.yml`).

## What I couldn't do myself — set these up on GitHub

1. **Create the repository.** Create a new public GitHub repo (e.g. `boglarkawagner/website` or similar) and push these files to the `main` branch.

2. **Enable GitHub Pages via Actions.** In the repo: Settings → Pages → under "Build and deployment", set **Source** to **GitHub Actions**. The included workflow will then deploy automatically on every push to `main`.

3. **Custom domain (if she has one).** If you want a custom domain instead of `<username>.github.io/<repo>`:
   - Add a file named `CNAME` at the repo root containing just the domain (e.g. `boglarkawagner.com`).
   - In your DNS provider, add either an `A` record pointing to GitHub's Pages IPs (`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`) for an apex domain, or a `CNAME` record pointing to `<username>.github.io` for a subdomain like `www`.
   - In Settings → Pages, enter the custom domain and enable "Enforce HTTPS" once DNS propagates.

## Still needed from you / Bogi

- **Real contact email** — I put a placeholder `hello@example.com` in the contact section (`index.html`, near the bottom) and need the real address.
- **logo.dev API token** — the experience section pulls company logos from logo.dev's image API. A publishable key (`pk_dOWesGqrRiy72tFZFEg3Vw`) is already wired into every logo `<img>` tag in `index.html`, so logos should just work. Note: logo.dev's free tier requires a small "logo.dev" attribution link somewhere on the page for commercial use (personal projects are exempt) — I haven't added one since this is a consultant/business site. If you want to stay fully compliant on the free tier, either add a small attribution link in the footer, or upgrade to a paid logo.dev plan to remove that requirement. Companies without a resolvable logo (e.g. iOR Sprachschule, which has no logo.dev entry) fall back to colored initials automatically — logo.dev also returns its own monogram fallback by default, so logos essentially never break.
- **Brand colors**, if she has preferences — currently a neutral navy/blue palette (`style.css`, `:root` variables at the top).
- **Custom domain name**, if applicable.

## Local preview

Just open `index.html` in a browser — no build step required.

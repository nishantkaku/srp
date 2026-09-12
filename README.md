# SRP prototype

Mobile search-results page (`srp.html`) from the Housing homepage codebase, packaged
as a standalone prototype with its built-in dummy listing data. Vite + vanilla JS/React.

## Run locally

```bash
npm install
npm run dev
```

Open `http://localhost:5173/srp.html?q=2+BHK+Apartment+in+Andheri+West` at a mobile
viewport width (this page is intentionally mobile-only — wider viewports show a
"Open in mobile" notice instead, matching the real product's behavior).

## Deploy to GitHub Pages

1. Create an empty GitHub repo and push this folder to it (`git remote add origin ...` then `git push -u origin main`).
2. In the repo: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Pushing to `main` runs `.github/workflows/deploy-github-pages.yml`, which builds with
   `VITE_BASE_PATH=/<repo>/` and publishes `dist/` to Pages.
4. Your site will be at `https://<you>.github.io/<repo>/srp.html?q=...`.

## Embed in Framer (or anywhere else)

Once it's live on Pages, add a Framer **Embed** component pointing at the deployed
`srp.html` URL (with whatever `?q=` you want preset). GitHub Pages doesn't send an
`X-Frame-Options`/frame-ancestors header, so it iframes without issue.

## What was changed from the original source

- The `mweb_buy_srp` internal experiment flag now defaults **on**, so the page
  renders immediately instead of requiring a manual `localStorage` toggle.
- Runtime (non-`import`) references to `public/` assets — listing photos, the
  logo, the back link, PDP navigation — go through `import.meta.env.BASE_URL`
  so they resolve correctly when hosted under a GitHub Pages project sub-path.
- Everything else (markup, styles, mock listing data, interactions) is unchanged.

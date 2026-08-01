# Deployment instructions

## Option A — Base44 (recommended)

This app is built on the Base44 platform.

1. Sign in to the Base44 builder.
2. Open this app (source is synced via **Settings → GitHub** → connect the `child-medical-screening` repo).
3. Click **Publish**. Base44 builds the Vite project, hosts the web app, and makes the same codebase available for iOS/Android packaging.
4. Environment variables (Base44 app id, service role) are managed in **Settings → Environment variables** — never commit secrets.

## Option B — Self-host the frontend build

```bash
npm install
npm run build      # outputs to dist/
```

Serve `dist/` from any static host (Vercel, Netlify, Cloudflare Pages, S3 + CloudFront, nginx).

> Note: the app depends on the Base44 backend (auth, entities, integrations, workflows). The frontend alone won't function without the Base44 app it was generated from. Keep the Base44 app active, or migrate entities/integrations to your own backend.

## GitHub 2-way sync

Use **Base44 builder → Settings → GitHub** to connect the repo. This keeps the builder source and the GitHub repo in sync in both directions. The GitHub *connector* (authorized with `repo` scope) is separate — it powers in-app features that read/write GitHub data, not the source-code sync.

---
title: "Deploying on Netlify"
permalink: /docs/netlify-deployment/
excerpt: "Use Netlify to build and host the Minimal Mistakes docs site."
last_modified_at: 2025-11-22
---

Minimal Mistakes can be deployed on Netlify without GitHub Pages by using the provided `netlify.toml` file at the root of the repository.
The configuration builds the `docs` site, publishes to `public`, and keeps URLs root-relative for Netlify-hosted domains.

## How the Netlify build works

- **Build command:** `bundle exec jekyll build --source docs --config docs/_config.yml --destination public --baseurl "" --url $URL`.
  The `--baseurl ""` flag removes the `/minimal-mistakes` subpath used on GitHub Pages, and the `--url` flag picks up Netlify's `URL` environment variable for canonical links.
- **Publish directory:** `public` (set in `netlify.toml`).
- **Bundler settings:** Environment variables in `netlify.toml` point Bundler at `docs/Gemfile`, cache gems in `vendor/bundle`, set `JEKYLL_ENV=production`, and lock the Ruby version to 3.2.
- **Deploy previews:** For preview builds the command swaps in `$DEPLOY_PRIME_URL` to generate correct preview URLs.

## Deploying your fork

1. Commit the repository to your own Git provider and connect it to Netlify with **Add new site → Import an existing project**.
2. Netlify will automatically read `netlify.toml`; no extra UI configuration is needed.
3. If you use optional services (e.g., Algolia search), add those credentials as Netlify environment variables under **Site configuration → Environment variables**.
4. Trigger a deploy; the generated site will be available from your Netlify-assigned domain (or a custom domain you configure).

## Testing locally with the Netlify settings

Run the same command Netlify uses so you can verify the build before pushing:

```bash
BUNDLE_GEMFILE=docs/Gemfile JEKYLL_ENV=production bundle exec jekyll build \
  --source docs --config docs/_config.yml --destination public --baseurl "" --url http://localhost:4000
```

This produces the `public` directory locally, matching the Netlify output.

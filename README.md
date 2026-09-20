# Astro Blog Starter (Cloudflare Workers)

## Structure

```
astro-blog/
├── src/
│   ├── content/
│   │   ├── config.ts        # schema for blog post frontmatter
│   │   └── blog/*.md        # your posts, one file per post
│   ├── layouts/
│   │   └── BaseLayout.astro # shared page shell (nav/footer)
│   └── pages/
│       ├── index.astro      # homepage, lists posts
│       └── blog/[...slug].astro  # renders each post
├── wrangler.toml              # Cloudflare Workers config (static assets)
├── astro.config.mjs
└── package.json
```

## Run locally

```
npm install
npm run dev
```

## Add a post

Create a new file in `src/content/blog/`, e.g. `my-new-project.md`, with
frontmatter matching the schema in `src/content/config.ts`:

```md
---
title: "My New Project"
description: "One line about it"
pubDate: 2026-09-18
tags: ["project"]
---

Body goes here in Markdown.
```

## Deploy to Cloudflare Workers + Porkbun domain

1. Install Wrangler and log in:
   ```
   npm install -g wrangler
   wrangler login
   ```
2. Build and deploy:
   ```
   npm run deploy
   ```
   (this runs `astro build`, then `wrangler deploy`, using the config in
   `wrangler.toml`). You'll get a live URL like
   `astro-blog.<your-subdomain>.workers.dev` immediately.
3. In the Cloudflare dashboard: Workers & Pages → your project →
   Settings → Domains & Routes → Add Custom Domain → enter your domain.
   Cloudflare will show you the DNS record to add.
4. In Porkbun's DNS panel for your domain, add the CNAME record Cloudflare
   gave you (usually `@` or `www` → `<project>.<subdomain>.workers.dev`,
   Cloudflare will be explicit about this).
5. Cloudflare auto-issues an SSL certificate once it verifies the DNS
   record — no manual "enforce HTTPS" step.

### Optional: auto-deploy on push

Connect this GitHub repo to Cloudflare Workers Builds (Workers & Pages →
Create → Connect to Git) so every push to `main` rebuilds and redeploys
automatically, without running `npm run deploy` by hand.

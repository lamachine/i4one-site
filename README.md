# I4One — Public Website

The public marketing website for **I4One**, served free via **GitHub Pages** at
**https://i4one.com**.

> This repository contains **only** the static website (HTML/CSS/JS). It contains
> **no application code and no secrets** — by design. The I4One application lives
> in a separate, private repository.

## Structure

```
.
├── index.html        # Landing page (placeholder copy — swap with your design)
├── privacy.html      # Privacy Policy (scaffold — fill bracketed placeholders)
├── terms.html        # Terms of Service (scaffold — fill bracketed placeholders)
├── 404.html          # Not-found page
├── CNAME             # Custom domain binding: i4one.com
├── robots.txt        # Crawler directives
├── sitemap.xml       # Sitemap
├── assets/
│   ├── style.css     # Small custom layer on top of Tailwind (CDN)
│   └── logo.svg      # Placeholder I4 monogram
├── LICENSE           # Content © I4One
└── .gitignore        # Belt-and-suspenders: blocks any secret/app file
```

No build step. Tailwind is loaded from its CDN, so the files are served exactly
as-is.

## Local preview

```bash
python -m http.server 8080
# then open http://localhost:8080
```

## Deploy (GitHub Pages)

See **DEPLOY.md** for the full step-by-step (create repo, enable Pages, DNS for
the apex domain, enforce HTTPS, Google domain verification).

## Security rule

Never copy application code, `.env` files, credentials, tokens, or internal infra
details into this repo. It is public. The `.gitignore` blocks the common offenders
as a safety net, but the real guarantee is keeping this repo separate.

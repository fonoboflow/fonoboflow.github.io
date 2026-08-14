# site/ — deploy root

**Everything in this folder is published. Nothing else is.**

This folder is the live website. It is deployed as-is to `fonoboflow.com`, so
its contents must be exactly what should be public, and nothing more.

```
site/
  index.html                          the site — the only page
  CNAME                               custom domain for the host (fonoboflow.com)
  assets/
    sebastian-bujak-portrait.webp     portrait, 800x1067, 28KB
    og.png                            share image, 1200x630
```

## Rules

1. **Do not put working files, drafts, or alternate versions here.** Explorations
   live in `explorations/`, superseded versions in `archive/`. A stray `.html` in
   this folder is a page that strangers can open.
2. **Web-optimised images only.** Full-resolution masters stay in the project
   root's `assets/`. The portrait ships as WebP only — the PNG and JPEG were
   deliberately removed, and `index.html` loads the WebP directly with no
   `<picture>` fallback.
3. **`CNAME` must not be deleted.** It is how the host maps the custom domain.
   Removing it drops the site back to the host's default subdomain.
4. **Paths are relative** (`assets/…`), so the folder works from any root. The
   Open Graph tags in `<head>` are the exception: they use absolute
   `https://fonoboflow.com/…` URLs, because social scrapers cannot resolve
   relative ones. Update those if the domain changes.

## History

- `archive/fonobo-flow-site.html` — earlier full-page version, moved out of this
  folder on 13 Aug 2026 so the deploy root contains only `index.html`.
- `assets/fonoboflow-og-1200x630.svg` (project root) — the vector source for
  `og.png`, moved out of this folder on 13 Aug 2026. Only served files live here.

## Regenerating og.png

Built from the wordmark paths in the root `assets/fonoboflow-on-white.svg`,
recoloured white on black and centred on a 1200x630 canvas. The vector source is
`assets/fonoboflow-og-1200x630.svg` in the project root; rasterise it at 1200x630
to regenerate `og.png`. The rules for compositing brand SVGs — copy path data
verbatim, position with transforms only, verify by rasterising — are in
`guidelines/logo-recreation-guide.card.html`.

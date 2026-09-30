# fonoboflow.com

**This repo is the single source of the website** (decided 30 Sep 2026). What is
committed here and pushed to `main` is what GitHub Pages publishes at
fonoboflow.com. There is no other copy to keep in sync.

```
index.html          English page
pl/index.html       Polish page
404.html            one not-found page, English above Polish
sitemap.xml         both URLs with hreflang alternates
robots.txt          allows all, points at the sitemap
CNAME               custom domain. Do not delete
.nojekyll           tells GitHub Pages not to run Jekyll
assets/             portrait (webp, srcset), og.png, favicon, apple-touch-icon
assets/fonts/       subset woff2 files. Read assets/fonts/README.md before any copy change
```

## Where things come from

| What | Source | Rule |
|---|---|---|
| Every word on both pages | Word Brandbook, newest release in Drive `02 releases`, sections Live copy › Website and Website PL | copied verbatim, never rewritten here |
| Colours, type, logo, assets | Claude Design design system (mirror in the `fonobo-flow-brand` repo) | the page is not in Claude Design any more |
| Layout, CSS, JS | this repo | edited here, one commit per change |

## Changing text

1. The change is made in the Word Brandbook master first, then a release is cut.
2. The text is applied here, in **both** pages where it has a counterpart.
3. Check before pushing: every sentence verbatim against the release; no en or em
   dash; every character inside `assets/fonts/CHARSET.txt` (including capitals
   produced by `text-transform: uppercase`).
4. Commit, push, then read the live page once.

## Rules

1. **No working files, drafts or alternate versions here.** A stray `.html` is a
   page strangers can open.
2. **Web-optimised assets only.** Masters live in the design system.
3. **`CNAME` must not be deleted.** It maps the custom domain.
4. **Paths are relative** (`assets/…` on the English page, `../assets/…` on the
   Polish one), except Open Graph and canonical URLs, which are absolute.
5. **Both pages change together.** A layout or CSS change made in `index.html` is
   made in `pl/index.html` in the same commit.

## Known, accepted tradeoffs

- The hero word swap cycles indefinitely, which fails WCAG 2.2.2 by choice; it
  pauses on hover, off-screen, in a hidden tab and under reduced motion.
- The language switcher sits in the navigation bar, which only appears once the
  visitor scrolls past the hero.

## History

- 13 Aug 2026: repo created, page moved here from the design tool export.
- 14 Aug 2026: optimised build (subset fonts, srcset portrait, favicon).
- 19 Aug 2026: dark mode and mobile menu added in the `fonobo-flow-brand` repo, never deployed.
- 30 Sep 2026: those edits carried over; this repo becomes the single source;
  English copy updated to brandbook release 2026-09-30b; Polish page added;
  fonts regenerated with Polish letters.

## Regenerating og.png

Built from the wordmark in the design system (`assets/fonoboflow-on-white.svg`),
recoloured white on black, centred on 1200x630. Vector source:
`assets/fonoboflow-og-1200x630.svg` in the design system.

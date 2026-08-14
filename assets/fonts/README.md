# Subset fonts — READ BEFORE EDITING COPY

These six files are **not complete fonts**. They contain only the characters listed
in `CHARSET.txt` (102 of them). Any character outside that set will render in a
fallback system font, **silently** — no error, no console warning, just one word in
the wrong typeface that is easy to miss.

Total: 50.2 KB for all six faces, down from 94.8 KB unsubset.

## ⚠️ Adding the Polish version REQUIRES regenerating these files

Polish needs nine characters that are **not in the current subset**:

```
ą ć ę ł ń ó ś ź ż    and their capitals    Ą Ć Ę Ł Ń Ó Ś Ź Ż
```

Ship the Polish copy against these files and every one of those letters falls back
to a system font. On a page whose entire identity is two typefaces, that is
immediately visible — `gubi czas, pieniądze, cel?` would render with a broken
`ą`.

**Regenerate both languages in one pass when the Polish copy is final.**

## How these were generated

Google Fonts' `text=` parameter returns a subset containing only the requested
characters. For each face:

```
https://fonts.googleapis.com/css2?family=<Family>:<axis>&text=<URL-encoded charset>
```

then download the `.woff2` the returned CSS points at. The six requests used:

| file | family | axis |
|---|---|---|
| poppins-latin-500 | Poppins | `ital,wght@0,500` |
| poppins-latin-600 | Poppins | `ital,wght@0,600` |
| poppins-latin-700 | Poppins | `ital,wght@0,700` |
| poppins-latin-italic-500 | Poppins | `ital,wght@1,500` |
| inter-latin-400 | Inter | `wght@400` |
| inter-latin-700 | Inter | `wght@700` |

To add Polish, append the eighteen characters above to `CHARSET.txt`, re-run all
six requests with the new charset, and replace all six files. Keep the filenames —
`index.html` references them directly.

`pyftsubset` (fonttools) does the same job offline if you prefer not to depend on
Google's endpoint.

## Why the charset is wider than what the page renders

The page currently renders 65 distinct glyphs. The subset carries 102. The extra
37 are ordinary punctuation and the rest of the alphabet, deliberately included so
routine copy edits cannot silently break typography. Trimming to exactly 65 would
save a further ~20 KB and make every future word a risk. Not worth it.

**A subtle trap that already caught one attempt at this:** `text-transform:
uppercase` renders glyphs that never appear in the HTML source. Four elements use
it — the hero eyebrow, the portrait caption role, and the two footer labels — which
between them need `R N C U D L K M` in capitals, none of which occur as capitals
in the source text. Deriving a charset by scraping the markup misses them.

## Licence

Poppins and Inter are both SIL Open Font License 1.1. Subsetting is a "Modified
Version", which the licence permits — but it requires the copyright notice and the
licence to travel with the redistributed files. `OFL.txt` in this folder carries both
upstream licences verbatim.

Neither family declares a Reserved Font Name, so the family names `Poppins` and `Inter`
are kept as-is in the `@font-face` rules. Do not rename them.

If you regenerate the subsets, `OFL.txt` stays as it is — unless you change the upstream
source, in which case replace it with that source's own `OFL.txt`.

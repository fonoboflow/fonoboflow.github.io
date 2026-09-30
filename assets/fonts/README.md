# Subset fonts — READ BEFORE EDITING COPY

These six files are **not complete fonts**. They contain only the characters listed
in `CHARSET.txt` (122 of them). Any character outside that set will render in a
fallback system font, **silently**: no error, no console warning, just one word in
the wrong typeface that is easy to miss.

Total: about 49 KB for all six faces.

## Polish is included (30 Sep 2026)

The charset now carries the Polish letters `ą ć ę ł ń ó ś ź ż` and their capitals,
plus `·` (the language switcher) and `„` (Polish opening quote). The same six files
serve both `index.html` and `pl/index.html`. Adding a character to either page's
copy means adding it to `CHARSET.txt` and regenerating all six files.

## How these were generated

Offline, with fontTools (`pyftsubset` / `fontTools.subset`), from the upstream
font files kept in the `fonobo-flow-brand` repo under `fonts/`:

| file | source | notes |
|---|---|---|
| poppins-latin-500 | Poppins-Medium.ttf | all layout features |
| poppins-latin-600 | Poppins-SemiBold.ttf | all layout features |
| poppins-latin-700 | Poppins-Bold.ttf | all layout features |
| poppins-latin-italic-500 | Poppins-MediumItalic.ttf | all layout features |
| inter-latin-400 | Inter-VariableFont_opsz,wght.ttf | instanced at opsz 14, wght 400; `kern`, `calt` only |
| inter-latin-700 | Inter-VariableFont_opsz,wght.ttf | instanced at opsz 14, wght 700; `kern`, `calt` only |

Output flavour woff2. Keep the filenames: both pages reference them directly.
Advance widths were compared glyph by glyph with the previous (Google Fonts)
subsets: identical for all Poppins faces and Inter 400; Inter 700 differs on two
glyphs (`2` and `"`), by the upstream version difference only.

The first subsets (14 Aug 2026) came from Google Fonts' `text=` endpoint. Either
method works; the offline one does not depend on Google's endpoint.

## Why the charset is wider than what the page renders

The pages render fewer glyphs than the subset carries. The extra ones are ordinary
punctuation and the rest of the alphabet, deliberately included so
routine copy edits cannot silently break typography. Trimming to exactly what renders
would save a few KB and make every future word a risk. Not worth it.

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

# pdfua2-mathml-se-alt — Structure Elements + Alt text

**Overleaf project:** [pdfua2-mathml-se-alt](https://www.overleaf.com/read/fbjvjmzppdyj#618976) (read-only)

This file tests **SE + Alt text**: MathML is written into the PDF tag tree as Structure Elements, and a plain-text alternative (Alt text) is also auto-generated on the formula tag. No Associated File is embedded.

## Files

| File | Description |
|---|---|
| `main.tex` | LaTeX source |
| `main.pdf` | Compiled PDF output |
| `latexmkrc` | Overleaf compilation configuration (shared across all six projects) |

## `\DocumentMetadata` configuration

```latex
\DocumentMetadata{
  lang=en,
  tagging=on,
  pdfstandard = {ua-2, A-4f},
  tagging-setup={
    math/setup = mathml-SE,
    math/alt/use = true
  }
}
```

**Key choices:**

- **`pdfstandard = {ua-2, A-4f}`** — `A-4f` is technically redundant here since no Associated Files are embedded, but it is declared consistently across all six test files. Its presence is harmless. See the [top-level README](../README.md#pdf-standards-pdfstandardua-2-and-pdfstandardA-4f).
- **`math/setup = mathml-SE`** — MathML is written into the tag tree as Structure Elements. Requires LuaLaTeX.
- **`math/alt/use = true`** — Auto-generates a plain-text `Alt` attribute on the formula tag in addition to the SE MathML.
- **`lang=en`** — See the [top-level README](../README.md#language-langen) for the reasoning behind using `en` rather than `en-US`.

## Test results summary

| Screen reader + PDF viewer | Result |
|---|---|
| NVDA with Adobe Acrobat Pro | ❌ Alt text (static string; no interactivity) |
| JAWS with Adobe Acrobat Pro | ❌ Alt text (static string; no interactivity) |
| NVDA with Firefox | ✅ Configurable math speech/braille; interactive expression exploring |
| JAWS with Firefox | ✅ Configurable math speech/braille; interactive expression exploring |
| NVDA or JAWS with Chrome/Edge | ❌ Math is skipped over; not read aloud |
| VoiceOver macOS (all viewers) | ❌ Speaks as gibberish / math skipped |

See the [full results table](../../index.html) for complete detail and test dates.

## Notes

Results are identical to AF+Alt for all tested environments. Adobe Acrobat Pro prioritizes the `Alt` attribute over the MathML Structure Elements, causing both NVDA and JAWS to read the static alt string in Acrobat. Firefox correctly ignores the `Alt` attribute and routes to MathML via MathCAT.

This result is notable because it shows that even with MathML embedded directly in the tag tree (SE), the presence of an `Alt` attribute is sufficient to suppress MathML access in Acrobat. The `Alt` attribute acts as a ceiling on math accessibility in that viewer regardless of what MathML is also present.

# pdfua2-mathml-se — Structure Elements only

**Overleaf project:** [pdfua2-mathml-se](https://www.overleaf.com/read/zghsqhpyybgd#0e4fdf) (read-only)

This file tests **SE only**: MathML written directly into the PDF tag tree as Structure Elements. No Associated File is attached to the formula tag, and no Alt text is generated.

## Files

| File | Description |
|---|---|
| `main.tex` | LaTeX source |
| `pdfua2-mathml-se.pdf` | Compiled PDF output |
| `latexmkrc` | Overleaf compilation configuration (shared across all six projects) |

## `\DocumentMetadata` configuration

```latex
\DocumentMetadata{
  lang=en,
  tagging=on,
  pdfstandard = {ua-2, A-4f},
  tagging-setup={
    math/setup = mathml-SE
  }
}
```

**Key choices:**

- **`pdfstandard = {ua-2, A-4f}`** — `A-4f` is technically redundant here since no Associated Files are embedded, but it is declared consistently across all six test files. Its presence is harmless. See the [top-level README](../README.md#pdf-standards-pdfstandardua-2-and-pdfstandardA-4f).
- **`math/setup = mathml-SE`** — Instructs the LaTeX tagging engine to write MathML directly into the PDF structure tree as tagged Structure Elements nested under the formula tag. This method requires LuaLaTeX; it is not available with PDFLaTeX or XeLaTeX.
- **No `math/alt/use`** — No Alt text is generated on the formula tag.
- **`lang=en`** — See the [top-level README](../README.md#language-langen) for the reasoning behind using `en` rather than `en-US`.

## Test results summary

| Screen reader + PDF viewer | Result |
|---|---|
| NVDA with Adobe Acrobat Pro | ✅ Configurable math speech/braille; interactive expression exploring |
| JAWS with Adobe Acrobat Pro | ❌ Math speech character by character (result uncertain) |
| NVDA with Firefox | ✅ Configurable math speech/braille; interactive expression exploring |
| JAWS with Firefox | ✅ Configurable math speech/braille; interactive expression exploring |
| NVDA or JAWS with Chrome/Edge | ❌ Math is skipped over; not read aloud |
| VoiceOver macOS (all viewers) | ❌ Speaks as gibberish / math skipped |

See the [full results table](../../index.html) for complete detail and test dates.

## Notes

JAWS with Adobe Acrobat Pro produced an unusual result with SE-only encoding: rather than speaking raw MathML markup (as with AF encoding), it appeared to traverse the MathML structure tree character by character. This behavior is uncertain and may warrant further investigation. NVDA and JAWS in Firefox both correctly routed through MathCAT.

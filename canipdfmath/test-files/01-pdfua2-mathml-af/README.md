# pdfua2-mathml-af — Associated Files only

**Overleaf project:** [pdfua2-mathml-af](https://www.overleaf.com/read/mqkqqkppggnh#972502) (read-only)

This file tests **AF only**: MathML embedded as an Associated File attached to the formula tag. No MathML Structure Elements are written into the PDF tag tree, and no Alt text is generated on the formula tag.

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
    math/setup = mathml-AF
  }
}
```

**Key choices:**

- **`pdfstandard = {ua-2, A-4f}`** — `A-4f` is required here because the AF method embeds MathML as a file attachment on each formula object. See the [top-level README](../README.md#pdf-standards-pdfstandardua-2-and-pdfstandardA-4f) for a full explanation.
- **`math/setup = mathml-AF`** — Instructs the LaTeX tagging engine to generate MathML and attach it as an Associated File to each formula tag rather than writing it into the PDF structure tree. The generated `.xml` MathML files are available in Overleaf's "Other logs and files" panel after compilation.
- **No `math/alt/use`** — No Alt text is generated on the formula tag.
- **`lang=en`** — See the [top-level README](../README.md#language-langen) for the reasoning behind using `en` rather than `en-US`.

## Test results summary

| Screen reader + PDF viewer | Result |
|---|---|
| NVDA with Adobe Acrobat Pro | ✅ Configurable math speech/braille; interactive expression exploring |
| JAWS with Adobe Acrobat Pro | ❌ Speaks raw MathML |
| NVDA with Firefox | ✅ Configurable math speech/braille; interactive expression exploring |
| JAWS with Firefox | ✅ Configurable math speech/braille; interactive expression exploring |
| NVDA or JAWS with Chrome/Edge | ❌ Math is skipped over; not read aloud |
| VoiceOver macOS (all viewers) | ❌ Speaks as gibberish / math skipped |

See the [full results table](../../index.html) for complete detail and test dates.

## Notes

JAWS with Adobe Acrobat Pro speaks raw MathML verbatim for AF-encoded math. This is a JAWS+Acrobat interoperability issue: Acrobat exposes the AF attachment in a way that JAWS reads as literal XML text rather than routing it through MathCAT. The same file works correctly with NVDA in Acrobat and with both screen readers in Firefox.

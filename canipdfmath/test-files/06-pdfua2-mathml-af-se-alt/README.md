# pdfua2-mathml-af-se-alt — Associated Files + Structure Elements + Alt text

**Overleaf project:** [pdfua2-mathml-af-se-alt](https://www.overleaf.com/read/pwdzngyftwwk#9871d1) (read-only)

This file tests **AF + SE + Alt text**: all three encoding methods are active simultaneously. MathML is embedded as an Associated File, written into the PDF tag tree as Structure Elements, *and* a plain-text alternative is auto-generated on the formula tag. This is the most complete encoding combination tested.

## Files

| File | Description |
|---|---|
| `main.tex` | LaTeX source |
| `pdfua2-mathml-af-se-alt.pdf` | Compiled PDF output |
| `latexmkrc` | Overleaf compilation configuration (shared across all six projects) |

## `\DocumentMetadata` configuration

```latex
\DocumentMetadata{
  lang=en,
  tagging=on,
  pdfstandard = {ua-2, A-4f},
  tagging-setup={
    math/setup = {mathml-AF, mathml-SE},
    math/alt/use = true
  }
}
```

**Key choices:**

- **`pdfstandard = {ua-2, A-4f}`** — `A-4f` is required here because the AF method embeds MathML as a file attachment on each formula object. See the [top-level README](../README.md#pdf-standards-pdfstandardua-2-and-pdfstandardA-4f).
- **`math/setup = {mathml-AF, mathml-SE}`** — Both AF and SE MathML encoding are active simultaneously.
- **`math/alt/use = true`** — Auto-generates a plain-text `Alt` attribute on the formula tag in addition to both MathML delivery channels.
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

Despite containing the richest encoding — AF, SE, and Alt text all present — this combination produces the same results as AF+Alt and SE+Alt in every tested environment. The `Alt` attribute suppresses MathML access in Acrobat regardless of how many MathML delivery channels are also present. Firefox continues to correctly route to MathML via MathCAT regardless of the `Alt` attribute.

The key finding from this combination is that **adding Alt text does not provide a safety net for environments where MathML fails** — it actively degrades the experience in environments where MathML would otherwise succeed (Acrobat with NVDA). The decision to include `math/alt/use = true` should therefore be made carefully, with an understanding that it trades MathML access in Acrobat for a static text fallback.

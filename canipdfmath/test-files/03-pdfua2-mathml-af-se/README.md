# pdfua2-mathml-af-se — Associated Files + Structure Elements

**Overleaf project:** [pdfua2-mathml-af-se](https://www.overleaf.com/read/yhsxdnfvfchj#b6fb41) (read-only)

This file tests **AF + SE**: MathML is both embedded as an Associated File and written into the PDF tag tree as Structure Elements. No Alt text is generated on the formula tag. This is the most redundant MathML-only encoding — it provides MathML via both delivery channels simultaneously.

## Files

| File | Description |
|---|---|
| `main.tex` | LaTeX source |
| `pdfua2-mathml-af-se.pdf` | Compiled PDF output |
| `latexmkrc` | Overleaf compilation configuration (shared across all six projects) |

## `\DocumentMetadata` configuration

```latex
\DocumentMetadata{
  lang=en,
  tagging=on,
  pdfstandard = {ua-2, A-4f},
  tagging-setup={
    math/setup = {mathml-AF, mathml-SE}
  }
}
```

**Key choices:**

- **`pdfstandard = {ua-2, A-4f}`** — `A-4f` is required here because the AF method embeds MathML as a file attachment on each formula object. See the [top-level README](../README.md#pdf-standards-pdfstandardua-2-and-pdfstandardA-4f).
- **`math/setup = {mathml-AF, mathml-SE}`** — Both encoding methods are active simultaneously. The LaTeX tagging engine generates MathML as an Associated File attachment *and* writes MathML Structure Elements into the tag tree for every formula.
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

Results are identical to AF-only for all tested environments. The presence of SE alongside AF did not resolve the JAWS+Acrobat raw MathML issue — Acrobat appears to expose the AF attachment preferentially to JAWS regardless of whether SE is also present. This suggests the problem lies in how JAWS and Acrobat negotiate which MathML delivery channel to use, rather than in the absence of a particular encoding.

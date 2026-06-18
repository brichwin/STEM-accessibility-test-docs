# PDF/UA-2 MathML Encoding Test Files

This directory contains the six LaTeX source files, compiled PDFs, and documentation used to generate the [PDF/UA-2 Math Encoding Test Results](../index.html). Each subdirectory corresponds to one encoding combination tested.

## Compilation environment

All six projects were compiled on Overleaf using the following settings:

| Setting | Value |
|---|---|
| Compiler | LuaLaTeX (via `lualatex-dev`) |
| TeX Live version | Rolling TeX Live (Overleaf Labs) |
| Compile mode | Normal |
| Stop on first error | On |

**Overleaf Labs** must be enabled to access the Rolling TeX Live version. The rolling image provides the latest LaTeX tagging project fixes ahead of the annual TeX Live release, which is important for MathML tagging support.

### The `latexmkrc` file

All six projects share the same `latexmkrc` file:

```perl
$max_repeat = 1;
$force_mode = 1;
$pdflatex='pdflatex-dev -synctex=1 -interaction=nonstopmode';
$lualatex='lualatex-dev -synctex=1 -interaction=nonstopmode';
```

**What each line does:**

- **`$max_repeat = 1`** — Tells `latexmk` to run the compiler only once rather than repeatedly until the output stabilizes. PDF tagging with the current LaTeX tagging project can produce false "rerun needed" signals; limiting to one pass avoids runaway compile loops on Overleaf.
- **`$force_mode = 1`** — Instructs `latexmk` to continue even if it encounters errors, equivalent to running in non-stop mode at the `latexmk` level. Combined with `-interaction=nonstopmode` on the engine itself, this ensures Overleaf produces a PDF rather than hanging on a non-fatal warning.
- **`$pdflatex='pdflatex-dev ...'`** — Overrides the PDFLaTeX engine with `pdflatex-dev`, the development/prerelease build that includes the latest LaTeX kernel changes. The `-synctex=1` flag enables source-to-PDF sync in the Overleaf editor; `-interaction=nonstopmode` suppresses interactive prompts.
- **`$lualatex='lualatex-dev ...'`** — Same override for LuaLaTeX. Since these projects use LuaLaTeX (required for MathML Structure Element tagging), this is the active rule. `lualatex-dev` carries the same prerelease kernel as `pdflatex-dev` and is recommended by the LaTeX Tagging Project for the most current MathML support.

> **Why `-dev` variants?** The `-dev` engines (`lualatex-dev`, `pdflatex-dev`) ship the development version of the LaTeX kernel (`latex-dev` package). When using Rolling TeX Live on Overleaf, this ensures you are running the absolute latest tagging code rather than the stable kernel bundled with that TeX Live snapshot.

---

## PDF standards: `pdfstandard=ua-2` and `pdfstandard=A-4f`

All six files declare `pdfstandard = {ua-2, A-4f}`. Here is what each means and why both are declared.

### `ua-2` — PDF/UA-2 (ISO 14289-2)

PDF/UA-2 is the current Universal Accessibility standard for PDFs. It is built on PDF 2.0 and provides native support for MathML as a first-class structure type. It is the standard most directly relevant to math accessibility and is what screen reader / PDF viewer combinations must support to render MathML correctly.

### `A-4f` — PDF/A-4f (ISO 19005-4, level f)

PDF/A is the archiving standard. The `-4` generation aligns with PDF 2.0 (the same base as PDF/UA-2). The `f` conformance level (for "files") permits embedded files — which is what makes the Associated File (AF) encoding method possible. Without `A-4f`, embedding a MathML file as an Associated File attached to the formula object would not be standards-conforming.

`A-4f` is strictly required only for the files that use AF encoding. It is declared in all six files for consistency; its presence in SE-only files is redundant but harmless — the PDF simply claims conformance to a standard that permits embedded files, whether or not any are present.

### Why `pdfversion=2` does not need to be set explicitly

When `pdfstandard=ua-2` (or `A-4f`) is declared, `\DocumentMetadata` automatically sets the PDF version to 2.0, because both of those standards require PDF 2.0. Writing `pdfversion=2` explicitly would be redundant.

---

## Language: `lang=en`

All six files use `lang=en` rather than `lang=en-US`. This is deliberate. `lang=en` is a valid BCP 47 tag meaning "English, no regional variant." When a screen reader or MathCAT encounters it, they fall back to the user's own configured locale for region-specific conventions — so an `en-GB` user hears math spoken with British English conventions (e.g. "bracket" for parenthesis) and an `en-US` user hears American English conventions. Setting `lang=en-US` would override that and impose American conventions on all users regardless of their locale. `lang=en` is therefore the correct choice for a document intended for a broad English-speaking audience.

---

## Encoding combinations at a glance

| # | Folder | Encoding | `math/setup` | `math/alt/use` | Overleaf project |
|---|---|---|---|---|---|
| 1 | `01-pdfua2-mathml-af` | AF only | `mathml-AF` | — | [pdfua2-mathml-af](https://www.overleaf.com/read/mqkqqkppggnh#972502) |
| 2 | `02-pdfua2-mathml-se` | SE only | `mathml-SE` | — | [pdfua2-mathml-se](https://www.overleaf.com/read/zghsqhpyybgd#0e4fdf) |
| 3 | `03-pdfua2-mathml-af-se` | AF + SE | `{mathml-AF, mathml-SE}` | — | [pdfua2-mathml-af-se](https://www.overleaf.com/read/yhsxdnfvfchj#b6fb41) |
| 4 | `04-pdfua2-mathml-af-alt` | AF + Alt text | `mathml-AF` | `true` | [pdfua2-mathml-af-alt](https://www.overleaf.com/read/trfqnkgwvxqv#8e07e6) |
| 5 | `05-pdfua2-mathml-se-alt` | SE + Alt text | `mathml-SE` | `true` | [pdfua2-mathml-se-alt](https://www.overleaf.com/read/fbjvjmzppdyj#618976) |
| 6 | `06-pdfua2-mathml-af-se-alt` | AF + SE + Alt text | `{mathml-AF, mathml-SE}` | `true` | [pdfua2-mathml-af-se-alt](https://www.overleaf.com/read/pwdzngyftwwk#9871d1) |

---

## Key findings

- MathML Structure Elements (SE) and Associated Files (AF) both produce fully accessible math output — configurable speech/braille with interactive expression navigation — when used with NVDA or JAWS in Firefox, and with NVDA in Adobe Acrobat Pro.
- When Alt text is present on the formula tag, Adobe Acrobat Pro (with both NVDA and JAWS) reads the static alt text string instead of processing the MathML. Firefox ignores the alt text and correctly routes to MathML.
- JAWS with Adobe Acrobat Pro does not correctly process AF-only or AF+SE encoding (speaks raw MathML). SE-only with JAWS in Acrobat used to work but appears to only produces character-by-character output in latest testing.
- PDFs rendered in Chrome and Edge regardless of screen reader or OS fail to provide MathML access.
- VoiceOver on macOS do not provide usable math access regardless of encoding combination or PDF viewer.
- VoiceOver on iOS has not yet been tested.

See the [full test results table](../index.html) for per-combination, per-environment detail.

# STEM Accessibility Test Documents

Various documents for testing the accessibility of reading systems, document 
compilers/converters, and assistive technologies when handling STEM content.

Maintained by Brian Richwine, [IU Assistive Technology and Accessibility Centers 
(ATAC)](https://atac.iu.edu), Indiana University.

## Contents

### [canipdfmath](./canipdfmath/) — Can I read math in a tagged PDF created from LaTeX?

Compatibility test results for MathML encoded in PDF/UA-2 documents, modeled after 
the [Can I Use](https://caniuse.com) format. Tests six combinations of MathML encoding 
methods (Associated Files, Structure Elements, and Alt text) across screen readers 
(NVDA, JAWS, VoiceOver macOS) and PDF viewers (Adobe Acrobat Pro, Firefox, Chrome, 
Edge, Preview).

- [View the test results page](https://brichwin.github.io/STEM-accessibility-test-docs/canipdfmath/)
- [Browse the LaTeX source files and documentation](./canipdfmath/test-files/)

Test files include source documents (LaTeX, etc.), compiled outputs (PDF), and 
written documentation of the test environment and results. Where applicable, 
read-only links to the original authoring environment (e.g. Overleaf) are provided 
so results can be independently reproduced.

## License

[BSD 3-Clause](./LICENSE) — test files and documentation are freely reusable with 
attribution.

# ES/TG Glossary

LaTeX glossary. Entries live in `content.tex`, layout in `main.tex`.

## Build

Requires a TeX distribution with LuaLaTeX (e.g. TeX Live, MacTeX).

```sh
latexmk -lualatex main.tex
```

Without latexmk: run `lualatex main.tex` twice (for "Page x of y").

## Deploy

Every push builds the PDF via GitHub Actions. Every push to `main` also creates the next version (`v1.0`, `v1.1`, …) as a GitHub release with the PDF.

```sh
git add -A
git commit -m "Describe the change"
git push origin main
```

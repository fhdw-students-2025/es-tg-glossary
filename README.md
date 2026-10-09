# ES/TG Glossary

LaTeX glossary. Entries live in `content.tex`, layout in `main.tex`.

## Adding entries

Add each entry to `content.tex` in alphabetical order:

```latex
\eintrag{ADC}[
  lang  = Analog-to-Digital Converter,
  dt    = Analog-Digital-Umsetzer (ADU),
  auch  = A2D,
  siehe = {DAC, IC},
]{Wandelt ein analoges Messsignal in ein digitales Signal um.}
```

The term and the explanation are required. All fields in `[…]` are optional, and the PDF only shows the fields you set:

| Field   | Meaning                       | Printed as                          |
| ------- | ----------------------------- | ----------------------------------- |
| `lang`  | long form of an abbreviation  | italic line below the term          |
| `dt`    | German translation            | "dt. X." before the explanation     |
| `auch`  | other names                   | "Auch: …"                           |
| `siehe` | related entries (comma list)  | "Siehe auch: …" as links            |
| `id`    | link name for duplicate terms | not printed (e.g. `id = ISA-Bus`)   |

An entry with no fields is just `\eintrag{Bus}{Gemeinsamer Übertragungsweg …}`.

If a value contains a comma, put it in braces: `auch = {A, B}`.

To link to another entry inside the explanation, write `\siehe{CMOS}`. It prints "CMOS" as a dark blue link. If the name doesn't match an entry, the PDF shows "??" and the build warns about an undefined reference.

## Build

Requires a TeX distribution with LuaLaTeX (e.g. TeX Live, MacTeX). BasicTeX also needs two extra packages:

```sh
sudo tlmgr install enumitem lastpage
```

```sh
latexmk -lualatex main.tex
```

Without latexmk: run `lualatex main.tex` twice (for "Page x of y" and the links).

## Deploy

Every push builds the PDF via GitHub Actions. Every push to `main` also creates the next minor version (`v2.0`, `v2.1`, …) as a GitHub release with the PDF and posts it to Discord.

```sh
git add -A
git commit -m "Describe the change"
git push origin main
```

### New major version

The major version is set by `MAJOR` in `.github/workflows/latex.yml`. To start a new major version, increase it (e.g. `2` → `3`) and push to `main`. That push is released as `v3.0`, and later pushes count up from there (`v3.1`, …).

```yaml
env:
  MAJOR: 3 # erhöhen, um eine neue Hauptversion (vN.0) zu beginnen
```

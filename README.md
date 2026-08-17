# CSV First Look

I have always had to deal with discovering the data I am dealing with before doing any analysis or deciding any Machine-Learning-related decisions. So I created this no-server tool that gives you a first read on any CSV or Excel file in seconds, paste data or drop a file, and it automatically infers column types, flags data-quality issues, and surfaces relationships between columns. Nothing leaves your browser; there's no upload, no server, no tracking.

**[Try it live →]** 
https://youssefali07.github.io/CSV-into-EDA-Tool/

## What it does

- **CSV and Excel support** — paste CSV text, or drop/upload a `.csv`, `.xlsx`, or `.xls` file. Multi-sheet workbooks get a sheet picker; single-sheet files skip straight to analysis.
- **Type inference** for every column — integer, float, boolean, date, categorical, or text — including columns that are *mostly* one type with a few stragglers (e.g. mostly numeric ages with a couple of typos), rather than silently falling back to plain text.
- **Data-quality flags**: constant columns, high-null columns, columns that look like an ID rather than a category, and statistical outliers.
- **Skew-aware outlier detection** — right-skewed columns (salary, price) are checked in log space so the natural high end isn't mistaken for anomalies.
- **Date column depth** — min/max range, a time-based histogram, and gap detection (e.g. flagging a 6-week hole in otherwise-daily data).
- **Relationships between columns** — numeric correlation and categorical functional dependencies (e.g. `city` reliably implying `country`), worded as observations, not causal claims.
- **Robust parsing** — auto-detects delimiter (comma, semicolon, tab, pipe) and file encoding (UTF-8 vs. Windows-1252) for CSV, strips a leading byte-order mark (common in Excel "CSV UTF-8" exports), disambiguates duplicate column headers, and takes an unbiased random sample rather than just the top of the file for very large datasets.
- **Export** — download the report as Markdown, or save it as a PDF via the browser's print dialog.
- **Dark mode** — respects your system preference on first visit, remembers your choice after that. Print/PDF output always stays light regardless.
- **Column search & sort** — filter columns by name, or sort by name, type, missing %, or how many issues each one has flagged.
- **Drag-and-drop upload**, alongside paste and click-to-browse. (Note: drag-and-drop of files isn't supported on iOS/mobile browsers — use the file picker there instead.)
- **Adaptive histograms** — bin count scales to each column's actual sample size and spread, instead of a fixed count that makes small columns look like noise.
- **Responsive layout** — works down to phone-width screens.

## Tech

Two files: `index.html` and `xlsx.full.min.js` (the [SheetJS](https://sheetjs.com) library, used only to parse `.xlsx`/`.xls` files). No build step. SheetJS is self-hosted rather than pulled from a CDN, so the tool still makes zero external requests except to Google Fonts — everything else, including all file parsing and analysis, runs entirely client-side.

## Why

Built as a practical exercise in exploratory data analysis tooling — the kind of first-look report you'd normally write ad hoc in a notebook, turned into something reusable.

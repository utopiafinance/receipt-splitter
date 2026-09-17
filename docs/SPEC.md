# Receipt Splitter — as-built spec

> Written 17 Sep 2026 by reading `index.html` (v4.0). It describes what the tool
> **does today**; it is not a plan. The tool's purpose has not yet been confirmed
> by Atiqah — see the brain page `finance-wiki/projects/payments-recon/receipt-splitter.md`.

## What it is

A single web page that turns bank payment-slip PDFs into individually named
receipt files, ready to drop into Google Drive. Everything runs in the browser:
no file is uploaded to any server.

## Two modes

| Mode | Input | What happens |
|---|---|---|
| **Split & Rename** | One or more bulk PDFs from a bank, one slip per page | Every page becomes its own PDF, named from the text on that page |
| **Rename Only** | PDFs that are already one slip each | Each file is renamed from its text, in a chosen slip format |

Results download together as one ZIP.

## What it reads from each slip

`extractInfo()` reads the page text and looks for:

- **Amount** — `Amount :` / `Transaction Amount :` followed by `MYR` or `RM`.
- **Date** — `Date :` or `Value Date :` as `DD Mon YYYY`, `DD/MM/YYYY`, `DD-MM-YYYY` or `YYYY-MM-DD`, normalised to `DD-MM-YYYY`.
- **Recipient's reference**, **bank reference**, **beneficiary** and **description** (e.g. Maybank "Debit Description").

## How files are named

**Split & Rename** (`buildFilename`), parts joined by the chosen separator (underscore, hyphen or space):

1. Optional prefix.
2. Field 1 — recipient's reference or bank reference (falls back to the other, then `UNKNOWN`).
3. Field 2 — `RM<amount>`, or nothing.

**Rename Only** (`buildRenameFilename`):

- **Refund slip:** `Refund_<order no>_RM<amount>.pdf` — order no from the description (Maybank) or recipient's reference (CIMB).
- **Supplier slip:** `<date>_<supplier>_<reference>_RM<amount>.pdf`.
- Missing parts become `NODATE`, `NOAMT`, `NOREF`, `NOSUPPLIER`.

Duplicate names get `_2`, `_3` … appended. A page with none of reference, amount
or beneficiary is skipped and counted as skipped.

## Built with

Plain HTML and JavaScript. Libraries from cdnjs: `pdf.js` 3.11 (read text),
`pdf-lib` 1.17 (split pages), `jszip` 3.10 (download ZIP).

## Files

- `index.html` — the tool (v4.0).
- `index (2).html` — an older copy (v2.0), kept as uploaded.

## Limits

- Only slips whose PDF contains real text work; a scanned image has no text to read.
- Field names are matched by English labels as they appear on Maybank and CIMB slips; other banks' wording may not match.
- The GitHub repository is **public** — never commit real slips or sample files.

# Receipt Splitter

A single-page browser tool ("v4.0 · Any Bank") for bank payment slips. Mode 1
splits a bulk multi-page PDF into one PDF per page and renames each from its
content (e.g. order/reference number + amount). Mode 2 renames PDFs that are
already separate, using a Refund slip or Supplier slip naming format. Output is
a ZIP with PDF and image folders ready for Google Drive. All processing happens
in the browser; nothing is uploaded to a server.

Cross-project patterns: `/Users/atiqahfattah/claude-projects/CLAUDE.md`.

## Status and where the truth lives
- Brain page: `/Users/atiqahfattah/claude-projects/finance-wiki/projects/payments-recon/receipt-splitter.md`
  (still marked unverified; its purpose line is an open question in
  `finance-wiki/99-open-questions.md` — the description above is read from the page itself)
- Repo: github.com/utopiafinance/receipt-splitter — **PUBLIC**
- Dormant: last commit April 2026, all "Add files via upload". No Vercel link.
- The planned bulk-payment design in Slip Bank Hub was to absorb this tool
  (memory `project_slip_bank_hub.md`).

## Stack
- Plain HTML/CSS/JS in one file, no build step
- CDN libraries: pdf.js 3.11.174, pdf-lib 1.17.1, JSZip 3.10.1

## Commands
None. Open `index.html` in a browser.

## Files
- `index.html` — current version (v4.0)
- `index (2).html` — older v2.0 copy

## Gotchas
- The repo is public: never commit real receipts, slips, customer names or amounts.
- Styling predates the brand CI (old `#2563EB` blue, JetBrains Mono). Bring it in
  line only if Atiqah asks for work on it.

## Docs
None yet — no spec or plan.

## Working rules
- Read the brain page first; confirm the tool is still wanted before building on it.
- Never commit secrets.
- After work: record lessons in `finance-wiki/lessons/` plus a Claude memory note,
  update the brain page, and keep the project pack complete — see
  `/Users/atiqahfattah/claude-projects/finance-wiki/projects/tooling/project-pack.md`.

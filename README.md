# Weekly cash view

Where's cash this week, who do I chase, and what do we owe each VAR?

A single static page that turns a Stripe invoice CSV export into a weekly cash view, a tiered chase list with copy-ready follow-ups, and line-by-line VAR payout statements. Everything runs in the browser. Files you load are parsed locally and never uploaded. There's no backend and nothing is stored.

It opens on fictional demo data (Contractor A to T, Partner A to C), labelled as such on every panel. Load your own export with **Load Stripe CSV**, or drag the file onto the page. **Download the demo CSV** in the footer shows the expected shape.

## Weekly cash
- Headline: collected this week, total outstanding, invoices to chase.
- Cash collected by week for the last 8 weeks, against the prior 7-week average.
- Billed vs collected by revenue stream (subscriptions, add-ons, partner).
- Aging buckets: 1–30, 31–60, 61–90 and 90+ days.
- Chase list sorted by amount × days overdue, with a drafted follow-up per tier: nudge (7+ days), firm (30+), escalate (60+).
- Any as-of date.

## VAR payouts
- Per-partner rules: base rate, tier threshold, rate above threshold, cap per period.
- Attributed revenue is rebuilt from invoices with a `partner` metadata column, or pasted/uploaded as CSV (`partner,customer,invoice,date,amount`).
- A statement per partner with the calculation shown line by line, plus CSV export.

## Method
- Void, draft and uncollectible invoices are excluded.
- Outstanding uses amount remaining, so part-paid invoices count only what's still owed.
- Figures are computed as of the selected date. Invoices created later are ignored. An invoice paid after that date counts as outstanding on it.
- Collected is amount paid, dated by paid-at. If the export has no paid-at column, the due date is used and the page says so.
- Column names are matched loosely (`Amount Due`, `amount_due`, `Total`, and so on). Stream comes from a `stream` metadata column if there is one, otherwise it's inferred from the description.

## Hosting
Static `index.html`, served by GitHub Pages from the root of `main`.

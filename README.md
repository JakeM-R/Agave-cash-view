# Invoice to cash

A single static page covering the money side of an ops seat: a weekly cash update for leadership, a chase list for the billing inbox, and a two-way partner ledger (remittances in, VAR rev-share out).

Everything runs in the browser. Files you load are parsed locally and never uploaded. There's no backend and nothing is stored.

It opens on fictional sample data in round numbers (Contractor A to T, VARs Partner A to C, paying partners D and E), labelled on every panel. The figures show the mechanics; they are not a guess at anyone's pricing. Load your own Stripe invoice export with **Load Stripe CSV**, or drag the file onto the page. **Download the demo CSV** in the footer shows the expected shape.

## Weekly cash
- Headline: collected this week, total outstanding, invoices to chase, with week-on-week changes.
- **Weekly note:** a plain-text update ready to paste into Slack or email. It covers collections against the weekly average, outstanding and overdue against last week, newly overdue invoices, chase-list invoices that got paid, partner remittances and payouts, and the top three risks with the next action on each.
- Cash collected by week for the last 8 weeks.
- Billed vs collected by revenue stream (subscriptions, add-ons, partners).
- Chase list for the billing inbox, sorted by amount × days overdue, with a strip showing overdue by age and a drafted follow-up per tier: nudge (7+ days), firm (30+), escalate (60+). Stripe's automatic reminders cover the first touch; these are the human follow-ups after that.

## Partners
Money in from partners and rev-share out to VARs, tracked separately. Rates, thresholds, caps, payment terms and attribution are all inputs; nothing assumes how a partner agreement is structured.
- **Remittances in:** expected vs received per partner and period (`partner,period,expected,received,received_date,reference`), with shortfalls from earlier periods carried until they're settled. Days-to-pay after period end is an input.
- **Rev-share out:** per-VAR rules (base rate, optional tier threshold and rate above it, optional cap per period) applied to attributed revenue (`partner,customer,invoice,date,amount`). Refunds go in as negative amounts and are clawed back from the period they land in.
- A payout statement per VAR with the calculation shown line by line, a mark-as-paid toggle, a partner-facing view you can print or save as PDF, and CSV export.

## Method
- Void, draft and uncollectible invoices are excluded.
- Outstanding uses amount remaining, so part-paid invoices count only what's still owed.
- Figures are computed as of the selected date. Week-on-week changes re-run the same numbers as of seven days earlier.
- Collected is amount paid, dated by paid-at. If the export has no paid-at column, the due date is used and the page says so.
- Remittances count as received only when dated on or before the as-of date, and fall due a set number of days after period end.
- Column names are matched loosely (`Amount Due`, `amount_due`, `Total`, and so on). Stream comes from a `stream` metadata column if there is one, otherwise it's inferred from the description.

## Hosting
Static `index.html`, served by GitHub Pages from the root of `main`.

# Complete Contact ERP — marketing assets

Source of truth for the HTML Automate2Scale builds and maintains for the
CCERP 90-Day Marketing Launch. Every file here is a **single self-contained
page** — all CSS and JavaScript inline, images embedded as data URIs, no build
step and no external dependencies except the Inter webfont from Google Fonts.

Download a file, open it in a browser, and it works. Paste it into a
GoHighLevel custom-HTML block and it works there too.

---

## Files

| File | What it is | Deployed at |
|---|---|---|
| `campaign-landing-page.v2026-10-19.html` | The campaign landing page. Hero, pain/outcome, platform, pricing tiers, plan comparison table, trust, single call to action. | Not yet published — pending Oscar's sign-off |
| `erp-fit-scorecard.v2026-10-15-B.html` | The ERP Fit & Efficiency Scorecard. 15 questions, scoring, tiered result, posts to GoHighLevel. | `go.ccerp.pro/erp-fit-scoreboard` — **live** |

Filenames carry their version. A new version gets a new file rather than
overwriting the old one, so what is live can always be compared against what is
being proposed.

---

## How the two pages fit together

The landing page does not capture anything. Its single call to action sends the
visitor to the scorecard, where the fifteen questions come first and the ask for
name and email comes at the end — once the visitor can see the result was worth
it. This was a deliberate change on 19 October: the landing page used to gate a
form in front of a visitor who had not answered anything yet.

Campaign attribution survives the hand-off. The landing page reads
`utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content` and
`gclid` from its own URL and appends them to the scorecard link, so a lead that
arrives from an ad still carries its source into the CRM.

---

## The scorecard's CRM connection

On submit, the scorecard posts a JSON payload of **43 fields** to a GoHighLevel
inbound webhook: contact details, the total out of 45, the tier band and label,
five section scores, every raw answer `q1`–`q15`, the rendered result copy, and
full UTM attribution. A form-encoded fallback fires if a browser blocks the JSON
request.

The six `result_*` fields carry the finished result copy — headline, lead
paragraph and three recommendations — so the result email in GoHighLevel can be
one template of plain merge tags rather than a three-way branch on tier band.
When the tier copy changes on this page, the email follows.

Each build announces itself in the browser console on load, e.g.
`CCERP Scorecard BUILD 2026-10-15-B — 43 fields`. Check that before debugging a
field that appears to be missing; it is usually an older build that is deployed.

---

## Open items

- **Trial and demo URLs.** Not yet supplied. No page currently links to either,
  so nothing is broken by their absence — but neither path exists yet.
- **The live scorecard is build 2026-10-15-B's predecessor.** The deployed page
  posts the original 37 fields. It needs republishing from the file here before
  the six `result_*` fields reach the CRM.
- **Landing page approval.** Not published anywhere yet.

---

## Conventions

- One page per file. No partials, no shared stylesheet, no bundler.
- All styles scoped under a single wrapper id (`#ccerp-lp`, `#ccerp-sc`) so a
  page can be pasted into a CMS without its styles leaking.
- No invented URLs. A link that has no destination yet is left out rather than
  pointed at `#`.
- No unevidenced claims. Anything that cannot be supported does not ship.

Maintained by Automate2Scale.

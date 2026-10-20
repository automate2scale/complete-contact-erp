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
| `ccerp-site.v2026-10-20.html` | **The site.** One file, two views: the landing page, and the ERP Fit Scorecard at `#scorecard`. | `go.ccerp.pro/erp-fit-scoreboard` |
| `loader-ccerp-site.html` | The GoHighLevel snippet that loads the file above. One paste, both views. | — |
| `landing-page.v2026-10-20.html` | The landing page on its own. Kept as the split version. | — |
| `scorecard.v2026-10-20.html` | The scorecard on its own. Kept as the split version. | — |

Filenames carry their version. A new version gets a new file rather than
overwriting the old one, so what is live can always be compared against what is
being proposed.

---

## One file, two views

`ccerp-site.v2026-10-20.html` holds both pages. The router reads the URL hash:
`#scorecard` shows the questionnaire, anything else shows the landing page.
One file to deploy, one snippet to paste, two pages to the visitor.

**Why routing rather than one long scroll.** Marketing content and a fifteen
question assessment are two different jobs. A visitor arriving cold reads the
pitch; a visitor arriving from an email that promised an assessment should land
on the questions, not scroll past the pitch to find them — which a deep link to
`#scorecard` gives you for free.

**The order inside the assessment is the point.** Questions first, name and
email at the end, once the visitor can see the result was worth it. The page
used to gate a form in front of someone who had not answered anything. Oscar's
review caught it and he was right.

**Attribution needs no hand-off.** A hash change does not touch the query
string, so `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`,
`utm_content` and `gclid` stay on the URL and the scorecard reads them straight
off `window.location.search`. Tested, not assumed.

The two split files are kept for reference. The routed file is what deploys.

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
- **The result buttons are hidden, not broken.** The trial and demo URLs do not
  exist, so those two buttons on the result panel hide themselves rather than
  rendering links that go nowhere. They reappear the moment the URLs are set.
- **Oscar has not signed off on the marketing copy.** The questionnaire half is
  approved and live; the landing half is not.

---

## Conventions

- One page per file. No partials, no shared stylesheet, no bundler.
- All styles scoped under a single wrapper id (`#ccerp-lp`, `#ccerp-sc`) so a
  page can be pasted into a CMS without its styles leaking.
- No invented URLs. A link that has no destination yet is left out rather than
  pointed at `#`.
- No unevidenced claims. Anything that cannot be supported does not ship.

Maintained by Automate2Scale.

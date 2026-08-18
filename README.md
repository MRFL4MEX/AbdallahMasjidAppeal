# Abdullah Masjid Building Appeal — website

Single-page fundraising site for **Abdullah Masjid, Hayes Welfare Association**
(registered charity 1186145), raising funds to complete the purchase of the
building on Waltham Avenue and clear the debt held against it.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The entire website. One self-contained file — HTML, CSS and JavaScript together. |
| `launch.json` | Config for previewing the site locally (see below). Not part of the website. |

There is no build step, no framework and no backend. Upload `index.html` to any
web host and it works immediately. The only external requests it makes are to
Google Fonts, and to Google Maps if a visitor taps the map link.

---

## ⚠️ Before this goes live

### 1. Switch off the demonstration data

**The donor count and the "recent contributions" strip are invented.** They are
there so the trustees can see how the finished page looks. While they are
switched on, red DEMO warnings appear on the page.

In the `<script>` block near the bottom of `index.html`, find:

```js
demo: true,
```

Change it to `demo: false`. The donor count and the whole contributions strip
disappear, along with the warnings.

The real figures live in separate fields (`donors` and `recent`), which are
empty by default — so switching the flag off **cannot** accidentally publish the
invented numbers. Fill those in only when you have genuine figures.

> A registered charity must not publish invented donation figures. This is the
> one item on this list that is not merely cosmetic.

### 2. The two numbers you will change most often

Also in the `<script>` block, near the top:

```js
const AMOUNT_RAISED = 300000;      // raised so far, in pounds
const TARGET_AMOUNT = 1500000;     // the appeal target, in pounds
```

Digits only — no pound sign, no commas. Changing `AMOUNT_RAISED` updates every
progress figure on the page at once: the headline total, the bar, the
percentage, "Remaining", the milestone markers, the square-metre count, the gold
tiles in the floor plan, and the sticky bar at the bottom of the screen.

### 3. Remaining placeholders

Search `index.html` for **`TRUSTEES:`** to find each one.

- **Prayer timetable** — the five daily times are dashes awaiting confirmation.
  Both Jummah times (13:30 and 14:30) are already correct.
- **GoCardless link** — paste your URL into `CONFIG.links.goCardlessMonthly`.
  The dashed placeholder box turns itself into a working button automatically,
  and the "Give monthly" button starts pointing at GoCardless instead of at the
  Ways to give section.
- **Open Graph URL and image** — replace `REPLACE-WITH-YOUR-DOMAIN` in the two
  `<meta>` tags near the top. The image should be 1200×630px. This is the
  picture people see when the link is shared on WhatsApp, so it matters.
- **Share URL** — set `CONFIG.share.url` to the live web address once uploaded.
  Left empty, the page shares whatever address the visitor happens to be on.
- **Photograph** — the "Our story" tab has a note where a photo of the building
  should go.
- **Milestones** — `CONFIG.milestones` holds sensible defaults, *not* confirmed
  figures. Change them to match the real stages of your purchase agreement.

### 4. Verified details already in the page

Charity number 1186145 · 07742 754 383 ·
hayeswelfareassociation@gmail.com · Waltham Avenue, Hayes, Middlesex, UB3 1TF ·
Lloyds Bank, sort code 30-98-97, account 63692262 ·
PayPal donate button `PNT8FEJPGMKSW`

---

## Editing the donation amounts

`CONFIG.giving` holds the preset buttons:

```js
once:    { presets: [10, 50, 100, 250, 1000], suggested: 100, ... },
monthly: { presets: [5, 10, 20, 50, 100],     suggested: 20,  ... }
```

**Keep each list at five.** Five presets plus the "Other" button fills exactly
two rows of three on a phone. A sixth leaves one button stranded alone on a
third row, and squeezes the "Suggested" tag until it overflows.

`CONFIG.impact` holds the line of text shown under the amount as it changes.

---

## Previewing it locally

The site is a plain file, so you can open `index.html` in a browser directly.
But two things only work when it is served over `http://`, not `file://`:

- the copy-to-clipboard buttons on the bank details
- the share links pick up a real web address

To serve it locally, from this folder:

```
python3 -m http.server 4173
```

Then open `http://localhost:4173`.

`launch.json` does the same thing automatically inside Claude Code. If you move
this folder, update the path inside it.

---

## Notes on how it is built

- **Accessibility** — the page is checked against WCAG AA contrast across every
  interactive state, is fully keyboard navigable (including the square-metre
  grid, which uses arrow keys, and the sideways contributions strip), and
  respects `prefers-reduced-motion`.
- **Body text never drops below 16px.** A significant part of this audience is
  over 50. Tap targets are 44px or larger.
- **No personal data is collected on the page.** Every payment hands off to
  PayPal or GoCardless, which handle compliance.
- **The square-metre grid** renders 203 tiles, each standing for eight of the
  1,624 square metres, rather than 1,624 separate elements — so it stays fast on
  a phone. The proportion filled is derived from `AMOUNT_RAISED / TARGET_AMOUNT`.
- **Donor names are initials only.** Donors have not consented to be listed by
  full name.

# TradeData — Landing Page

Conversion landing page for **TradeData** (verified trade data for sales teams) at
**https://tradedata.ai2eo.com/**.

Current pilot product: **JB-SG Food Trader List** — 100 verified records, $49 one-time.

Flow: landing page → free 10-row sample → $49 purchase → manual CSV delivery within 24h.

Brand hierarchy: **TradeData** = brand · **JB-SG** = current market ·
**food traders** = current vertical · **100 verified records** = current pilot.

## Deploy

Single static file (`index.html`), zero dependencies, no build step.

- Push `index.html` + `README.md` to GitHub, import the repo in Vercel,
  deploy with default static settings, then attach the `tradedata.ai2eo.com` domain
  to the project (canonical + OG URL are already set to it).

## Configuration

All settings live in the `CONFIG` object at the top of the inline `<script>` —
no other code changes needed:

```js
const CONFIG = {
  PILOT_PAYMENT_URL: "",              // Wise / PayNow / bank link. Empty = mailto fallback
  CONTACT_EMAIL: "tradedata@ai2eo.com",
  SAMPLE_SHEET_URL: ""                // View-only Google Sheet with the 10-row sample
};
```

Set these three values before launch. No fake addresses: if a value is empty,
the page falls back to email delivery messaging instead of a dead link.

## Analytics

Conversion events are pushed to `window.dataLayer` (attach GA/Plausible later,
nothing loaded by default):

- `sample_cta_click` — any "Get 10 Free Rows" click (`cta` label included)
- `sample_form_start` — first field focus
- `sample_form_submit` — valid submission
- `purchase_cta_click` — any $49 CTA click

## Notes

- No login, dashboard, billing, or backend. Sample form posts via Formspree
  (`https://formspree.io/f/mljellvo` → `info@ai2eo.com`) with AJAX, keeping the
  on-page success state. Requests are also stored in `localStorage`
  (`jbsg_sample_request`) as a backup.
- Sample table rows are illustrative previews of the record structure,
  not real customer data. No fake testimonials or user counts on the page.
- Offer constants (do not change without updating the sprint doc):
  100 verified records · $49 one-time · 14-day bounce replacement ·
  20 fresh rows within 14 days · 24h manual delivery · 10-row free sample.

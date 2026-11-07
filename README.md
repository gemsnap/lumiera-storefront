# LUMIÈRA Clinical — storefront

Single-file storefront for the LUMIÈRA Pro 8-colour LED face & neck mask, built in the
editorial commerce style of CurrentBody: white canvas, monochrome type, full-bleed studio
product photography, tight uppercase micro-labels and black pill CTAs.

## What's in here

| File | Purpose |
| --- | --- |
| `index.html` | The whole storefront: markup, CSS and JavaScript inlined (no build step, no dependencies beyond Google Fonts). |
| `README.md` | This file. |

## Pages / views

- **Home** — hero, trust marquee, four technology tiles (wavelength entry points), bestsellers
  grid, results with the eight-week timeline, interactive 8-mode selector, science, bundle
  picker, reviews, journal, newsletter.
- **Product** (`/#product`) — gallery, variant picker (Essential 249 € / Face & Neck 279 € /
  Twin Ritual 449 €), delivery estimate, accordions (box, specs, how to use, shipping & returns),
  FAQ and related products.
- **Cart drawer, checkout and confirmation** — persistent cart in `localStorage`, email/address
  validation, order reference and ETA, order history behind the account icon.
- **Overlays** — search, mobile menu, shipping/returns/orders/about/contact/legal panels.

## Editing

Everything content-driven lives in the `<script>` block near the bottom of `index.html`:

- `PRODUCTS` — names, prices, compare-at prices, ratings, reviews, copy, gallery images.
- `MODES` — the eight wavelengths, their nm values, accent colours and body copy.
- `REVIEWS` / `RATING_DIST` — review cards and the star distribution bars.
- `FAQ` — product-page questions.
- `PANELS` — the text of every policy/support panel.

Images are remote and can be swapped for your own CDN URLs in `PRODUCTS` and in the
`GALLERY` array.

## Commerce status

This build is a front-end demo: the cart and checkout are real (validation, totals, order
references, order history) but **no payment is processed and no order is transmitted**. To go
live, point the checkout's `placeOrder()` at a payment provider (Stripe Checkout, Shopify Buy
Button, or a Base44 backend function) and replace the policy copy with your own legal text.

## Deploy

Static site, no build. Push the folder to GitHub and enable Pages (Settings → Pages → Deploy
from branch → `main` / root), or drop `index.html` on any static host (Netlify, Vercel,
Cloudflare Pages, S3).

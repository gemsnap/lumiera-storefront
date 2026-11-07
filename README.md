# LUMIÈRA Clinical — storefront

Single-file storefront for the LUMIÈRA Pro LED face & neck mask, built as a structural clone of
CurrentBody.com: monochrome type, square buttons, white canvas, full-bleed studio photography,
wavelength colour bar and a long-form product page.

Live: https://gemsnap.github.io/lumiera-storefront/
Product: https://gemsnap.github.io/lumiera-storefront/#product
Checkout: https://gemsnap.github.io/lumiera-storefront/#checkout

## Structure

Everything ships as one `index.html` (HTML + CSS + JS, no build step, no dependencies).

- `#home` — editorial landing page: hero, wavelength tiles, bestsellers, results, mode selector, bundles, reviews, journal.
- `#product` — CurrentBody-style product page: gallery with thumbnails, claims, "Pick your product" variant cards,
  price + Klarna split, add to basket, payment icons, perks, accordions, wavelength bar, USP marquee, our opinion,
  genuine results, clinical evidence by wavelength, how to use, four presets, press, expert opinion, in the box,
  awards, UGC grid, reviews with histogram and filters, FAQ, journal, support, related products, sticky buy bar.
- `#checkout` — Shopify-style checkout: express wallet buttons, contact, delivery, shipping method, card / Klarna /
  PayPal, billing address, live order summary with discount codes and totals, Shopify-style thank-you page.

## Editing content

All copy is data at the bottom of `index.html`:

| What | Where |
| --- | --- |
| Products, prices, what's in the box | `PRODUCTS` object |
| Gallery images and captions | `GALLERY` array |
| Reviews | `REVIEWS` + `MORE_REVIEWS` arrays, `HIST` for the rating histogram |
| FAQ | `FAQ` array |
| Wavelengths, modes | `MODES` array |
| Legal / policy panels | `PANELS` object |
| Delivery windows | `deliveryWindow()` |

Discount codes live in `bindCheckout()`: `LUMIERA10` (10%), `WELCOME` (5%), `PROTOCOL` (15%).

## Turning on Stripe

Payments are not live. The checkout validates, calculates totals and shows an order confirmation, but no
card is charged and nothing ships.

To take real payments with Stripe Checkout:

1. Create a Stripe product and price for each variant, then a Payment Link or Checkout Session per variant.
2. In `index.html`, find the block marked `CHECKOUT · Shopify-style flow, Stripe hand-off` and set:

```js
const STRIPE_ENABLED = true;
const STRIPE_LINKS = {
  pro:       'https://buy.stripe.com/...',   // Face & Neck Set, 279 €
  essential: 'https://buy.stripe.com/...',   // Essential Mask, 249 €
  twin:      'https://buy.stripe.com/...'    // Twin Ritual Set, 449 €
};
```

The "Pay now" button and the express wallet buttons then redirect to Stripe with the customer's email,
a `client_reference_id` order reference and the EUR locale. Multi-item carts need a Checkout Session created
on a server rather than a static Payment Link.

## Deploying

GitHub Pages serves `main` from the repository root. Push to `main` and the site updates in about a minute:

```bash
git add index.html && git commit -m "update storefront" && git push
```

## Notes

- Product imagery for this build is illustrative. Replace with your own photography before going live,
  and replace the before/after and clinical figures with results from studies you can cite: publishing
  unsubstantiated efficacy claims is illegal in the EU and the UK.
- Prices are in EUR and include VAT.

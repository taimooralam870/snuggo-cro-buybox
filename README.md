# Snuggo: mobile hero and buy box

Two versions of the same design:

- `shopify/`: the real build: two Online Store 2.0 sections and a product template, all editable in the theme editor.
- `prototype/index.html`: a static copy for quick review on a phone (prices fixed in HTML).

## Install the Shopify section

Built and tested on a dev store running Horizon. It has no theme dependencies, so it also works on Dawn or any Online Store 2.0 theme.

1. Copy `shopify/sections/snuggo-buybox.liquid` and `shopify/sections/snuggo-details.liquid` into your theme's `sections/` folder.
2. Copy `shopify/snippets/snuggo-icon.liquid` into `snippets/`, and `shopify/templates/product.snuggo.json` into `templates/`.
3. In the dev store, create the product with two variants, in this order:
   - `One Snuggo`: price 199, compare-at 299
   - `Two Snuggos`: price 349, compare-at 598
   Upload the product images (and the demo video, if you have one).
4. In the product admin, set the theme template to `snuggo`. The template already holds
   the buy box and the details section (how it works, what's in the box, parent FAQ).
5. Preview: `shopify theme dev --store <your-store>.myshopify.com`, or push with
   `shopify theme push --unpublished` and share the preview link.

## Files

- `sections/snuggo-buybox.liquid`: gallery, price, offer, pack picker, add to cart, trust row, sticky bar
- `sections/snuggo-details.liquid`: how it works, what's in the box, parent FAQ
- `snippets/snuggo-icon.liquid`: the three trust icons (inline SVG)
- `templates/product.snuggo.json`: product template that uses both sections

## How it works

- Prices, compare-at prices, Afterpay split and per-unit price all come from variants
  through the `money` filter. Nothing is hardcoded.
- Each "Pack option" block points to a variant by position (1 = first variant).
- Add to cart is Shopify's native `{% form 'product' %}`, so Shopify's Meta and Google
  channel events fire the same way they do on the current page.
- The offer line hides itself after the end date set in the theme editor.
- The sticky add-to-cart bar appears on mobile once the main button scrolls off screen.
- No libraries. Under 60 lines of vanilla JS, first image loads eagerly, the rest lazily.

## Editable in the theme editor

Badge, headline, subheading, toy note, rating text and link, demo video and caption,
offer line and end date, pack label, instalment line, button label, delivery line,
setup note, colours, pack options (blocks) and up to 3 trust items (blocks).

The rating line stays hidden until it's filled in. It should only ever show real reviews.

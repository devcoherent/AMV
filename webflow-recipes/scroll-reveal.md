# Scroll Reveal

Site-wide scroll animation for pages that do not use the legacy `slide-in-*` wrapper pattern.
Same motion as `slide-in-bottom`: 100px up + fade, 1s, outQuart. No wrapper divs and no extra
classes are needed in the Designer; the pages and elements are listed in the code.

## Where it is applied

Site settings > Custom code (added 2026-11-17):

- **Head code**: the "Scroll Reveal (setup)" `<script>`. Lists the pages (`PAGES`) and the
  elements (`ITEMS`), hides them before first paint and defines the animation.
- **Footer code**: the "Scroll Reveal (observer)" `<script>`. Reveals items as they scroll into view.

The current code lives in the site custom code; read it from there before editing.

## Pages using it

Transmission Delivery, Authorized Distributor, Systems Design & Integration,
Managed Studio Services, Equipment Sales, Custom Engineering & Fabrication, About AMV.
A page is matched by its section class (`.section_transmission`, `.section_distributor`,
`.section_systems`, `.section_managed`, `.section_sales`, `.section_custom`, `.section_about`).

Home, Mobile, Equipment Rentals and the two template pages (Mobile Units, Studios) still use the
legacy `slide-in-*` classes. Production Spaces (`/stage`) has no scroll animation yet.

## How it behaves

- Items that enter the screen together are revealed one after another, 100ms apart (max 700ms).
- An item inside another item is not animated on its own; it moves with its parent.
- The hero image slides in from the right; everything else comes from below.
- Items are hidden with opacity only and animated on reveal. Do not hide them with a transform:
  the hero has `overflow: hidden`, which clips shifted items so they are never detected.
- "Reduce motion" visitors, browsers without `:has()` and a failed script all end with the content
  simply visible (there is a 5s safety timer).

## Checking a page after it changes

When a page's structure is edited, new blocks may fall outside `ITEMS` and stay un-animated
(this happened to the Custom Engineering contact block, fixed 2026-11-24 by adding
`.contact-split_component`). Compare the page's blocks against `ITEMS` and add the missing selector.

## To change it

- **New page**: add its section class to `PAGES` in the head script.
- **New element type**: add its selector to `ITEMS` in the head script.
- **Remove**: delete both "Scroll Reveal" script blocks.

## Hover animations added the same day (Designer classes, no code)

- Card images zoom 5% and brighten on hover (600ms): `feature-card_image`, `photo-strip_image`,
  `service-card_image`, `mobile-detail_gallery-image` (same as the existing `gallery_image`).
  `photo-strip_image` and `service-card_image` sit in a clipping wrapper
  (`photo-strip_image-wrapper`, `service-card_image-wrapper`) so the zoom stays inside the image box.
- `text-style-link`: colour fades to Link/secondary on hover (300ms).
- `manufacturer_card`: border colour + shadow on hover (300ms), like the Home service cards.
- `button`, `footer_link`: 300ms colour transitions.

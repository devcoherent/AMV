# Tab Open Slide-In

Slide-in animation for content inside Webflow tab panes that are hidden on page load.

## Why

The site's scroll animations are legacy interactions bound to the `slide-in-bottom-*` /
`slide-in-left-*` / `slide-in-right-*` classes (number = delay in ms). On a hidden tab pane
they fire while the pane is still hidden, so nothing is seen when the tab is opened.
This CSS replays the same motion (100px up + fade, 1s, outQuart) every time a pane becomes active.

## Where it is applied

- Mobile Units Template page > Page settings > Custom code > Head (Spec Sheets and Floor Plans tabs). Code below.
- Studios Template page > Page settings > Custom code > Head (Tech Specs and Gallery tabs). Code in the "Studios Template version" section.

## Code

```html
<style>
/* Tab-open animation for the Spec Sheets and Floor Plans tabs.
   Same motion as the site's slide-in-bottom interactions (100px up + fade, 1s, outQuart).
   Plays every time a tab pane becomes active. Scroll interactions cannot do this
   because these panes are hidden on page load. */
@media (prefers-reduced-motion: no-preference) {
  @keyframes amv-tab-slide-in {
    from { opacity: 0; transform: translate3d(0, 100px, 0); }
    to { opacity: 1; transform: none; }
  }
  .w-tab-pane.w--tab-active .spec-sheet_title,
  .w-tab-pane.w--tab-active .spec-sheet_component > .text-size-regular,
  .w-tab-pane.w--tab-active .spec-sheet_group,
  .w-tab-pane.w--tab-active .spec-sheet_download,
  .w-tab-pane.w--tab-active .floor-plan_header,
  .w-tab-pane.w--tab-active .floor-plan_card,
  .w-tab-pane.w--tab-active .floor-plan_component > .margin-top-small {
    animation: amv-tab-slide-in 1s cubic-bezier(0.165, 0.84, 0.44, 1) 200ms both;
  }
  .w-tab-pane.w--tab-active .spec-sheet_component > .text-size-regular,
  .w-tab-pane.w--tab-active .floor-plan_card:nth-child(1) { animation-delay: 300ms; }
  .w-tab-pane.w--tab-active .floor-plan_card:nth-child(2) { animation-delay: 400ms; }
  .w-tab-pane.w--tab-active .floor-plan_card:nth-child(3) { animation-delay: 500ms; }
  .w-tab-pane.w--tab-active .floor-plan_component > .margin-top-small { animation-delay: 600ms; }
  /* Spec sheet groups animate one by one, row by row; the right column trails by 50ms. */
  .w-tab-pane.w--tab-active .spec-sheet_group:nth-child(1) { animation-delay: 400ms; }
  .w-tab-pane.w--tab-active .spec-sheet_group:nth-child(2) { animation-delay: 500ms; }
  .w-tab-pane.w--tab-active .spec-sheet_group:nth-child(3) { animation-delay: 600ms; }
  .w-tab-pane.w--tab-active .spec-sheet_group:nth-child(4) { animation-delay: 700ms; }
  .w-tab-pane.w--tab-active .spec-sheet_group:nth-child(n+5) { animation-delay: 800ms; }
  .w-tab-pane.w--tab-active .spec-sheet_column:nth-child(2) .spec-sheet_group:nth-child(1) { animation-delay: 450ms; }
  .w-tab-pane.w--tab-active .spec-sheet_column:nth-child(2) .spec-sheet_group:nth-child(2) { animation-delay: 550ms; }
  .w-tab-pane.w--tab-active .spec-sheet_column:nth-child(2) .spec-sheet_group:nth-child(3) { animation-delay: 650ms; }
  .w-tab-pane.w--tab-active .spec-sheet_column:nth-child(2) .spec-sheet_group:nth-child(4) { animation-delay: 750ms; }
  .w-tab-pane.w--tab-active .spec-sheet_column:nth-child(2) .spec-sheet_group:nth-child(n+5) { animation-delay: 850ms; }
  .w-tab-pane.w--tab-active .spec-sheet_download { animation-delay: 900ms; }
}
</style>
```

To reuse on another page, add the selectors of that page's tab content to the lists above.

## Studios Template version

Added 2026-11-17. Spec cards and gallery items animate one by one.

```html
<style>
/* Tab-open animation for the Tech Specs and Gallery tabs (see recipe "Tab Open Slide-In").
   Same motion as the site's slide-in-bottom interactions (100px up + fade, 1s, outQuart).
   Plays every time a tab pane becomes active; these panes are hidden on page load,
   so scroll interactions cannot animate them. Cards and gallery items animate one by one. */
@media (prefers-reduced-motion: no-preference) {
  @keyframes amv-tab-slide-in {
    from { opacity: 0; transform: translate3d(0, 100px, 0); }
    to { opacity: 1; transform: none; }
  }
  .w-tab-pane.w--tab-active .spec-sheet_component > .hero_accent-line,
  .w-tab-pane.w--tab-active .spec-sheet_component > .heading-style-h2,
  .w-tab-pane.w--tab-active .spec-sheet_component > .text-size-regular,
  .w-tab-pane.w--tab-active .stage-detail_spec-card,
  .w-tab-pane.w--tab-active .stage-detail_specs-footer,
  .w-tab-pane.w--tab-active > .hero_accent-line,
  .w-tab-pane.w--tab-active > .heading-style-h2,
  .w-tab-pane.w--tab-active > .text-size-regular,
  .w-tab-pane.w--tab-active .gallery_item {
    animation: amv-tab-slide-in 1s cubic-bezier(0.165, 0.84, 0.44, 1) 200ms both;
  }
  .w-tab-pane.w--tab-active .spec-sheet_component > .heading-style-h2,
  .w-tab-pane.w--tab-active > .heading-style-h2 { animation-delay: 300ms; }
  .w-tab-pane.w--tab-active .spec-sheet_component > .text-size-regular,
  .w-tab-pane.w--tab-active > .text-size-regular { animation-delay: 400ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(1),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(1) { animation-delay: 500ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(2),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(2) { animation-delay: 580ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(3),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(3) { animation-delay: 660ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(4),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(4) { animation-delay: 740ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(5),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(5) { animation-delay: 820ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(6),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(6) { animation-delay: 900ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(7),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(7) { animation-delay: 980ms; }
  .w-tab-pane.w--tab-active .stage-detail_spec-card:nth-child(n+8),
  .w-tab-pane.w--tab-active .gallery_item:nth-child(n+8),
  .w-tab-pane.w--tab-active .stage-detail_specs-footer { animation-delay: 1060ms; }
}
</style>
```

## Template page pattern

Both template pages (Mobile Units, Studios) use the same setup:

- Hero and Overview tab: each element sits in a wrapper div with `slide-in-bottom-200` ... `-700` (number = delay).
- Tab links: `stage-detail_tab-link` + `slide-in-bottom-200 / 300 / 400` stacked on the link.
- Hero image: `background-image` + `slide-in-right-400`. Overview floor plan: `stage-detail_floor-plan` + `slide-in-bottom-500`.
- Hidden tabs: the CSS in this recipe.

## Notes

- Tab links cannot be wrapped in a div (Webflow tabs break), so on tab links and images the
  `slide-in-*` class is stacked directly on the element instead of on a wrapper div.

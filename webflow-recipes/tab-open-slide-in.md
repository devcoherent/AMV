# Tab Open Slide-In

Slide-in animation for content inside Webflow tab panes that are hidden on page load.

## Why

The site's scroll animations are legacy interactions bound to the `slide-in-bottom-*` /
`slide-in-left-*` / `slide-in-right-*` classes (number = delay in ms). On a hidden tab pane
they fire while the pane is still hidden, so nothing is seen when the tab is opened.
This CSS replays the same motion (100px up + fade, 1s, outQuart) every time a pane becomes active.

## Where it is applied

Mobile Units Template page > Page settings > Custom code > Head
(Spec Sheets and Floor Plans tabs).

## Code

```html
<style>
@media (prefers-reduced-motion: no-preference) {
  @keyframes amv-tab-slide-in {
    from { opacity: 0; transform: translate3d(0, 100px, 0); }
    to { opacity: 1; transform: none; }
  }
  .w-tab-pane.w--tab-active .spec-sheet_title,
  .w-tab-pane.w--tab-active .spec-sheet_component > .text-size-regular,
  .w-tab-pane.w--tab-active .spec-sheet_column,
  .w-tab-pane.w--tab-active .spec-sheet_download,
  .w-tab-pane.w--tab-active .floor-plan_header,
  .w-tab-pane.w--tab-active .floor-plan_card,
  .w-tab-pane.w--tab-active .floor-plan_component > .margin-top-small {
    animation: amv-tab-slide-in 1s cubic-bezier(0.165, 0.84, 0.44, 1) 200ms both;
  }
  .w-tab-pane.w--tab-active .spec-sheet_component > .text-size-regular,
  .w-tab-pane.w--tab-active .floor-plan_card:nth-child(1) { animation-delay: 300ms; }
  .w-tab-pane.w--tab-active .spec-sheet_column:nth-child(1),
  .w-tab-pane.w--tab-active .floor-plan_card:nth-child(2) { animation-delay: 400ms; }
  .w-tab-pane.w--tab-active .spec-sheet_column:nth-child(2),
  .w-tab-pane.w--tab-active .floor-plan_card:nth-child(3) { animation-delay: 500ms; }
  .w-tab-pane.w--tab-active .spec-sheet_download,
  .w-tab-pane.w--tab-active .floor-plan_component > .margin-top-small { animation-delay: 600ms; }
}
</style>
```

To reuse on another page, add the selectors of that page's tab content to the lists above.

## Notes

- Tab links cannot be wrapped in a div (Webflow tabs break), so on tab links and images the
  `slide-in-*` class is stacked directly on the element instead of on a wrapper div.

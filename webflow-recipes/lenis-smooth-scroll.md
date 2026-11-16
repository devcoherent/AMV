# Lenis Smooth Scroll

Smooth wheel scrolling for the whole site with Lenis 1.3.27, set up so the existing animations keep working.

**Status:** applied site-wide on 2026-11-16 (head + footer custom code) and tested on the published staging site.

## Why it is safe with the site's animations

- Lenis moves the real page scroll (no transform on the page), so the legacy `slide-in-*` scroll interactions, the sticky navbar, the sticky tab menu and the sticky Key Features column behave as before.
- The mobile menu and the gallery lightbox pause Lenis while they are open.
- Lenis turns itself off for visitors with "reduce motion" enabled, and touch scrolling stays native.

## How to apply

Site settings > Custom code.

**Head code** (add below what is already there):

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/lenis@1.3.27/dist/lenis.css">
```

**Footer code:**

```html
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.27/dist/lenis.min.js"></script>
<script>
(function () {
  if (typeof Lenis === 'undefined') return;

  var nav = document.querySelector('.nav_component');
  var lenis = new Lenis({
    autoRaf: true,          // Lenis runs its own animation loop
    lerp: 0.07,             // smoothness: lower = smoother/slower (0.05-0.12 is a good range)
    wheelMultiplier: 1,     // scroll speed per wheel step
    anchors: { offset: nav ? -nav.offsetHeight : 0 } // smooth #anchor links, stop below the sticky navbar
  });
  window.amvLenis = lenis;

  // Keep GSAP ScrollTrigger (new Webflow Interactions) in sync, if a page uses it.
  if (window.ScrollTrigger) lenis.on('scroll', window.ScrollTrigger.update);

  // Areas that scroll on their own: let them scroll natively.
  document.querySelectorAll('.w-nav-menu, [data-unit-lightbox="root"]').forEach(function (el) {
    el.setAttribute('data-lenis-prevent', '');
  });

  // Pause page scrolling while an overlay is open (mobile menu, gallery lightbox).
  function watch(el, isOpen) {
    if (!el) return;
    new MutationObserver(function () {
      if (isOpen(el)) lenis.stop(); else lenis.start();
    }).observe(el, { attributes: true, attributeFilter: ['class'] });
  }
  watch(document.querySelector('.w-nav-button'), function (el) { return el.classList.contains('w--open'); });
  watch(document.querySelector('[data-unit-lightbox="root"]'), function (el) { return el.classList.contains('is-open'); });
})();
</script>
```

## Tuning

- `lerp`: lower is smoother and slower to settle (currently 0.07; try 0.05 to 0.12).
- `wheelMultiplier`: scroll distance per wheel step.
- Any new element that scrolls on its own (modal, scrollable list) needs the attribute `data-lenis-prevent`.
- A new overlay that should lock page scroll needs a `watch(...)` line like the two at the end of the script.

## To undo

Remove the `<link>` from the head code and the two `<script>` blocks from the footer code.

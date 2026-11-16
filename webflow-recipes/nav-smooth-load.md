# Nav Smooth Load

Smoother load animation for the navbar (`nav_component` > `nav_container`).

## Why

The navbar's legacy interaction "Nav load aniamtion" slides `.nav_container` down from -127%
in 0.5s with linear easing, and it only starts once Webflow's scripts have loaded, so it looks
abrupt. Legacy interactions cannot be edited through the Webflow MCP tools, so a CSS animation
on the same element takes over: it starts at first paint, runs 0.9s with outQuart easing and
adds a fade. The legacy interaction is still on the navbar but has no visible effect.

## Where it is applied

Site settings > Custom code > Head code (site-wide).

## Code

```html
<style>
@media (prefers-reduced-motion: no-preference) {
  @keyframes amv-nav-slide-in {
    from { opacity: 0; transform: translate3d(0, -100%, 0); }
    to { opacity: 1; transform: none; }
  }
  .nav_container { animation: amv-nav-slide-in 0.9s cubic-bezier(0.165, 0.84, 0.44, 1) both; }
}
@media (prefers-reduced-motion: reduce) {
  .nav_container { transform: none !important; }
}
</style>
```

## To undo

Delete the block from the site head code. The legacy interaction takes over again.
To make it permanent in the Designer instead, edit "Nav load aniamtion" in the legacy
Interactions panel (easing Out Quart, ~900ms) and then delete this CSS.

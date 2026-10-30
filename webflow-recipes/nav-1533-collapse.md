# Recipe: "Nav 1533 Collapse"

**What it does:** makes the AMV navbar (`nav_component`, component `Navbar_component`) switch to its tablet / hamburger layout below **1533px** instead of Webflow's built-in 991px.

**Status:** tried on 2026-10-30, then removed at the client's request. Kept here so it can be re-applied later by name ("Nav 1533 Collapse").

## Why custom code is needed

Webflow's Navbar can only collapse at fixed points (tablet 991px, mobile landscape, mobile portrait, or none). A custom width such as 1533px is not possible in the Designer, so the 992–1532px range is handled with CSS.

Webflow decides whether the navbar is collapsed by checking if the menu button is displayed. Showing `.w-nav-button` and hiding `.w-nav-menu` in this range makes Webflow's own navbar script treat it as collapsed. Open/close, dropdowns and the hamburger (IX2) animation keep running through Webflow itself; no element or interaction is changed.

## How to apply

1. Inside the `Navbar_component` component, append an **Embed** element as the last child of the root `nav_component` (NavbarWrapper).
2. Name it in the Navigator: `Nav CSS – collapse below 1533px`.
3. Paste the code below.
4. Test on the published or staging site at widths 1000–1532px (the Designer canvas does not always render custom code).

## Code

The 992–1532px rules copy the navbar's existing tablet (medium) styles, as they were on 2026-10-30. If the tablet styles change later, update these rules to match.

```html
<style>
/* Navbar: use the tablet (collapsed) layout below 1533px. Webflow only offers fixed collapse points, so 992-1532px is handled here. */
@media screen and (min-width: 992px) and (max-width: 1532px) {
  .nav_component .w-nav-menu { display: none; }
  .nav_component .w-nav-button { display: block; }
  .nav_component .w-dropdown { display: block; }
  .nav_component .w-dropdown-list { position: static; }
  .nav_component { padding-left: var(--_layout---spacing--medium); padding-right: var(--_layout---spacing--medium); }
  .nav_component .nav_menu { position: absolute; overflow: auto; height: 100vh; margin-left: 0; padding: 1.5rem 2rem 5rem; align-items: flex-start; border-top: 1px solid var(--_theme---border--inverse-subtle); background-color: var(--_theme---background--primary); background-clip: border-box; }
  .nav_component .nav_menu-left { display: flex; flex-direction: column; align-items: flex-start; column-gap: 0px; row-gap: var(--_layout---spacing--none); color: var(--_theme---text--alternate); }
  .nav_component .nav_dropdown { position: relative; width: 100%; }
  .nav_component .nav_dropdown-toggle { display: flex; padding-top: var(--_layout---spacing--tiny); padding-bottom: var(--_layout---spacing--tiny); padding-left: 0; align-items: center; color: var(--_theme---text--alternate); font-size: 1rem; }
  .nav_component .nav_dropdown-toggle:hover { color: #101828; }
  .nav_component .nav_dropdown-icon { left: auto; top: auto; right: 0%; bottom: auto; margin: 0; color: #667085; }
  .nav_component .nav_dropdown-list { position: static; overflow: hidden; padding-left: var(--_layout---spacing--none); padding-right: var(--_layout---spacing--none); box-shadow: none; }
  .nav_component .nav_dropdown-link { padding-left: var(--_layout---spacing--xxsmall); padding-right: var(--_layout---spacing--xxsmall); }
  .nav_component .nav_dropdown-link:hover { background-color: transparent; }
  .nav_component .nav_dropdown-content { padding-top: 1rem; padding-bottom: 1rem; }
  .nav_component .nav_menu-right { margin-top: 1.5rem; padding-bottom: 7rem; flex-direction: column-reverse; align-items: stretch; grid-template-columns: 1fr; grid-template-rows: auto auto; }
  .nav_component .nav_button-wrapper { display: flex; flex-direction: column-reverse; align-items: stretch; }
  .nav_component .menu-icon_component { padding-right: 0; padding-bottom: 0; }
  .nav_component .menu-icon_line-top,
  .nav_component .menu-icon_line-middle,
  .nav_component .menu-icon_line-bottom { border-radius: 1rem; background-color: var(--_theme---background--subtle); }
}
</style>
```

## Known issues to fix before using again

- The client did not like the result when it was first applied. Find out what looked wrong before re-applying.
- `nav_dropdown-list` keeps the desktop `transform: translate(-50%)`, which tablet does not reset. The open dropdown may sit about 7.5rem to the left in both tablet and this range. Consider adding `transform: none;` to the tablet style and to this CSS.

## How to remove

Delete the `Nav CSS – collapse below 1533px` embed from `Navbar_component`. Nothing else was changed.

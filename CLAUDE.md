# AMV Webflow project rules

Webflow site "style guide v2" (site id `6ae0d68e35ac2bac3961b43e`), built with Client-First naming.

## Rules from the client

- **New utility classes go in the Style Guide.** Any extra class added to the site must also be shown on the Style Guide page, in its own clearly labelled section or row.
- **Classes use variables.** Build utility classes the same way as the existing ones (e.g. `text-color-primary`): bind values to variables, not hard-coded values.
- **Text sizes:** use the existing `text-size-*` classes (tiny / small / regular / medium / large) for paragraphs and text. Do not add new typography variable groups.
- **Typography always from the Style Guide classes.** Never put font-size, font-weight, line-height or text color into a new class. Apply the existing Style Guide classes on the element instead (e.g. `text-size-regular`, `text-weight-semibold`, `text-color-*`, `heading-style-*`). New classes may only hold layout, spacing, border and background.
- **Line heights:** Number variables only, pointing at the 4 Base values (small 1.1, medium 1.2, large 1.4, xlarge 1.5). Pick the closest one.
- **Do not delete existing variables or classes without asking.**
- **Images sent in chat:** when the client sends an image without other instructions, reply with the text content of the image only. Do not change Webflow.

## Reusable components

- **Spec table** (label / value table, used on many pages): global classes `spec-table_component` > `spec-table_row` > `spec-table_label` + `spec-table_value`. Rows alternate tinted (Background/brand-subtle) and white, with a border between label and value. Text comes from Style Guide classes on the cells: label = `spec-table_label text-size-regular text-weight-semibold`, value = `spec-table_value text-size-regular`. Always reuse these classes for any new spec / data table; never make page-specific copies. Shown in the Style Guide "Spec Table" section. Add margin with a utility class on a wrapper, not on the component.

## Saved recipes

- `webflow-recipes/nav-1533-collapse.md` — "Nav 1533 Collapse": custom CSS to collapse the navbar to its tablet layout below a custom width (currently applied at 1280px).
- `webflow-recipes/tab-open-slide-in.md` — "Tab Open Slide-In": custom CSS that replays the slide-in-bottom motion when a hidden tab pane is opened (applied in the head code of the Mobile Units Template and Studios Template pages). Also explains how the site's `slide-in-*` scroll animations work.
- `webflow-recipes/nav-smooth-load.md` — "Nav Smooth Load": site-wide head CSS that replaces the navbar's abrupt legacy load slide with a smoother eased slide + fade.
- `webflow-recipes/lenis-smooth-scroll.md` — "Lenis Smooth Scroll": site-wide Lenis smooth scrolling code, written to stay compatible with the slide-in animations, sticky elements, mobile menu and gallery lightbox. Applied site-wide in the site head + footer custom code.

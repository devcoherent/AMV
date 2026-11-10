# AMV Webflow project rules

Webflow site "style guide v2" (site id `6ae0d68e35ac2bac3961b43e`), built with Client-First naming.

## Rules from the client

- **New utility classes go in the Style Guide.** Any extra class added to the site must also be shown on the Style Guide page, in its own clearly labelled section or row.
- **Classes use variables.** Build utility classes the same way as the existing ones (e.g. `text-color-primary`): bind values to variables, not hard-coded values.
- **Text sizes:** use the existing `text-size-*` classes (tiny / small / regular / medium / large) for paragraphs and text. Do not add new typography variable groups.
- **Line heights:** Number variables only, pointing at the 4 Base values (small 1.1, medium 1.2, large 1.4, xlarge 1.5). Pick the closest one.
- **Do not delete existing variables or classes without asking.**
- **Images sent in chat:** when the client sends an image without other instructions, reply with the text content of the image only. Do not change Webflow.

## Saved recipes

- `webflow-recipes/nav-1533-collapse.md` — "Nav 1533 Collapse": custom CSS to collapse the navbar to its tablet layout below a custom width (currently applied at 1280px).

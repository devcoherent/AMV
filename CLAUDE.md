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

## Working rules learned from the client

- Talk to the client in Bangla (Banglish is fine). Keep replies short and say plainly what was done and what is left.
- Only touch the page the client is working on. If they say a page is finished (e.g. "Mobile Units template a kono touch korba na"), never change it, even for shared fixes: make a page-specific copy of the fix instead.
- Do not change the styles of existing classes. Add a new class (layout, spacing, border, background only) or reuse an existing one. Before creating a class, check whether another page already has a class doing the same job and reuse it; never make two classes for the same job.
- No CSS in custom code. All styling lives in Webflow classes; embeds may hold JavaScript only.
- Every element gets a Client-First class name (no unnamed divs).
- Use the existing site components: Spacer (variant prop), Hero_accent-line, buttons (`button is-flex`, `button is-secondary`), CTA, Navbar, Footer.
- Give every new CMS field a help text that says where it shows on the page, and put it in the matching field group (listing page group first, then one group per template section / tab).
- After every change: publish, then verify on the live site (allmobilevideo.webflow.io) with Playwright and screenshots before reporting.

## Site map (pages and CMS)

| Page | Page id | Live path | CMS collection |
|---|---|---|---|
| Home | `6ae0d69035ac2bac3961b4cc` | `/` | |
| Mobile (listing, Finsweet filters, card tooltip) | `6ae4fc18d35f0b5fa5af6cac` | `/mobile` | |
| Mobile Units Template (finished, do not touch) | `6ae50a6ca43174bb93995e25` | `/mobile/<slug>` | Mobile Units `6ae50a6ca43174bb93995e1f` |
| Production Spaces (studios listing) | `6af377896c7676999e8ec1dd` | `/stage` | |
| Studios Template | `6af379570dad849b03220882` | `/stage/<slug>` | Studios `6af379560dad849b0322087c` |
| Equipment Rentals | `6af3729fc0f4d4b03ff06a7b` | `/rental` | |
| Transmission Delivery (static, duplicated from Production Spaces) | `6afc7ebfd4ebac5a3c7845c4` | `/transmission-delivery` | |
| Style Guide (draft) | `6ae0d69035ac2bac3961b4d1` | `/style-guide` | |

### Detail template pattern (Mobile Units and Studios)

- Hero: `section_stage-hero` > `stage-hero_content` (text box) + `stage-hero_fade` (white gradient into the photo) + `background-image-wrapper hero-right`. Breadcrumb: `breadcrumb_component text-size-regular` > `breadcrumb_list` > `breadcrumb_link text-style-link` / `breadcrumb_divider` / `breadcrumb_current`.
- Tabs: default Webflow Tabs. `stage-detail_tabs` > `stage-detail_tabs-menu is-sticky` (sticky under the navbar) with `stage-detail_tab-link` (label div `text-size-regular text-weight-bold`) and `stage-detail_tabs-content` > `stage-detail_tab-pane`. Active tab colour is the class's Current state in the Designer.
- Tab section header: Hero_accent-line, Spacer, `heading-style-h2`, Spacer, `text-size-regular text-color-blue` line, then content in a `margin-top-medium` wrapper.
- Studios tabs: Overview (`stage-detail_overview-grid` 3 columns: highlights `mobile-detail_overview-content`, floor plan `stage-detail_floor-plan`, Quick Specs `mobile-detail_specs-content` with the spec table), Tech Specs (`spec-sheet_component` > `stage-detail_specs-grid` of `stage-detail_spec-card`), Gallery (`gallery_component` > `gallery_list-wrapper` > `gallery_list` > `gallery_item` > `gallery_image`; bento grid, first photo 2x2).
- Gallery lightbox: the "Unit Lightbox" component (`unit-lightbox_*` classes, `data-unit-lightbox` attributes) plus a script-only HtmlEmbed at the top of the detail section.
- Floor plans (Mobile Units): `floor-plan_*` classes. Spec sheet tab: `spec-sheet_*` classes.

### Transmission Delivery page pattern

- Hero: light version of the stage hero: `section_stage-hero` > `stage-hero_content is-wide` (32rem) > `padding-section-small background-color-alternate`, plus `stage-hero_fade`.
- One section `section_transmission` > `transmission_component`. Section headings: Hero_accent-line, Spacer 16px, h2 with `heading-style-h3 text-color-blue` (text typed in capitals).
- Feature cards (image left, text right): `feature-card_list` (2 columns) > `feature-card_component` > `feature-card_image-wrapper` > `feature-card_image` + `feature-card_content` (h3 `heading-style-h4 text-color-blue`, p `text-size-regular`).
- Tag bar: `tag-bar_component` with `text-size-regular text-weight-bold text-color-blue` labels and `footer_divider background-color-primary` dividers.
- Photo row: `photo-strip_list` (5 columns) > `photo-strip_image`.
- Team box: `stage-detail_spec-card` > `team_grid` > `team_item` / `team_divider`.
- 3-column table: spec table with the row combo `spec-table_row is-3-col`; the last cell of a header row is `spec-table_value text-size-regular text-weight-semibold`.

## Webflow MCP API limits (work-arounds)

- A Collection List source cannot be set to a multi-image / multi-reference field: ask the client to set the source in the Designer, then add and bind the child elements.
- Elements with CMS bindings fail inside nested builder calls: create them first, then bind with `set_settings`.
- The builder cannot create a tab link or pane: build a temporary Tabs element, move its 3rd link and pane into the real tabs, then delete the temporary Tabs.
- Conditional visibility, Lightbox element media and the "Current" state cannot be set by API: ask the client to do these in the Designer.
- Multi-class `set_style` needs the combo to exist: create an empty combo first.
- Webflow cannot keep a variable inside a gradient value, so gradients are hard-coded.
- Publishing is limited to once per minute.
- `set_text` inside a nested builder call is ignored for TextBlock (Heading, Paragraph and TextLink are fine), and `set_text` on the TextBlock fails afterwards: set the text on its String child (same element id with the last hex digit + 1).
- An element cannot be moved or inserted `after` a component instance: anchor `before` the next normal element instead.

## Saved recipes

- `webflow-recipes/nav-1533-collapse.md` — "Nav 1533 Collapse": custom CSS to collapse the navbar to its tablet layout below a custom width (currently applied at 1280px).

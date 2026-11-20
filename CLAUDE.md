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
| Authorized Distributor (static, duplicated from Transmission Delivery) | `6afcbbd32629c9ec552c7162` | `/authorized-distributor` | Manufacturers `6afcbbe136b71b9eb7735608` (collection list) |
| Systems Design & Integration (static) | `6afcbd89e5e28fd37f0c6d0f` | `/systems-design-integration` | |
| Managed Studio Services (static) | `6afcbe7f2174b0705e4e56f0` | `/managed-studio-services` | |
| Equipment Sales (static) | `6afcc02c08be3d8ec05172db` | `/sales` | Featured Equipment `6afcc02fb8c4a4eb58b662a0` (collection list) |
| Custom Engineering & Fabrication (static) | `6afcc2f65d702d810b221380` | `/custom-engineering-fabrication` | |
| Manufacturers Template (auto-created, unused) | `6afcbbe136b71b9eb773560e` | `/manufacturer/<slug>` | Manufacturers |
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

### Authorized Distributor page pattern

- Hero: same light hero as Transmission Delivery, with the breadcrumb on top.
- Section `section_distributor` > `distributor_component`.
- Logo grid (Manufacturers collection: Name, Logo, Website): `manufacturer_list-wrapper` > `manufacturer_list` (5 / 3 / 2 columns) > `manufacturer_item` > link `manufacturer_card` (bound to Website, new tab) > `manufacturer_logo` (Logo) + h3 `heading-style-h4 text-color-heading` (Name, fallback while a logo is missing) + `manufacturer_arrow text-color-blue` with an `icon-1x1-small` svg.
- Button: `margin-top-medium text-align-center` wrapper > `button is-secondary`.
- Help bar: reuses `tag-bar_component` with `icon-1x1-large text-color-blue` svgs, `footer_divider background-color-primary` and `team_item` text blocks.

### Systems Design & Integration and Managed Studio Services pattern

- Both use the light hero and one `section_systems` / `section_managed` per band: section > `padding-section-small` (+ `background-color-brand-subtle` or `background-color-primary` for a tinted / dark band) > `padding-global` > `container-large` > `systems_component` / `managed_component`.
- Title + text columns: `team_grid` rows (3 columns with `team_divider`, rows split by `team_line`) or `process_list` (6 columns) of `team_item` (h3 `heading-style-h4`, p `text-size-regular`).
- Numbered steps: `process_list` > `process_line` + `process_item text-align-center` > `process_number` (number in `text-size-medium text-color-alternate`), title `text-size-regular text-weight-bold text-color-blue`.
- Image + text cards: `photo-strip_list` (5 columns) or `home-services_grid` (4 columns) with `stage-detail_spec-card` > `team_item` > `photo-strip_image`.
- Contact band: `tag-bar_component` with `process_item text-align-center` blocks (`button` + `text-style-link text-size-large`).
- Use Paragraph (not TextBlock) for short labels built by the API, so `set_text` works in nested builds.

### Managed Studio Services clean-up (reusable classes added)

- Divided columns: `divided-list_component` (overflow-x clip, overflow-y visible so items can slide in) > `divided-list_list` (6 columns from 1440px, 3 below, 2 on mobile landscape, 1 on mobile portrait; margin-left -1rem so the first divider of every row is clipped; hard-coded because a variable cannot be negative, keep it equal to the item padding Spacing/xxsmall) > `divided-list_item` (left border + side padding). Centred label variant: `divided-list_item is-centered`. Used for What We Do and Who We Support.
- Heading with a line to the right: inside `section_header`, `heading-line_component` (bottom-aligned) > h2 + `heading-line_line` (1px, Blue/300, sits on the heading's baseline via margin-bottom Spacing/xtiny).
- Image card with a flush image: `media-card_component` > `photo-strip_image-wrapper` > `photo-strip_image` (the client added the hover zoom on these) + `media-card_content`.
- Photo banner: `cta-banner_component background-color-primary` > `background-image-wrapper` > `background-image`, `cta-banner_overlay` (Background/overlay-strong), `cta-banner_content` > `padding-global` > `container-large` > ... > `max-width-large align-center` > `team_item`.
- Tighter section spacing: `padding-section-bottom-small` on a section that follows a white section.
- The other new pages still use the older `stage-detail_spec-card` cards, `tag-bar_component` and plain headings.

### Custom Engineering & Fabrication page pattern

- Light hero (H1 wraps to 3 lines at `is-wide` 32rem), then `section_custom` > ... > `custom_component` bands: tinted capabilities band (`grid-autofit-small` of `stage-detail_spec-card` > `team_item` with `photo-strip_image`, h3 `heading-style-h4 text-color-blue`), dark banner (`padding-section-small background-color-primary`, `heading-style-h3 text-color-alternate`), contact (`mobile-contacts_list` of `team_item` blocks with a `footer_divider background-color-primary`).

### Equipment Sales page pattern

- Light hero, then `section_sales` > ... > `sales_component` bands.
- Intro cards: `grid-autofit-small` > `stage-detail_spec-card` > `team_item` (`photo-strip_image`, h2 `heading-style-h3 text-color-blue`, p `text-size-regular`, `text-style-link`).
- Featured Equipment (collection: Name, Brand, Image, Product Link): `product_list-wrapper` > `product_list` (8 / 4 / 2 columns) > `product_item` > `stage-detail_spec-card` > `team_item` (image, h3 `text-size-regular`, p `text-size-small`, `text-style-link` "VIEW PRODUCT").
- Contact row: `mobile-contacts_list` with `text-style-link text-size-large` links and a `footer_divider background-color-primary`.

## Scroll reveal animation

- Lives in the site custom code (head: setup script with the `PAGES` and `ITEMS` selector lists; footer: observer). JavaScript only, same motion as the `slide-in-bottom` interactions.
- A new card / block class only animates after its selector is added to `ITEMS` (and a new page's section class to `PAGES`). Read the head code with `get_site_freeform_code`, add the selector, write the whole block back with `set_site_freeform_code`, publish.
- Currently listed for the new components: `.divided-list_item`, `.media-card_component`, `.max-width-large > .team_item`.

## Webflow MCP API limits (work-arounds)

- A Collection List source cannot be set to a multi-image / multi-reference field: ask the client to set the source in the Designer, then add and bind the child elements.
- Elements with CMS bindings fail inside nested builder calls: create them first, then bind with `set_settings`.
- The builder cannot create a tab link or pane: build a temporary Tabs element, move its 3rd link and pane into the real tabs, then delete the temporary Tabs.
- Conditional visibility, Lightbox element media and the "Current" state cannot be set by API: ask the client to do these in the Designer.
- Multi-class `set_style` needs the combo to exist: create an empty combo first.
- Webflow cannot keep a variable inside a gradient value, so gradients are hard-coded.
- Publishing is limited to once per minute.
- `set_text` inside a nested builder call is ignored for TextBlock (Heading, Paragraph and TextLink are fine), and `set_text` on the TextBlock fails afterwards: set the text on its String child (same element id with the last hex digit + 1).
- Collection List: set the source with `set_settings` key `source`, `static_json` `{"collectionId":"..."}`; bind an image with key `assetId`. Setting `sort` fails with a conflict error: ask the client to set the sort in the Designer.
- `set_link` with a page link inside a nested builder call is not applied (the link stays `#`); url, email and phone links are fine. Set page links afterwards with `set_link`.
- `calc()` with a variable in a style value is collapsed to the bare variable by the API, and the `sizes` attribute cannot be set on an image.
- Hero photos on API-built pages publish with a tiny `sizes` value (blurry image): ask the client to open the page in the Designer and republish, or regenerate responsive images.
- The client's scroll-reveal script hides images again in Playwright full-page screenshots: capture viewport by viewport instead.
- An element cannot be moved or inserted `after` a component instance: anchor `before` the next normal element instead.

## Saved recipes

- `webflow-recipes/nav-1533-collapse.md` — "Nav 1533 Collapse": custom CSS to collapse the navbar to its tablet layout below a custom width (currently applied at 1280px).

# Purelane Shopify – Build Notes

## Overview

This project converts the Purelane homepage prototype into reusable, merchant-editable Shopify sections using the Dawn theme.

The implementation focuses on the five required homepage areas:

1. Hero
2. Shop / Product Grid
3. Best-selling Combos
4. Bundles
5. Reviews Rail

The design was treated as the visual specification while the prototype's implementation was adapted into production-oriented Shopify Liquid.

---

## Shopify Setup

- Theme: Dawn
- Shopify CLI: 3.92.1
- Store: Purelane development store
- Platform: Shopify Online Store 2.0
- Repository: `purelane-shopify`
- Main development branch: `feature/purelane-homepage`

---

## Required Sections

### 1. Purelane Hero

File:

`sections/purelane-hero.liquid`

The hero section is merchant-editable through the Shopify Theme Editor.

Configurable content includes:

- Eyebrow text
- Main heading
- Supporting text
- Primary CTA
- Secondary CTA
- Hero image
- Image alt text

The hero image uses eager loading because it is part of the initial viewport.

---

### 2. Shop / Product Grid

File:

`sections/purelane-product-grid.liquid`

The product grid uses real Shopify product data rather than hardcoded product information.

Merchant-configurable options include:

- Section heading
- Supporting text
- Product collection
- Number of products
- Grid layout
- CTA text

The implementation handles:

- Available products
- Sold-out products
- Products without images
- Long product titles
- Product prices
- Product links
- Product images and alt text

Product images are lazy-loaded to avoid unnecessary initial network work.

---

### 3. Best-selling Combos

File:

`sections/purelane-combos.liquid`

Combos are implemented using Shopify section blocks so merchants can add, remove, reorder, and replace products from the Theme Editor.

Each combo supports:

- Product selection
- Label
- Description
- CTA text

Current configured examples include:

- Natural Herbal Floor Cleaner
- Gentle Hydrating Liquid Handwash
- Purelane Plant-Based Multi-Surface Home & Kitchen Cleaner

---

### 4. Bundles

File:

`sections/purelane-bundles.liquid`

Bundles are also implemented as reusable section blocks.

Each bundle supports:

- Product selection
- Badge / label
- Description
- CTA text

Current configured examples include:

- Laundry Detergent
- Organic Dishwash Gel
- Non-Toxic Toilet Cleaner

This structure allows the marketing team to modify bundle content without editing Liquid code.

---

### 5. Reviews Rail

File:

`sections/purelane-reviews.liquid`

Reviews are implemented as merchant-editable section blocks.

Each review supports:

- Customer name
- Rating
- Review text
- Verified-review option

The review content is therefore editable directly from the Shopify Theme Editor without requiring code changes.

---

## Styling

Shared Purelane styling is located in:

`assets/purelane.css`

The stylesheet contains:

- Purelane color variables
- Typography
- Buttons
- Cards
- Product grid
- Responsive layouts
- Hover states
- Focus states
- Sold-out states
- No-image states
- Reduced-motion behavior

The stylesheet is loaded globally from:

`layout/theme.liquid`

using Shopify's asset pipeline.

---

## Responsive Design

The homepage was tested across desktop and mobile layouts.

The implementation uses responsive CSS rather than separate desktop/mobile markup wherever possible.

The layout adapts for:

- Mobile
- Tablet
- Desktop

Product and content grids collapse appropriately on smaller screens while preserving the visual hierarchy of the prototype.

---

## Accessibility

Accessibility considerations included:

- Semantic HTML
- Descriptive image alt text
- Keyboard-accessible links and controls
- Visible `:focus-visible` states
- Sufficient text/background contrast
- Reduced-motion support
- Proper button/link usage
- Sold-out state communication
- Accessible product links

The implementation also avoids relying on animation as the only way to communicate information.

---

## Animation Approach

Animations are implemented primarily with CSS.

The custom Purelane sections do not depend on JavaScript event listeners, DOM queries, `IntersectionObserver`, or `requestAnimationFrame`.

This was intentional because Shopify merchants can add, remove, and reorder sections through the Theme Editor. CSS-based animation keeps the sections independent and reduces the risk of JavaScript initialization problems when the page structure changes.

A `prefers-reduced-motion` media query is included to reduce or disable non-essential motion for users who request reduced motion.

---

## Performance

Performance considerations include:

- Shopify-hosted theme assets
- No hardcoded external product/image URLs
- Lazy loading for below-the-fold product imagery
- Eager loading for the primary hero image
- CSS-based animations instead of JavaScript animation loops
- Reusable shared CSS
- Native Shopify product and collection data
- No unnecessary third-party JavaScript dependencies added for the required sections

The implementation is designed to keep the initial page lightweight while allowing the merchant to manage content dynamically.

---

## Merchant Editability

The required sections are designed for use by a non-developer marketing team.

Content is exposed through Shopify section settings and blocks wherever appropriate.

Merchants can:

- Change headings and copy
- Change images
- Select products
- Select collections
- Add/remove combo items
- Add/remove bundles
- Add/remove reviews
- Reorder section blocks
- Reorder homepage sections

No Liquid code changes are required for normal content updates.

---

## Shopify Theme Editor Resilience

The implementation avoids page-level assumptions between custom sections.

Each required section owns its own markup and styling behavior.

This allows sections to be:

- Added
- Removed
- Reordered
- Duplicated where supported

without requiring another custom section to exist.

The animation implementation is also section-independent and does not rely on a single page initialization script.

---

## Data Model

The current implementation intentionally keeps Reviews as section blocks because this provides a simple merchant-editing workflow for the assignment.

For a larger production implementation, reviews could be migrated to a Shopify Metaobject such as:

**Review**

Suggested fields:

- Customer name — single line text
- Review text — multi-line text
- Rating — integer/number
- Verified — boolean
- Product — product reference
- Review date — date

This would allow the same review records to be reused across multiple sections or pages.

The current assignment implementation does not require this additional abstraction because the review rail is already fully merchant-editable.

---

## Prototype-to-Production Changes

The original prototype was treated as the visual reference rather than code to copy directly.

The production implementation changes the prototype where required for Shopify compatibility and maintainability.

Key changes include:

- Static product markup replaced with Shopify product objects
- Static product URLs replaced with Shopify product URLs
- Static product information replaced with merchant-selectable products
- Reusable Shopify sections created from the prototype areas
- Repeated content converted into section blocks
- Product images use Shopify image handling
- Missing product images are handled gracefully
- Sold-out products have a dedicated visual state
- Long product titles are handled without breaking the card layout
- CSS is moved into a reusable theme asset where appropriate
- Accessibility states were added
- Reduced-motion support was added
- JavaScript-dependent animation behavior was avoided for the required sections

These changes preserve the intended visual design while making the implementation suitable for Shopify's theme architecture.

---

## Testing Performed

The following areas were tested:

- Desktop homepage rendering
- Mobile homepage rendering
- Theme Editor section settings
- Adding/removing sections
- Reordering sections
- Product selection
- Sold-out product display
- Product without an image
- Long product title
- Combo blocks
- Bundle blocks
- Review blocks
- Keyboard focus states
- Reduced-motion CSS
- Shopify Theme Check

Theme Check completed with:

- 160 files inspected
- 0 errors
- 10 warnings

The warnings are from existing Dawn theme files and do not originate from the custom Purelane sections.

---

## Repository Structure

Important custom files:

```text
assets/
└── purelane.css

sections/
├── purelane-hero.liquid
├── purelane-product-grid.liquid
├── purelane-combos.liquid
├── purelane-bundles.liquid
└── purelane-reviews.liquid

layout/
└── theme.liquid

templates/
└── index.json
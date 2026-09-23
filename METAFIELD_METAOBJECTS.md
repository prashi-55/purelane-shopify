# Purelane – Metafield / Metaobject Definitions

> **Implementation status:** No custom metafields or metaobjects were created for the final assignment implementation. The required sections use Shopify's native product/collection data and section settings/blocks. The Review metaobject described below is a proposed production data model for a future iteration if reviews need to be reused across multiple surfaces.

## Current Implementation

The required homepage sections use Shopify's native section settings and blocks for merchant-editable content.

The Reviews Rail is currently implemented using section blocks because this provides a simple editing workflow for the assignment.

No product-specific information is hardcoded into the product grid.

---

## Recommended Review Metaobject

For a larger production implementation, reviews can be represented as a Shopify Metaobject.

### Metaobject Type

`purelane_review`

### Display Name

`Purelane Review`

### Fields

| Field | Type | Purpose |
|---|---|---|
| Customer name | Single-line text | Name displayed with the review |
| Review text | Multi-line text | Customer review content |
| Rating | Integer / number | Star rating |
| Verified | Boolean | Whether the review is verified |
| Product | Product reference | Product associated with the review |
| Review date | Date | Date associated with the review |

---

## Suggested Validation

### Customer name

Required.

### Review text

Required.

### Rating

Required.

Suggested valid range:

`1–5`

### Verified

Optional boolean.

### Product

Optional product reference.

This allows reviews that are associated with a specific product while also supporting general store reviews.

### Review date

Optional date.

---

## Example Data

### Review 1

Customer name:

`Riya`

Rating:

`5`

Review text:

`The floor cleaner smells fresh without the harsh chemical smell.`

Verified:

`false`

---

### Review 2

Customer name:

`Ananya`

Rating:

`5`

Review text:

`Finally a cleaner that feels good to use every day.`

Verified:

`false`

---

### Review 3

Customer name:

`Aarav`

Rating:

`5`

Review text:

`The products clean beautifully without the harsh smell.`

Verified:

`false`

---

## Why a Metaobject

A Metaobject would allow review records to be reused across:

- Homepage reviews
- Product pages
- Dedicated review pages
- Collection pages
- Marketing sections

It also separates review data from presentation.

The current assignment implementation intentionally keeps reviews as section blocks because the required Reviews Rail is already merchant-editable through the Theme Editor.

---

## Potential Product Metafields

If the store later requires additional product-level merchandising data, the following metafields could be introduced.

### `custom.badge`

Type:

Single-line text

Purpose:

Store a merchandising badge such as:

- Best Seller
- New
- Popular
- Limited

---

### `custom.short_description`

Type:

Multi-line text

Purpose:

Store a short marketing description independently from the product description.

---

### `custom.bundle_label`

Type:

Single-line text

Purpose:

Store a merchandising label used when the product is presented as part of a bundle or combination.

---

## Design Principle

Product data should remain in Shopify product objects wherever possible.

Custom metafields should only be introduced when the information represents additional merchant-managed data that Shopify's standard product fields do not already provide.

This keeps the implementation maintainable and avoids duplicating native Shopify data.
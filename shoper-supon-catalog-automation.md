# Case Study: E-commerce Catalog Automation (Shoper / SUPON Kielce)

## Context

SUPON Kielce is a B2B supplier of workwear, PPE, and fire-safety equipment.
Its online store (`sklep.supon.kielce.pl`) runs on the Shoper e-commerce
platform. The store's catalog had grown organically over time: duplicate
product listings, an inconsistent category tree, disabled attribute groups,
and inconsistent SEO metadata.

## Task

Modernize the store's catalog end-to-end — structure, content, and visual
presentation — and convert it from a direct-sale storefront into a B2B
"request a quote" catalog, without manual one-by-one editing in the Shoper
admin panel.

## My Role & Approach

I built and ran a set of Node.js scripts against the **Shoper REST API** to
automate catalog operations at scale, instead of editing ~1,000 products by
hand.

The work broke down into several areas:

**Visual redesign** — implemented a flat, high-contrast theme on Shoper's
Storefront engine matching the brand's visual identity, plus mobile layout
fixes.

**Category restructuring** — rebuilt the category tree (6 main categories,
multiple subcategories) via the REST API, removed duplicate/empty categories,
and added missing subcategories to reflect the actual product range.

**Bulk catalog import** — parsed a ~3,500-row CSV/Excel export, grouped rows
into unique products, and created them via the REST API. Along the way I hit
an architectural limitation in Shoper's REST API (the default base warehouse
doesn't support per-variant option binding) and worked around it by
registering per-variant service warehouses with correct SKUs — this was the
trickiest part of the integration.

**Deduplication & recategorization** — identified and merged product entries
that had been duplicated per color/size variant into proper multi-variant
products, then deleted the redundant pages; separately, ran a recategorization
pass across several hundred products to fix misplaced items by product type.

**Attribute/variant system** — re-enabled previously disabled parameter
groups, relinked them to the new category structure, and populated dropdown
values (sizes, colors, materials, safety norms) consistently across the
catalog.

**Content cleanup** — standardized and cleaned up HTML product descriptions
across the catalog (stripped inline styles, fixed broken markup, made
tables/lists responsive) and rewrote SEO metadata (title/description/keywords)
for all main and sub-categories.

**B2B conversion ("ask for a quote" mode)** — updated stock/availability
records at scale to disable direct "add to cart" and activate Shoper's native
"ask about product" inquiry form, matching the client's B2B sales model.

**Sorting & consistency** — fixed inconsistent ordering of variant option
values (sizes, colors) using locale-aware sorting rules.

## Tech Stack

Node.js · Shoper REST API · `@shoper/cli` · LESS (theme styling) · `xlsx`
(CSV/Excel processing)

## Results

- Rebuilt the category tree from a flat, duplicate-ridden structure into 6
  well-organized main categories with consistent subcategories
- Imported and structured the full product catalog (~945 unique products)
  from a ~3,500-row source export
- Merged hundreds of duplicate product listings into properly structured
  multi-variant products
- Re-enabled and populated the attribute/variant system across 11 parameter
  groups
- Cleaned and standardized HTML descriptions across the bulk of the catalog
- Converted the store from direct sale to a B2B inquiry-based catalog at the
  data level, across the full stock/variant set
- Optimized SEO metadata across all main and sub-categories

## What I'd highlight from this project

Working directly against a third-party platform's REST API at scale exposes
real architectural constraints that don't show up in the docs (e.g., the
warehouse/option-binding limitation above) — diagnosing and designing a
workaround for that, while keeping data integrity verifiable via spot-checks,
is the most representative part of this project.

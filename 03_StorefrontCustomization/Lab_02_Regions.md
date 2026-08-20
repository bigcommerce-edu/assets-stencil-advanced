# Lab Activity: Add Regions to the Product Page

**Objectives**

* Add a standard region to the product detail page
* Add a global region to the product detail page

**Prerequisites**

* Stencil CLI Installed
* Cornerstone theme cloned

Regions are named locations in a Stencil theme's template files that make a page editable in a visual editor — Page Builder or Makeswift. In this lab, you will add two regions to the product detail page: one standard region scoped to the product page, and one global region available sitewide. A good place to add them is the product page template, _templates/pages/product.html_, which renders on every product detail page.

## Add a Standard Region

1. **Open** _templates/pages/product.html_ in your Cornerstone theme
2. **Locate** a logical insertion point on the page — for example, just below the product details
3. **Add** the following region helper, giving it a descriptive name:

```html showLineNumbers={false}
{{{region name="product_below_details"}}}
```

This region appears as an editable drop target only on pages that use the product template.

## Add a Global Region

1. **Choose** a second insertion point in the same file — for example, above the product details
2. **Add** a region with the _--global_ suffix so it is available sitewide:

```html showLineNumbers={false}
{{{region name="product_above_details--global"}}}
```

Because it is global, this region is available on every storefront page where the component renders, not just the product page.

**Note:** You will test these regions once your theme is bundled and pushed to a store. That step is covered in _05_Deployment/Lab_02_TestRegions.md_. After deployment, both regions become available as drop targets in the visual editor — Page Builder or Makeswift — so store users can place widgets in the locations you defined.

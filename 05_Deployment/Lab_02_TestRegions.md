# Lab Activity: Test Custom Regions and Config Settings

**Objectives**

* Place content in the custom regions you added earlier
* Confirm a standard region is scoped to a single page
* Confirm a global region appears sitewide

**Prerequisites**

* Completed _03_StorefrontCustomization/Lab_02_Regions.md_
* Bundled and pushed your customized theme to a store

Now that your customized theme is deployed, you can test the two regions you added to the product page template — the standard _product_below_details_ region and the global _product_above_details--global_ region. You can do this in either of the two visual editors. Follow the **Page Builder** path below, or the optional **Makeswift** path if you have the beta enabled.

## Test in Page Builder

1. **Open** the store control panel and go to _Storefront > My Themes_
2. **Click** Customize on your active theme to open Page Builder
3. **Navigate** to a specific product detail page (PDP) in the editor preview
4. **Drag** a widget into the standard _product_below_details_ region and configure its content
5. **Drag** a widget into the global _product_above_details--global_ region and configure its content
6. **Save** your changes
7. **Navigate** to a _different_ PDP in the editor preview
8. **Observe** that the global region's content appears on this second PDP, while the standard region's content does not

The standard region is scoped to the page where you placed it, whereas the global region carries its content across every PDP that renders the template.

## Test in Makeswift (Optional)

**Note:** Makeswift on Stencil is currently in Beta, and this section is optional. Features and availability are subject to change. To enable the beta and connect Makeswift to your storefront, see [Makeswift on Stencil](https://docs.makeswift.com/product/docs/guides/makeswift-on-stencil).

If you have the Makeswift beta enabled, you can run the same test in Makeswift:

1. **Open** the store control panel and go to the Channel Manager
2. **Select** the Makeswift-connected channel and click Edit in Makeswift
3. **Navigate** to a specific product detail page (PDP) in the editor
4. **Add** content to the standard _product_below_details_ region
5. **Add** content to the global _product_above_details--global_ region
6. **Save** your changes
7. **Navigate** to a _different_ PDP and **observe** that the global region's content appears there as well, while the standard region's content does not

### Use built-in Stencil components

While building content, explore the components in the Makeswift component drawer. Makeswift ships a set of unique, built-in Stencil components — such as Accordion and Card — that you can drop directly into your regions to compose richer layouts without writing code.

### Component Styles in the Elements panel

Open the Elements panel to find the Component Styles controls. These let you set global styling for an entire component type — for example, adjusting the default appearance of every Card or Accordion on the storefront at once — rather than styling each instance individually. This keeps your components visually consistent across the pages where they appear.

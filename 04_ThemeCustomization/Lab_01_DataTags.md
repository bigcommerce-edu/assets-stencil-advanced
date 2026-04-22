# Lab Activity: Adding Data Tags

Data Tags provide detailed data on the way shoppers interact with your store's products. However, data tags are not only limited to only product data collection. Data Tags can also track your store's header and footer for promotions and can collect data on whether those promotions were viewed and/or clicked. BigCommerce's Data Tags are powered by Segment and Platform.js, and will send your store's product data through to Google Analytics.

Cornerstone versions 2.6.0+ will have Data Tags already included in the theme.

[Dev Docs link to Data Tags](https://docs.bigcommerce.com/developer/docs/storefront/stencil/getting-started)

**Prerequisites**

* [BigCommerce Store](https://support.bigcommerce.com/s/article/Starting-a-Bigcommerce-Trial)
* [Optimized One-Page Checkout enabled](https://support.bigcommerce.com/s/article/Optimized-Single-Page-Checkout)
* [Cornerstone theme installed](https://docs.bigcommerce.com/developer/docs/storefront/stencil/getting-started/about-stencil)

## Include the Enhanced eCommerce Property

1. Open your local copy of your theme and navigate to the theme's _cornerstone/config.json_ file
2. In the config.json file, navigate to the features array. There should be a property in this array called `enhanced_ecommerce`. If the enhanced ecommerce property is not present in the features array, add it. The features object should then look similar to the example below

### Enhanced eCommerce Feature

```json title="config.json" showLineNumbers={false}
"features": [
      "fully_responsive",
      "mega_navigation",
      "multi_tiered_sidebar_menu",
      "masonry_design",
      "frontpage_slideshow",
      "quick_add_to_cart",
      "switchable_product_view",
      "product_comparison_table",
      "complex_search_filtering",
      "customizable_product_selector",
      "cart_suggested_products",
      "free_customer_support",
      "free_theme_upgrades",
      "high_res_product_images",
      "product_filtering",
      "advanced_quick_view",
      "product_showcase",
      "persistent_cart",
      "one_page_check_out",
      "product_videos",
      "google_amp",
      "customized_checkout",
      "account_payment_methods",
      "enhanced_ecommerce",
      "csrf_protection"
    ]
```

You are now ready to begin adding data tags into the HTML files across your Cornerstone theme.

## Adding Data Tags into Cornerstone's HTML files

Data tags must be manually added to a product in order to track shopper events and interactions with a product. Because data tags collect product data at a very granular level, there will be multiple locations you will have to add tags on a singular product in order to get a comprehensive look at the product's data. For example, a merchant has requested that a product can be viewed by clicking any of the following:

* The name of the product
* The "Quick View" button
* The product image

So, in order to get a fully comprehensive look at shoppers' interactions with a product, you will want to include a data tag on each of these fields. If a specific product possesses multiple data tags, the data tag that is closest to the product is the one that will track clicks, product impressions, or product views.

Data tags will be implemented in your store by using simple HTML. In order to begin tracking, you will add data tags as an attribute to the already existing HTML tags present in your theme.

See Pull Request #1377 to see how Data Tags were implemented in Cornerstone 2.6.0.

**Data Tag Implementation Example**

You can see a data tag implemented in the HTML form tag in the code sample below:

```jsx title="Data Tag HTML" showLineNumbers={false}
<form action="{{urls.compare}}" method='POST' data-list-name="Brand: {{brand.name}}" data-product-compare>
    {{#if theme_settings.product_list_display_mode '===' 'grid'}}
        {{> components/products/grid products=brand.products show_compare=brand.show_compare theme_settings=theme_settings event="list"}}
    {{else}}
        {{> components/products/list products=brand.products show_compare=brand.show_compare theme_settings=theme_settings event="list"}}
    {{/if}}
</form>

{{> components/common/paginator pagination.brand}}
```

In the above snippet, the data tag is embedded in a `<form>` HTML tag in lines 1 and 2. The data tag is _data-list-name_ and its value is _Brand: \{\{brand.name\}\}_.

### Data Tag Reference

Currently, BigCommerce supports 11 different data tags. Below is a table with a breakdown of each tag and its description.

**Mandatory Data**

* If tracking promotions data, either _data-banner-id_ or _data-name_ is required.
* If tracking data for a product, either _data-entity-id_ or _data-name_ is required.
* If tracking data for a product list, either _data-product-list_ or _data-entity-id_ is required.

The "tracked product" refers to the product on which you are inserting the data tag on.


| **Data Tag** | **Description** | **Value Type** | **Example** |
|---|---|---|---|
| data-list-name | The data-list-name tag denotes the name of the list that will be reflected on Google Analytics | string or handlebars helper | String Example:data-list-name=&quot;Kitchen Appliances&quot;Handlebars Value Example: The data-list-name tag can also get its value using Handlebars. For example, if you are adding a data tag to your carousel products in products/carousel.html, you could create the tag data-list-name=&quot;\{\{list\}\}&quot; and define the list value in products/new.html to be: list=&quot;New product |
| data-entity-id | The data-entity-id is equal to the tracked item's id. | integer | data-entity-id=12 |
| data-position | The data-position tag is equal to the tracked product's position or the tracked promotion's position. | Value is a string if creating the data tag for a promotion. The string should denote the location of the promotion.Value is an integer if creating the data tag for a product. The integer should represent the product's placement. An example use case for this data tag is to answer a question like, "does the product in position 1 sell more than the product in position 4?" | **String Value Example:** data-position=&quot;center&quot; <br /><br /> **Integer Value Example:** data-position=2 |
| data-banner-id | The data-banner-id tag is the id of the banner being tracked. The banner id is not to be mistaken with the promotion id. | integer | integer |
| data-event-type | The data-event-type tag is equal to the shopper event that will be tracked. There are a 4 shopper/product interactions you can measure and set the data-event-type equal to. Custom events are not yet implemented. | string that can be: <br /> &quot;promotion&quot; <br /> &quot;promotion click&quot; <br /> &quot;product&quot; <br /> &quot;list&quot; | data-event-type=&quot;promotion&quot; |
| data-name | The data-name tag is equal to the tracked product's or banner's name. | string or handlebars helper | **String Value Example:&nbsp;** data-name=&quot;Ruffle Off-the-Shoulder Top&quot; <br /><br /> **Handlebars Value Example:** The `data-name` tag can also get its value using Handlebars. **For example,** if you are adding a data tag to your footer in products/footer.html, you could create the tag: `data-name="{{this.banner-name}}"` Or, if you are adding a data tag to a product list item in products/list-item.html, you could create the tag below `data-name="{{name}}"` as long as these values are defined. |
| data-product-category | The data-product-category tag is equal to the tracked product's category. | string | data-product-category=&quot;Women's Apparel&quot; |
| data-product-brand | The data-product-brand tag is equal to the tracked product's brand. | string | data-product-brand=&quot;Ralph Lauren Corporation&quot; |
| data-product-price | The data-product-price tag is equal to the tracked product's price. | integer | data-product-price=&quot;27.99&quot; |
| data-product-sku | The data-product-sku tag is equal to the tracked product's sku value. | string | data-product-price=&quot;27.99&quot; |
| data-product-variant | The data-product-variant is equal to the tracked product's variant. | string | data-product-variant=&quot;4-Yellow&quot; |

## Custom Dimensions and Metrics

Custom dimensions and metrics are also supported. To add them in the config.json settings array, add the name of the dimension/metric followed by the generic custom metric/dimension alias.

**Example:**

```json title="config.json" showLineNumbers={false}
{
    // ...
    "settings": {
        // ...
        "custom-dimensions": {
            "<your-custom-dimension-name>": "dimension1", "dimension-common": "dimension2"
        },
        "custom-metrics": {
            "<your-custom-metric-name": "metric1", "metric-common": "metric2"
        }
    }
    // ...
}
```

**Note:**

* Spelling must be exact
* Names may not have spaces

Next, add the custom _metrics/dimensions_ to the desired theme template:

* Dimensions are typically strings
* Metrics are usually integers

```jsx showLineNumbers={false}
<!--...-->
{{#if settings.data_tag_enabled}}
    <article class="listItem" dimension-common="yes" metric-common=1 data-event-type="{{event}}">
{{else}}
<!--...-->
{{/if}}
<!--...-->
```

#Simple, Dynamic Shopify Product Tabs

A simple, dynamic implementation of shopify product tabs.
Much credit goes to [Shopify Docs implementation](https://docs.shopify.com/support/your-store/products/how-do-i-add-tabs-to-product-descriptions); be we extended it to make dynamic.

## Get started

#### Add the asset files

Add the tabs.js file to your assets folder and `theme.liquid` layout
Add the tabs.scss file to your assets folder and `theme.liquid` layout

#### Hide your source

On your `product.liquid` template (or other) wrap your source of tab content in a hidden div (you decide how; easiest is to hardcode `style="display:none"` onto the element).  For example:

```

<div class="product-description rte" itemprop="description">
  <div id="productDescription" style="display:none">    <---- We inline styled this 
  {{ product.description }}
  </div>
</div>

```

#### Add the tabs container and designate a source

Add this element to your template and indicate in the `data-source` the id of the source container.  Read the "What's going on here?" below to get an idea how this fits together.  Generally your code might now look something like this:

```
<div class="product-description rte" itemprop="description">
  <div class="jsTabsContainer" data-source="#productDescription"></div>   <---- We added this 
  <div id="productDescription" style="display:none">
    {{ product.description }}          
  </div>
</div>

```


## What's going on here

We're buildling a `ul` of tab menu items within the `.jsTabContainer` elements.  The titles for the tabs are the inner text of your source's H3 elements.  The tabs.js collects all nodes between H3 elements and pushes them into a new doc element which becomes the tab pane within the `.jsTabContainer`.
#Simple, Dynamic Shopify Product Tabs

A simple, dynamic implementation of shopify product tabs... but they don't necessarily have to be product tabs (you can use anywhere that you can indicate html within Shopify);

The motivation behind this was to create a simple way for clients to add tabs within product descriptions but for them not to write any code in the markup.  This simply relies on them formatting tab titles to be "Heading 3" (h3) elements and putting content in between.  They can use regular Shopify text editor to do this.

Much credit goes to [Shopify Docs implementation](https://docs.shopify.com/support/your-store/products/how-do-i-add-tabs-to-product-descriptions); but we extended it to make dynamic.

## Get started

#### Add the asset files

Add the `tabs.js` file to your assets folder and `theme.liquid` layout

Add the `tabs.scss` file to your assets folder and `theme.liquid` layout

#### Hide your source

On your `product.liquid` template (or other) wrap your source of tab content in a hidden div (you decide how; easiest is to hardcode `style="display:none"` onto the element).  For example:

```

<div class="product-description rte" itemprop="description">
  <div id="productDescription" style="display:none">    <---- We inline-styled this 
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

#### Write in the text editors

In your shopify admin, you can use the "Heading 3" (or H3) tag to indicate tab titles; everything between H3 tags becomes content of the preceding H3.  So for example

```
<h3>Details</h3>
<p>Some content of details</p>
<h3>Directions</h3>
<p>Some content of directions</p>
<ul>
<li>And a list</li>
<li>Of directions</li>
</ul>
```

Will create two tabs with titles "Details" and "Directions".  The "Details" tab will have a paragraph with "Some content of details" within it.  The "Directions" tab will have a paragraph of with "Some content of directions" and the list.

*BUT THE CLIENT DOESN'T HAVE TO ACTUALLY WRITE THE HTML*

Just have them write in the text editors and use the gui that Shopify provides, text editor buttons to style the titles as "Heading 3" and type everything else as they would.  We'll sort through what the text editor writes no behalf of the client.

## Improve the styling

There's basic styling provided to get started (which is essentially the styling provided by the Shopify tut)

## What's going on here?

We're buildling a `ul` of tab menu items within the `.jsTabsContainer` elements.  The titles for the tabs are the inner text of your source's H3 elements.  The tabs.js collects all nodes between H3 elements and pushes them into a new doc element which becomes the tab pane within the `.jsTabsContainer`.
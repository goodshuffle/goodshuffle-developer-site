---
weight: 10
title: Squarespace Setup
---

# Squarespace Setup

## Requirements

You will need...

- A Squarespace site with the business-level plan.
- Administrative credentials.
- The ability to copy and paste code-snippets.

## Overview

These are the high-level steps:

1. Activate you Website Wishlist Integration.
2. Add HTML code snippets to your site's header.
3. Add custom CSS to your site's design.
4. Create a page for the basic gallery and embed an HTML code snippet.

_If you prefer a narrated walk-through, checkout our [Squarespace Setup Youtube video](https://www.youtube.com/watch?reload=9&v=Ap5zhuijH90&feature=youtu.be)._

## Walk-Through

### Activation

You can do this from the [Integration Tab](https://pro.goodshuffle.com/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Inject in Site Header

You can access this by going to "Settings" &gt; "Advanced" &gt; "Code Injection"

**PLEASE NOTE! You need to update "YOUR-WEB-SITE-KEY" with your Public Browser Key from Goodshuffle Pro.**

```
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.1/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.1/dist/gspro-wc/gspro-wc.js"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
```

### Create a Gallery Page

1. Create a page to display a basic gallery of items.
2. Insert the following snippet in a `Code` block.

```
<gspro-item-gallery></gspro-item-gallery>
```

## All Set!

You should now have a basic page that displays a list of relevant categories/subcategories and your inventory.

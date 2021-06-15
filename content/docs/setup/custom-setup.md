---
weight: 30 
bookFlatSection: true 
title: "Custom Website Setup"
---

# Setup

## Step 1: Add Dependencies

Add the following code into your website `<head>...</head>` element. It will add our web components library and
reference your Goodshuffle Pro inventory. This is only needed on pages that you intend to display the wishlist or your
inventory.

### Required

```
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.0/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.0/dist/gspro-wc/gspro-wc.js"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
```

_Please Note: Your public web site key can be obtained from your Goodshuffle Pro Account Settings._

## Step 2: Test

To test your configuration, add this to a web page:

```
<gspro-item-gallery></gspro-item-gallery>
```

## Troubleshooting

- Are you using a valid public web site key?
- Is our webcomponent library downloading?

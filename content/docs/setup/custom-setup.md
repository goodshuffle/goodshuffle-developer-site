---
weight: 30 
bookFlatSection: true 
title: "Custom Website Setup"
---

# Setup

Use this guide for any site where you can edit the page's HTML. If your site is on Squarespace, WordPress, Wix,
Showit, GoHighLevel or Lovable, use [that builder's guide]({{< relref "/docs/setup" >}}) instead.

If your site is on version 0.5.x, see [Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## Step 1: Add the snippet

Add this to the `<head>...</head>` of every page that should show your inventory or the wishlist button. If your site
has a shared header template, put it there.

**Replace YOUR-PUBLIC-WEBSITE-KEY with the Public Browser Key from the
[Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations) of your Goodshuffle
Pro account.**

```
<script src="https://EMBED_HOST/v1/loader.js"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
```

> **Placeholder address.** `EMBED_HOST` stands in for the address the Website Integration will be served from. To be
> filled in when GSPRO-31872 ships: the final address. Until then, this tag loads nothing.

You don't need a footer snippet. `<gspro-wishlist-config>` adds the wishlist and item detail to the page.

> To be filled in when GSPRO-31872 ships: whether the script tag works both with and without `type="module"`, and
> whether it adds the styles itself or needs a stylesheet tag next to it.

## Step 2: Test

Add this to a page:

```
<gspro-item-gallery></gspro-item-gallery>
```

Open the page, pick a category, add an item to the wishlist with the heart, and send it. The quote request appears in
Goodshuffle Pro as a new project under Projects, Filters, Origin = "Website".

## Troubleshooting

- If nothing loads, check the Public Browser Key against the Integrations tab. Regenerating it in Goodshuffle Pro
  stops the old one at once.
- If the browser's network tab doesn't show `loader.js` loading, the script tag is missing or its address is wrong.
- Test on the website address saved for your brand in Goodshuffle Pro. Apart from a few builder preview addresses,
  inventory loads only there.

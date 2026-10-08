---
weight: 40
title: GoHighLevel Setup
---

# GoHighLevel Setup

On a GoHighLevel website or funnel, the snippet goes in the head tracking code, and each page that shows inventory
gets a custom code element.

## Requirements

You will need:

- A GoHighLevel website or funnel, published on your own domain.
- Access to edit its settings and pages.
- An active Website Integration on your Goodshuffle Pro account.

## Overview

1. Copy your Public Browser Key from Goodshuffle Pro.
2. Add the snippet to the head tracking code.
3. Add a gallery to a page with a custom code element.
4. Send a test quote request.

If your site is on version 0.5.x, replace the two script tags in your head tracking code. See
[Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## Walk-through

### 1. Copy your Public Browser Key

In Goodshuffle Pro, open the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
and activate the Website Integration if it isn't active yet. **Copy the Public Browser Key.**

![Integration Tab](/wordpress-website-integration-activation.png)

### 2. Add the snippet to the head tracking code

The snippet belongs in the code GoHighLevel adds to the `<head>` of your pages.

1. Open the website or funnel's **Settings**.
2. Find the **Tracking Code** section and its **Header** (head) box. Use the site-wide box if there is one, so the
   wishlist shows on every page. A single page's own settings have the same box if you only want it on that page.
3. Paste this snippet:

```
<script src="https://EMBED_HOST/v1/loader.js"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
```

> **Placeholder address.** `EMBED_HOST` stands in for the address the Website Integration will be served from. To be
> filled in when GSPRO-31872 ships: the final address. Until then, this tag loads nothing. Also to be filled in
> then: whether this tag adds the styles itself or needs a stylesheet tag next to it.

4. Replace `YOUR-PUBLIC-WEBSITE-KEY` with the key you copied.
5. Save.

To change settings, such as the wishlist's name or a required phone number, add attributes to
`<gspro-wishlist-config>`. See [Wishlist Config]({{< relref "/docs/components/wishlist-config" >}}).

### 3. Add a gallery to a page

1. Open the page in the editor.
2. Add a section and a row for the gallery, full width.
3. Add a **Custom JS/HTML** (custom code) element to the row.
4. Open the element's code editor and paste:

```
<gspro-item-gallery></gspro-item-gallery>
```

5. Save the element, then save and publish the page.

Paste only the gallery tag here. The script tag and settings element already come from the head tracking code; adding
them again on the page isn't needed.

For a fixed list of items without the search bar, use [`<gspro-item-list>`]({{< relref "/docs/components/item-list" >}})
instead.

### 4. Send a test quote request

On your published domain (not the editor preview):

1. Open the gallery page and pick a category.
2. Click the heart on an item to add it to the wishlist.
3. Open the wishlist, choose dates, then **Contact & Venue Info**.
4. Fill in your name and email, then **Send List**.

In Goodshuffle Pro, the request appears as a new project under **Projects**, **Filters**, Origin = "Website".

## Things to know on GoHighLevel

- **Test on your own domain.** Inventory loads on the website address saved for your brand in Goodshuffle Pro. The
  editor preview and GoHighLevel's preview links run on other addresses, so the gallery may stay empty there.
- **Funnel steps.** Each funnel step is its own page. A funnel-level head tracking code covers every step; a step's own
  tracking code covers only that step.
- **Your own forms.** GoHighLevel's forms and the wishlist are separate. A quote request sent from the wishlist goes to
  Goodshuffle Pro, not to your GoHighLevel contacts.

## When it doesn't work

- **No wishlist button.** Check that the snippet is in the Header box of the tracking code, that you saved, and that
  you republished the page.
- **The custom code element is empty.** Check that it holds only `<gspro-item-gallery></gspro-item-gallery>` and that
  you're on your published domain.
- **The button shows but no items load.** Check the key. If someone regenerated it in Goodshuffle Pro, copy it again.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

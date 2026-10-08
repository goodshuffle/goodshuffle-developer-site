---
weight: 25
title: Showit Setup
---

# Showit Setup

On Showit, you add the Website Integration with **Embed Code** elements: one in a canvas that shows on every page, for
the settings, and one on the page that shows your inventory.

## Requirements

You will need:

- A Showit site. The basic plan is enough.
- Access to the Showit design app for the site.
- An active Website Integration on your Goodshuffle Pro account.

## Overview

1. Copy your Public Browser Key from Goodshuffle Pro.
2. Add the snippet to your header canvas with an Embed Code element.
3. Add a gallery canvas to a page with a second Embed Code element.
4. Send a test quote request.

Already set up on version 0.5.x? Open the Embed Code element in your header canvas and replace the two script tags.
See [Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## Walk-Through

### 1. Copy your Public Browser Key

In Goodshuffle Pro, open the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
and activate the Website Integration if it isn't active yet. **Copy the Public Browser Key.**

![Integration Tab](/wordpress-website-integration-activation.png)

### 2. Add the snippet to your header canvas

Your header canvas shows on every page, so the snippet goes there.

1. In the left menu, open the **Site** tab, then **Site Canvases**.
2. Select your header canvas. On a new Showit site it is called "Header"; yours may have another name.
3. Click inside the header on the page, so you are editing the header canvas.
4. In the toolbar at the bottom of the page, click the middle button and choose **Embed Code**.

![Embed HTML](/showit-embed.png)

5. Double-click the black box that appears in the header.
6. Paste this snippet:

```
<script src="https://EMBED_HOST/v1/loader.js"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
```

> **Placeholder address.** `EMBED_HOST` stands in for the address the Website Integration will be served from. To be
> filled in when GSPRO-31872 ships: the final address. Until then, this tag loads nothing.

7. Replace `YOUR-PUBLIC-WEBSITE-KEY` with the key you copied.
8. Click **Save**.

The settings element shows nothing itself, so the box can stay small. To change settings, such as the wishlist's name
or a required phone number, add attributes to `<gspro-wishlist-config>`. See
[Wishlist Config]({{< relref "/docs/components/wishlist-config" >}}).

### 3. Add a gallery canvas to a page

1. Open the **Page** tab.
2. Click the three dots next to the page's name and choose **Add Blank Canvas**.
3. Rename the new canvas "Gallery".
4. Set the canvas height on both the **Desktop** and **Mobile** views. Start with 3000px and adjust once you see your
   inventory.
5. Add an **Embed Code** element to the canvas, as in step 2, and paste:

```
<gspro-item-gallery></gspro-item-gallery>
```

6. Drag the element's corners, or set its size on the right, so it fills the canvas. Do this on Desktop and Mobile.
7. Save and publish.

Showit doesn't grow a canvas to fit its content. If the gallery is cut off at the bottom, make the canvas and the
element taller.

### 4. Send a test quote request

On your published site:

1. Open the gallery page and pick a category.
2. Click the heart on an item to add it to the wishlist.
3. Open the wishlist, choose dates, then **Contact & Venue Info**.
4. Fill in your name and email, then **Send List**.

In Goodshuffle Pro, the request appears as a new project under **Projects**, **Filters**, Origin = "Website".

## When it doesn't work

- **No wishlist button.** Check that the snippet is in the header canvas, that the canvas shows on this page, and that
  you published.
- **The gallery is cut off.** Make the canvas and the Embed Code element taller, on Desktop and on Mobile.
- **Items load on your domain but not on a Showit preview address.** Inventory loads on the website address saved for
  your brand in Goodshuffle Pro. Test on your published site.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

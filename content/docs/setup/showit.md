---
weight: 25
title: Showit Setup
---

# Showit Setup

## Requirements

You will need...

1. A Showit subscription (basic tier is sufficient)
2. Access to the Showit site dashboard
3. The ability to copy and paste code snippets
4. Your Goodshuffle Website Wishlist Integration public browser key

## Overview

These are the high-level steps:

1. Activate you Website Wishlist Integration.
2. Add HTML code snippets to your page's header and footer.
3. Create a page for the basic gallery and embed an HTML code snippet.

This document will guide you through setting up a basic Wishlist on a Showit site, but more customization will likely be desired. This customization is intuitive thanks to Showit's easy to use drag-and-drop interface

We encourage you to experiment with personalizing your site after running through these basic setup instructions.

## Walk-Through
### Activation

You can do this from the [Integration Tab](https://pro.goodshuffle.com/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Inject in Page Header

Select a Page from the Site Menu &gt; Click Page Tab &gt; Advanced Settings on the right &gt; Custom Head HTML &gt; Paste the below Snippet

**PLEASE NOTE! You need to update "YOUR-WEB-SITE-KEY" with your Public Browser Key from Goodshuffle Pro.**

```
<meta name="gspro-config"
      content="https://data.goodshuffle.com/vendor/YOUR_WEB_SITE_KEY" />
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.4.4/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.4.4/dist/gspro-wc/gspro-wc.js"></script>
<script src="https://unpkg.com/tua-body-scroll-lock"></script>
```

If this is a brand new Showit site, proceed to the next step. 

For existing Showit sites, repeat this step for every page where clients will interact with your Wishlist.

**NOTE**: This step must be done on **every** page where you want your Wishlist to be visible.

### Create Wishlist Canvas 

From the site tab:

1. Go to the Site Canvases section of the Site tab
2. Click the Plus Sign button next to Site Canvases
3. Select Add Blank Site Canvas
4. Change the Canvas name to "Wishlist" (double click "New Site Canvas")

On the canvas options (right side of screen), repeat the following steps for both the "Mobile" and "Desktop" tab:

1. Change initial height to 80
2. Change the "Sticky" dropdown to "Bottom"

On the bottom toolbar, highlight the middle Icon and select "Embed Code". The "Embed Code" option is the selected by clicking the middle button (see image).

_Example: How to insert code into a Showit canvas_

![Embed HTML](/showit-embed.png)

A black box will appear with the text "Enter iframe URL or embed code in properties panel".

Double click that box and paste the following snippet inside.

```
<div class="gspro-gallery-omni-present">
  <gspro-wishlist></gspro-wishlist>
  <gspro-item-detail
    data-mode="inactive"
    class="gspro-u-fullscreen"
    route="/item/:id/:title*"></gspro-item-detail>
  <gspro-sprite></gspro-sprite>
</div>
```

Resize the blue rectangle (it will appear empty) and move it to the far right of the Canvas.

We have now created a Canvas that contains our Wishlist "cart" icon.

We will add this canvas to your page in the following step.

### Add "Wishlist Cart" Canvas to Page

From the site tab:

1. Click the page where you injected the header in the first step
2. Click the "Page" tab
3. Click on the three dots to the right of the page name
4. Select Add New Canvas
5. Select the "Wishlist" component (which we created in the above step)
6. Click "Add" in the bottom right

### Add a Gallery to the Page

Remain on the Page tab:

1. Click the three dots to the right of the page name
2. Select "Add Blank Canvas"
3. Double Click "New Canvas" and rename to Gallery
4. Click on the Gallery Canvas
5. Click inside the page on the blue button labelled "Gallery"
6. Embed HTML. This is exactly the same as the process described in Create Wishlist Canvas above
7. Paste the following snippet into the popup

```
<gspro-item-gallery></gspro-item-gallery>
```

On the left hand Page tab, drag your Wishlist canvas so that it is **below** the Gallery canvas.

That's it!






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

This document will guide you through setting up a basic Wishlist on a Showit site, but more customization will likely be desired. This customization is intuitive thanks to Showit's easy to use drag-and-drop interface.

We encourage you to experiment with personalizing your site after running through these basic setup instructions.

## Walk-Through
### Activation

If you'd prefer to follow along with a video tutorial, we have one [available here](https://www.youtube.com/watch?v=gYZod6-o4hk)!

You can do this from the [Integrations Tab](https://pro.goodshuffle.com/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Inject in Page Header

To inject code in your page header, you will need to inject code into your site's "Header" Canvas by following the steps below:

1. Go to the Site Canvases menu (under the Site tab of the lefthand menu)
2. Select the Header Canvas (if this is an existing Showit site, your header may be named something different)
3. Click inside the Header on your page so that you are editing the Header Canvas
4. Click on the middle button of the button grouping at the bottom of the page (shown in the image below)
   
![Embed HTML](/showit-embed.png)

6. Select Embed Code
7. Double click on the black box that appears on the header
8. Paste the below code snippet into the box:
```
<meta name="gspro-config"
      content="https://data.goodshuffle.com/vendor/YOUR_WEB_SITE_KEY" />
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.4.4/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.4.4/dist/gspro-wc/gspro-wc.js"></script>
<script src="https://unpkg.com/tua-body-scroll-lock"></script>
```

**PLEASE NOTE! You need to update "YOUR-WEB-SITE-KEY" with your Public Browser Key from Goodshuffle Pro.**

9. Click Save
10. Your Wishlist is now installed on your site
11. Proceed to the next section


### Create Wishlist Canvas 

From the site tab:

1. Go to the Site Canvases section of the Site tab
2. Click the Plus Sign button next to Site Canvases
3. Select Add Blank Site Canvas
4. Change the Canvas name to "Wishlist" (double click New Site Canvas)

On the Canvas options (right side of screen), repeat the following steps for both the Mobile and Desktop tabs:

1. Change initial height to 80
2. Change the "Sticky" dropdown to "Bottom"

On the bottom toolbar, highlight the middle Icon and select "Embed Code". The "Embed Code" option is the selected by clicking the middle button (see image).

_Example: How to insert code into a Showit Canvas_

![Embed HTML](/showit-embed.png)

A black box will appear with the text "Enter iframe URL or embed code in properties panel".

Double click that box and paste the following snippet inside:

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

We will add this Canvas to your page in the following step.

### Add "Wishlist Cart" Canvas to Page

From the site tab:

1. Click the page where you injected the header in the first step
2. Click the Page tab
3. Click on the three dots to the right of the page name
4. Select Add New Canvas
5. Select the "Wishlist" component (which we created in the above step)
6. Click Add in the bottom right

### Add a Gallery to the Page

Remain on the Page tab:

1. Click the three dots to the right of the page name
2. Select Add Blank Canvas
3. Double click New Canvas and rename to "Gallery"
4. Click on the Gallery Canvas
5. Click inside the page on the blue button labelled "Gallery"
6. Give this new Gallery Canvas a height of 800px on the right side of the screen.
7. Embed HTML. This is exactly the same as the process described in Create Wishlist Canvas above
8. Paste the following snippet into the popup:

```
<gspro-item-gallery></gspro-item-gallery>
```

8. Make sure to resize your gallery iframe to fit your page. You can either drag and drop the corners of the blue box containing your gallery, or change the numerical values on the right side of the screen.

On the left hand Page tab, drag your Wishlist Canvas so that it is **below** the Gallery Canvas.

That's it!






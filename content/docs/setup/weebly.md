---
weight: 10
title: Weebly Setup
---

# Weebly Setup

## Requirements

You will need...

- A Weebly website
- Your login credentials for the Weebly website
- The ability to copy and paste code-snippets.

## Overview

These are the high-level steps:

1. Activate you Website Wishlist Integration.
2. Add HTML code snippets to your site's header and footer.
3. Add custom CSS to your site's design.
4. Create a page for the basic gallery and embed an HTML code snippet.

## Walk-Through

### Activation

You can do this from the [Integration Tab](https://pro.goodshuffle.com/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Inject in Site Header

#### Add Custom Header Code
1. Go to your Weebly Site Editor
2. Click the button that says "Settings" on the top toolbar
3. Scroll down to the section labelled "Header Code"
4. Paste the following snippet into that box

**PLEASE NOTE! You need to update "YOUR-WEB-SITE-KEY" with your Public Browser Key from Goodshuffle Pro.**

```
<meta name="gspro-config"
      content="https://data.goodshuffle.com/vendor/YOUR_WEB_SITE_KEY" />
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.4.4/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.4.4/dist/gspro-wc/gspro-wc.js"></script>
<script src="https://unpkg.com/tua-body-scroll-lock"></script>
```

### Add Custom Footer Code

1. Stay on the same page where you added the header code
2. Find the box labelled "Footer Code"
3. Paste the following snippet into that box:

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

### Create a Gallery Page

1. From the top menu, click "Pages"
2. Click the "+" icon next to Pages to create a new page
3. Select Standard Page
4. Give your page a name, such as "Rentals"
5. From the top menu, click "Build"
6. Drag the button that says "Embed Code" into the page section labelled "Drag Elements Here"
7. Click where it says "Click to set custom HTML"
8. Click "Edit Custom HTML" on the popup that appears
9. Paste the following snippet into the box

```
<gspro-item-gallery></gspro-item-gallery>
```

Make sure to publish your changes!

## All Set!

You should now have a basic page that displays a list of relevant categories/subcategories and your inventory.

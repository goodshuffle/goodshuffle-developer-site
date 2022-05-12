---
weight: 20
title: WordPress Setup
---

# WordPress Setup

## Requirements

You will need...

- WordPress version 5 or better.
- An active "Website Wishlist" subscription on Goodshuffle Pro.

## Overview

These are the high-level steps:

1. [Download the WordPress plugin](https://goodshufflecdn.s3.amazonaws.com/gspro-embed-wpp/gspro-wishlist-plugin-0.5.2.zip).
1. Activate your Website Wishlist integration.
1. Upload the plugin to your site.
1. Configure the plugin to use you public web key.
1. Create a page to display a basic gallery.

If you prefer a narrated walk-through, checkout our [WordPress Setup Youtube video](https://www.youtube.com/watch?v=gzxL2LPECr0).

## Detailed Walk-Through

### Activation

You can do this from the [Integration Tab](https://pro.goodshuffle.com/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Installation

1. Sign into your WordPress site using an account that has administrative access.
1. Select the “Plugins” item on the left sidebar.
1. At the top of the main area, click the “Add New” button.
1. At the top of the main area, click the “Upload Plugin” button.
1. Click “Choose File” to locate and select the plugin you downloaded.
1. Click “Install Now”.
1. Click “Activate Plugin”.

You should now see “Goodshuffle Embedded Catalog” in your list of plugins.

### Configuration

1. Click the "Settings" link beneath "Goodshuffle Embedded Catalog".
1. Enter the "Web Key" that you obtained earlier.
1. Set "Display Inventory on Page" with the slug of the page you want to display your inventory. Using the name "goodshuffle" is good for testing and evaluation purposes. You will be able to change it later.
1. Leave the "Default Category" blank for now and the "Display wishlist on all pages blank for now."
1. Press the "Update Options" button to save your changes.

You should now be able to add a basic gallery to display your inventory.

![Wordpress Settings](/wordpress-settings-screen.png)

### Create a Basic Gallery

1. Select the “Pages” item on the left sidebar.
1. Click “Add New” to create a new page.
1. Enter a title for the page (e.g. Goodshuffle)
1. Click Publish in the top right.

When you view that page, you should now see a basic gallery that includes category and subcategory filters.

## Next Steps

1. Apply your colors and typography to the web components.
1. Learn how to use the `<gspro-item-list>` to create [customized lists]({{< relref "/docs/customization/colors-and-typography" >}}) of your items.

![Basic Gallery](/wordpress-basic-gallery.png)

---
weight: 35
title: Wix Setup
---

# Wix Setup

## Requirements

Using the Website Integration on a WIX site requires any paid or premium plan. The "Light" plan will work and is recommended by Goodshuffle Pro.

## Overview

These are the high-level steps:

1. Activate your Website Integration.
2. Create a page for the basic gallery.
3. Add Custom Elements to your site via the Wix Editor.

## Walk-Through

### Activation

You can do this from the [Integration Tab](https://pro.goodshuffle.com/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Adding the correct code to the Header of your Wix site

To get started, first head to your Wix site editor. You can get there on most WIX sites by clicking "Home" and then clicking "Design Site" or "Edit Site"

![Wix Dashboard](/wix-dashboard.png)

Now that we're in the right place, we need to set the Website Integration up in your site's header. You can do this by clicking " Add Elements" and then "Add Custom Element"

![Wix Editor](/wix-editor.png)

Now that you have this element added watch the video below to learn more about what you need to copy/paste:

For a detailed video of how to perform this step [See Here](https://www.youtube.com/watch?v=GsAs8J6mVUM)

Custom Element Properties:

Source:

- Server URL: `https://unpkg.com/@goodshuffle/gspro-wc@0.5.8/dist/custom-elements/index.js`
- Tag Name: `gspro-wishlist-config`

Attributes (These are two separate Attributes):

First:

- Name: `data-url`
- Value: `https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY`

Second:

- Name: `disable-body-scroll-lock`
- Value: `true`

#### Note: Don't forget to get the Public Browser Key from your account in the Integrations Tab!

You'll know you have things connected correctly if, after clicking "Publish", you see this icon on the front end of your site:

![Wix Config Preview](/wix-config-preview.png)

### Listing inventory items

We've connected our inventory—great! Let's make it appear on a page with an Item Gallery and an Item List.

Wherever you'd like to list items, click "Add Element" and add a custom element,

![Wix Editor](/wix-editor.png)

From here, we'll adjust the Server URL and the tags again — learn more in [this video](https://www.youtube.com/watch?v=w9Spx86UCss).

Source:

- Server URL: `https://unpkg.com/@goodshuffle/gspro-wc@0.5.8/dist/custom-elements/index.js`
- Tag Name: `gspro-item-gallery` or `gspro-item-list`

Attributes (if using `gspro-item-list`):

- Name: `tags` or `category` (Note - this can change depending on what you'd like listed)
- Value: a tag or category of your choosing.

#### Note: If you need help figuring out what value to provide for your desired category reference [this doc](https://help.goodshuffle.com/en/articles/5274417-how-do-i-find-the-code-for-my-item-categories-to-display-a-category-on-a-web-page).

## All Set!

You should now have a basic page that displays a list of relevant categories/subcategories and your inventory.
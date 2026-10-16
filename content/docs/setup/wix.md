---
weight: 30
title: Wix Setup
---

# Wix Setup

On Wix, each part of the Website Integration is a **Custom Element** that you add in the Wix Editor. Every Custom
Element uses the same Server URL; the Tag Name and attributes say what it shows.

## Requirements

You will need:

- A paid Wix plan. Custom Elements need one; the Light plan works.
- Access to the Wix Editor for the site.
- An active Website Integration on your Goodshuffle Pro account.

## Overview

1. Copy your Public Browser Key from Goodshuffle Pro.
2. Add the settings Custom Element to your site header.
3. Add a gallery Custom Element to a page.
4. Send a test quote request.
5. Optional: add a lead form.

If your site is on version 0.5.x, open each Goodshuffle Custom Element and replace its Server URL with the one
below. Nothing else changes. See [Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## The Server URL

Every Goodshuffle Custom Element on your site uses this Server URL:

{{< embed-code lang="text" >}}
LOADER_URL
{{< /embed-code >}}

This one file is all Wix needs. It adds the release's stylesheet, `gspro-embed.css`, and its script,
`gspro-embed.js`, to the page's `<head>`. It adds them once per page, however many Custom Elements use it. If two
elements on a page have different Server URLs, the first one to run decides which release loads, so keep them all the
same.

The address pins version {{< embed-version >}}, so your site changes only when you change that number on every Custom
Element. See [Updating to a newer version]({{< relref "/docs/setup/updating" >}}), or
[Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}) to get 1.x fixes without
editing.

Older instructions used an address ending in `/dist/custom-elements/index.js`. Don't use it for new setups: it loads
version 0.5.x, which no longer gets fixes.

## Walk-through

### 1. Copy your Public Browser Key

In Goodshuffle Pro, open the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
and activate the Website Integration if it isn't active yet. **Copy the Public Browser Key.**

![Integration Tab](/wordpress-website-integration-activation.png)

### 2. Add the settings Custom Element to your header

1. Open the Wix Editor. From your site's dashboard, this is usually **Edit Site** or **Design Site**.

![Wix Dashboard](/wix-dashboard.png)

2. Click **Add Elements**, then **Embed Code**, then **Custom Element**.

![Wix Editor](/wix-editor.png)

3. Drag the new element into your site's **header**. That puts it on every page.
4. Click **Choose Source** and set:
   - **Server URL**: the Server URL above.
   - **Tag Name**: `gspro-wishlist-config`
5. Click **Set Attributes** and add two attributes, one at a time:

| Name | Value |
| --- | --- |
| `data-url` | `https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY` |
| `disable-body-scroll-lock` | `true` |

6. Replace `YOUR-PUBLIC-WEBSITE-KEY` with the key you copied.
7. Click **Publish**.

On your published site, the wishlist button (a heart with a count) now shows on every page.

![Wix Config Preview](/wix-config-preview.png)

`disable-body-scroll-lock` keeps your Wix page scrolling normally while item detail is open. Add any other settings the
same way, as attributes on this element. See [Wishlist Config]({{< relref "/docs/components/wishlist-config" >}}) for
the full list. For example, to require a phone number, add the attribute `require-phone-number` with the value `true`.

### 3. Add a gallery to a page

1. Open the page that should show your inventory.
2. Click **Add Elements**, then **Embed Code**, then **Custom Element**, and place it on the page.
3. Click **Choose Source** and set:
   - **Server URL**: the same Server URL.
   - **Tag Name**: `gspro-item-gallery`
4. Resize the element to fill the width and height you want for the gallery.
5. Click **Publish**.

For a fixed list of items without the search bar, use the Tag Name `gspro-item-list` instead, and add an attribute such
as `category` or `tags`. See [Item List]({{< relref "/docs/components/item-list" >}}). To find a category's value, see
[this help article](https://help.goodshuffle.com/en/articles/5274417-how-do-i-find-the-code-for-my-item-categories-to-display-a-category-on-a-web-page).

### 4. Send a test quote request

On your published site:

1. Open the gallery page and pick a category.
2. Click the heart on an item to add it to the wishlist.
3. Open the wishlist, choose dates, then **Contact & Venue Info**.
4. Fill in your name and email, then **Send List**.

In Goodshuffle Pro, the request appears as a new project under **Projects**, **Filters**, Origin = "Website".

### 5. Add a lead form

A lead form shows one of your Goodshuffle Pro Custom Forms on a page, styled by your site. See
[Lead Form]({{< relref "/docs/components/lead-form" >}}). On Wix it's one more Custom Element.

<!-- GSPRO-32476: the form's Share section gets the "Website Integration code" row (goodshuffle PR #9099). Match this
step to that screen once it ships. -->

1. In Goodshuffle Pro, open the form and make sure it's published. Find the **Website Integration code** in the
   form's **Share** section and copy the address inside `form="..."`, `https://www.goodshuffle.com/c/f/FORM_ID`.
2. In the Wix Editor, open the page where the form should go.
3. Click **Add Elements**, then **Embed Code**, then **Custom Element**, and place it on the page.
4. Click **Choose Source** and set:
   - **Server URL**: the [Server URL](#the-server-url) above.
   - **Tag Name**: `gspro-lead-form`
5. Click **Set Attributes** and add one attribute:

| Name | Value |
| --- | --- |
| `form` | The share link you copied, `https://www.goodshuffle.com/c/f/FORM_ID` |

6. Resize the element so the whole form fits. Leave extra height below it for questions that appear depending on
   earlier answers, and for error messages.
7. Click **Publish**.
8. On your published site, fill in the form and click **Submit**. The response shows in the form's **Responses** in
   Goodshuffle Pro.

<!-- GSPRO-32473: submit and Responses for the lead form land with GSPRO-32473. Confirm this check then. -->

The form doesn't need the settings element from step 2. If you only want forms on your site, this is the only step
you need.

## Things to know on Wix

- **Attribute values are typed by hand.** On/off attributes turn off only with the lowercase word `false`. Any other
  value turns them on, including `False`. To keep an option at its default, leave the attribute out. Some options
  default to on (`wishlist-show-on-all-pages`, `show-categories`, `show-filters`). Leaving those out keeps them on.
  To turn one off, set it to `false`.
- **One settings element.** Put `gspro-wishlist-config` in the header once. A second copy on a page is ignored.
- **The videos.** Our earlier Wix videos ([header](https://www.youtube.com/watch?v=GsAs8J6mVUM),
  [listing items](https://www.youtube.com/watch?v=w9Spx86UCss)) show the steps, but with the old Server URL. Use the
  Server URL on this page.

## When it doesn't work

- **No wishlist button.** Check that the settings element's Tag Name is exactly `gspro-wishlist-config`, that it sits
  in the header, and that you published.
- **The gallery element is empty.** Check its Server URL and Tag Name, and that the settings element's `data-url` has
  your key.
- **Items don't load in the Editor preview.** Inventory loads on the website address saved for your brand in
  Goodshuffle Pro. The Editor preview runs on another address, and the gallery may stay empty there. Test on your
  published domain, and check that it matches the address saved in Goodshuffle Pro.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

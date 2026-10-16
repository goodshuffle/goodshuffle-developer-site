---
weight: 10
title: Squarespace Setup
---

# Squarespace Setup

## Requirements

You will need:

- A Squarespace plan that includes Code Injection.
- Administrator access to the site.
- An active Website Integration on your Goodshuffle Pro account.

## Overview

1. Copy your Public Browser Key from Goodshuffle Pro.
2. Add the snippet to your site header with Code Injection.
3. Add a gallery to a page with a Code block.
4. Send a test quote request.
5. Optional: add a lead form.

If your site is on version 0.5.x, you only need to replace your script tags. See
[Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## Walk-through

### 1. Copy your Public Browser Key

In Goodshuffle Pro, open the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
and activate the Website Integration if it isn't active yet. **Copy the Public Browser Key.**

![Integration Tab](/wordpress-website-integration-activation.png)

### 2. Add the snippet to your site header

1. In Squarespace, go to **Website** > **Pages** > **Custom Code** > **Code Injection**.
2. Paste this snippet into the **Header** box:

{{< embed-code >}}
<script src="LOADER_URL"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
{{< /embed-code >}}

> The script tag also adds the release's stylesheet, `gspro-embed.css`, so you don't need a stylesheet tag. It pins version {{< embed-version >}}. See
> [Updating to a newer version]({{< relref "/docs/setup/updating" >}}), or
> [Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}) to get 1.x fixes
> without editing.

3. Replace `YOUR-PUBLIC-WEBSITE-KEY` with the key you copied. Leave the rest as is.
4. Click **Save**.

Code Injection runs on every page. The wishlist button now shows across your site.

To change how the Website Integration behaves (rename the wishlist, require a phone number, hide time selection), add
attributes to the `<gspro-wishlist-config>` tag here. See [Wishlist Config]({{< relref "/docs/components/wishlist-config" >}}).

### 3. Add a gallery to a page

1. Create a page for your inventory, for example "Rentals".
2. Add a **Code** block to the page.
3. Paste this into the block:

```
<gspro-item-gallery></gspro-item-gallery>
```

4. Save and publish the page.

The gallery shows a search bar, your categories and filters. Pick a category to see its items. To show a fixed set of
items without the search bar, use [`<gspro-item-list>`]({{< relref "/docs/components/item-list" >}}) instead.

### 4. Send a test quote request

On your published site (not the editor preview):

1. Open the gallery page and pick a category.
2. Click the heart on an item to add it to the wishlist.
3. Open the wishlist, choose dates, then **Contact & Venue Info**.
4. Fill in your name and email, then **Send List**.

In Goodshuffle Pro, the request appears as a new project under **Projects**, **Filters**, Origin = "Website".

### 5. Add a lead form

A lead form shows one of your Goodshuffle Pro Custom Forms on a page, styled by your site. See
[Lead Form]({{< relref "/docs/components/lead-form" >}}).

<!-- GSPRO-32476: the form's Share section gets the "Website Integration code" row (goodshuffle PR #9099). Match this
step to that screen once it ships. -->

1. In Goodshuffle Pro, open the form and make sure it's published. Copy the **Website Integration code** from the
   form's **Share** section. It's a `<gspro-lead-form>` tag with your form's link in `form`:

```
<gspro-lead-form form="https://www.goodshuffle.com/c/f/FORM_ID"></gspro-lead-form>
```

2. In Squarespace, open the page where the form should go and add a **Code** block.
3. Paste the tag into the block.
4. Save and publish the page.
5. On your published site, fill in the form and click **Submit**. The response shows in the form's **Responses** in
   Goodshuffle Pro.

The form needs only the script tag from step 2. If you only want forms on your site, paste just this line into
Code Injection's **Header** box. You can leave out `<gspro-wishlist-config>`:

{{< embed-code >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

## Common changes

- **Hide the venue fields.** In **Website** > **Pages** > **Custom Code** > **Custom CSS**, add
  `.gspro-c-wishlist__venue { display: none !important; }`.
- **Colors and fonts.** See [Colors and Typography]({{< relref "/docs/customization/colors-and-typography" >}}).

## When it doesn't work

- **No wishlist button anywhere.** Check that the snippet is in Code Injection and that you saved.
- **The button shows but no items load.** Check the key. If someone regenerated it in Goodshuffle Pro, copy it again.
- **Items load on a `squarespace.com` address but not on your own domain.** Inventory loads on the website address
  saved for your brand in Goodshuffle Pro. Check that it matches your domain.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

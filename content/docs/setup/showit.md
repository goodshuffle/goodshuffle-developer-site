---
weight: 40
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
5. Optional: add a lead form.

If your site is on version 0.5.x, open the Embed Code element in your header canvas and replace the two script
tags. See [Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## Walk-through

### 1. Copy your Public Browser Key

In Goodshuffle Pro, open the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
and activate the Website Integration if it isn't active yet. **Copy the Public Browser Key.**

![Integration Tab](/wordpress-website-integration-activation.png)

### 2. Add the snippet to your header canvas

The snippet goes in your header canvas, which shows on every page.

1. In the left menu, open the **Site** tab, then **Site Canvases**.
2. Select your header canvas. On a new Showit site it is called "Header"; yours may have another name.
3. Click inside the header on the page to edit the header canvas.
4. In the toolbar at the bottom of the page, click the middle button and choose **Embed Code**.

![Embed HTML](/showit-embed.png)

5. Double-click the black box that appears in the header.
6. Paste this snippet:

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

7. Replace `YOUR-PUBLIC-WEBSITE-KEY` with the key you copied.
8. Click **Save**.

The box can stay small: the settings element shows nothing itself. To change settings, such as the wishlist's name
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

6. Make the element fill the canvas by dragging its corners or setting its size on the right. Do this on Desktop and
   Mobile.
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

### 5. Add a lead form

A lead form shows one of your Goodshuffle Pro Custom Forms on a page, styled by your site. See
[Lead Form]({{< relref "/docs/components/lead-form" >}}).

1. In Goodshuffle Pro, open the form and make sure it's published. In its **Share** section, copy the lead form tag.
   It looks like this, with your form's link in `form`:

```
<gspro-lead-form form="https://www.goodshuffle.com/c/f/FORM_ID"></gspro-lead-form>
```

2. On the page where the form should go, add a canvas for it, as in step 3.
3. Add an **Embed Code** element to the canvas, as in step 2, and paste the tag.
4. Make the canvas and the element tall enough for the whole form, on Desktop and Mobile.
5. Save and publish.
6. On your published site, fill in the form and click **Submit**. The response shows in the form's **Responses** in
   Goodshuffle Pro.

<!-- GSPRO-32473: submit and Responses for the lead form land with GSPRO-32473. Confirm this check then. -->

The form needs only the script tag from step 2. If you only want forms on your site, paste just this line into the
Embed Code element in your header canvas. You can leave out `<gspro-wishlist-config>`:

{{< embed-code >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

## When it doesn't work

- **No wishlist button.** Check that the snippet is in the header canvas, that the canvas shows on this page, and that
  you published.
- **The gallery is cut off.** Make the canvas and the Embed Code element taller, on Desktop and on Mobile.
- **Items load on your domain but not on a Showit preview address.** Inventory loads on the website address saved for
  your brand in Goodshuffle Pro. Test on your published site.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

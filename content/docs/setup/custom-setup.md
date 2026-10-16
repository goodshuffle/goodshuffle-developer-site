---
weight: 70
bookFlatSection: true 
title: "Custom Website Setup"
---

# Setup

Use this guide for any site where you can edit the page's HTML. If your site is on Squarespace, WordPress, Wix,
Showit, GoHighLevel or Lovable, use [that builder's guide]({{< relref "/docs/setup" >}}) instead.

If your site is on version 0.5.x, see [Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## Step 1: Add the snippet

Add this to the `<head>...</head>` of every page that should show your inventory or the wishlist button. If your site
has a shared header template, put it there.

**Replace YOUR-PUBLIC-WEBSITE-KEY with the Public Browser Key from the
[Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations) of your Goodshuffle
Pro account.**

{{< embed-code >}}
<script src="LOADER_URL"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
{{< /embed-code >}}

You don't need a footer snippet. `<gspro-wishlist-config>` adds the wishlist and item detail to the page.

### What the script tag does

`loader.js` is small. It adds two things to the page's `<head>`, both from the same release folder:

- a stylesheet, `gspro-embed.css`, so you don't add a stylesheet tag of your own;
- the Website Integration itself, `gspro-embed.js`.

It works as a plain `<script>` tag, as shown, and also with `type="module"` if your site adds every script that way.
If the page already has a `gspro-embed.js` script from any release, it adds nothing. So when the tag is on a page
twice, the first copy to run decides which release loads. It doesn't look for the 0.5.x `gspro-wc` scripts: if your
page still has those, remove them. See [Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

The address pins version {{< embed-version >}}, so your site changes only when you change that number. See
[Updating to a newer version]({{< relref "/docs/setup/updating" >}}), or
[Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}) to get 1.x fixes without
editing.

## Step 2: Test

Add this to a page:

```
<gspro-item-gallery></gspro-item-gallery>
```

Open the page, pick a category, add an item to the wishlist with the heart, and send it. The quote request appears in
Goodshuffle Pro as a new project under Projects, Filters, Origin = "Website".

## Troubleshooting

- If nothing loads, check the Public Browser Key against the Integrations tab. Regenerating it in Goodshuffle Pro
  stops the old one at once.
- If the browser's network tab doesn't show `loader.js` loading, the script tag is missing or its address is wrong.
- Test on the website address saved for your brand in Goodshuffle Pro. Apart from a few builder preview addresses,
  inventory loads only there.

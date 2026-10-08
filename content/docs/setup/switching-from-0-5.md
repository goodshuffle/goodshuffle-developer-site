---
weight: 2
title: "Switching from 0.5.x"
---

# Switching from 0.5.x

If your site loads the Website Integration from `unpkg.com/@goodshuffle/gspro-wc@0.5...`, you're on version 0.5.x.
Switching to the current version is one change to your site header. After that, every fix and improvement reaches
your site without another edit.

## What to change

In your site header, find the two script tags that load `gspro-wc`. They look like this, with your version number in
place of `0.5.7`:

```
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.7/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.7/dist/gspro-wc/gspro-wc.js"></script>
```

Replace both with this one tag:

```
<script src="https://EMBED_HOST/v1/loader.js"></script>
```

> **Placeholder address.** `EMBED_HOST` stands in for the address the Website Integration will be served from. To be
> filled in when GSPRO-31872 ships: the final address. Until then, this tag loads nothing.

Leave your `<gspro-wishlist-config>` tag where it is, and save or publish your site.

Where the header lives depends on your site builder:

| Builder | Where the two tags are |
| --- | --- |
| Squarespace | Code Injection, Header. See [Squarespace]({{< relref "/docs/setup/squarespace" >}}) |
| WordPress | Inside the Goodshuffle plugin. Update the plugin instead of editing tags. See [WordPress]({{< relref "/docs/setup/wordpress" >}}) |
| Wix | No script tags. Change the Server URL on each Custom Element. See [Wix]({{< relref "/docs/setup/wix" >}}) |
| Showit | The Embed Code element in your header canvas. See [Showit]({{< relref "/docs/setup/showit" >}}) |
| GoHighLevel | The page or site Head tracking code. See [GoHighLevel]({{< relref "/docs/setup/gohighlevel" >}}) |
| Lovable | `index.html`. See [Lovable]({{< relref "/docs/setup/lovable" >}}) |
| Any other site | The page `<head>`. See [Custom Website]({{< relref "/docs/setup/custom-setup" >}}) |

## What stays the same

- Your `<gspro-wishlist-config>` tag and its Public Browser Key.
- Every `<gspro-item-gallery>`, `<gspro-item-list>` and `<gspro-item-card>` on your pages, and every attribute on them.
- Your own CSS. The class names it targets, such as `gspro-c-item-card` and `gspro-c-wishlist__venue`, are unchanged.
- Your listeners for `gspro-wishlist.submit` and `gspro-wishlist.submit-complete`, as long as they read `contact`,
  `venue` or the number of items. See below for the item fields.
- Links into your catalog, such as `#!/inventory/...` and `#!/item/...`.
- Wishlists your clients already started. They carry over to the new version.

## What's different

Check these if your site has custom JavaScript.

| On 0.5.x | Now |
| --- | --- |
| `gspro-item-card.click`, `gspro-item-card.add` and `gspro-item-detail.add` fire when a client opens or adds an item | Not fired. Listeners for them stop running |
| Each entry in an event's `detail.wishlist` is the whole item: category, tags, attributes and more | Each entry holds the item's ID, name, photo, price, quantity, price type and dates. See [Events]({{< relref "/docs/integrations/events" >}}) |
| `gspro-wishlist.submit` fires on every click of Send List, even while a send is in progress | Fires once per send |
| The two script tags | One tag. To be filled in when GSPRO-31872 ships: whether that tag also adds the styles, or a stylesheet tag goes with it |

If you rely on any of the 0.5.x behavior above, contact us using the blue chat bubble in Goodshuffle Pro before you
switch.

## Staying on a specific version

> To be filled in when GSPRO-31872 ships: whether and how a site can stay on one numbered release instead of `/v1/`,
> and how to switch back to `/v1/` later.

Sites that don't switch keep working on 0.5.x. They don't get fixes or new features.

## Checking that you've switched

View your site's page source and search for `loader.js`. If it's there and `unpkg.com/@goodshuffle` isn't, your site
is on the current version.

> To be filled in when GSPRO-32235 ships: how Goodshuffle's support team can confirm which version your site runs.

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
> filled in when GSPRO-31872 ships: the final address, and whether this tag also adds the styles or a stylesheet tag
> goes with it. Until then, this tag loads nothing.

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

Nothing else changes. All of these keep working as they are:

- Your `<gspro-wishlist-config>` tag and its Public Browser Key.
- Every `<gspro-item-gallery>`, `<gspro-item-list>` and `<gspro-item-card>` on your pages, and every attribute on them.
- Your own CSS. The class names it targets, such as `gspro-c-item-card` and `gspro-c-wishlist__venue`, are unchanged.
- Your listeners for every event, with the same `detail`. See [Events]({{< relref "/docs/integrations/events" >}}).
- Links into your catalog, such as `#!/inventory/...` and `#!/item/...`.
- Wishlists your clients already started. They carry over to the new version.

> `gspro-item-card.click`, `gspro-item-card.add`, `gspro-item-detail.add` and the whole item in each
> `detail.wishlist` entry ship with GSPRO-32329.

One detail differs. On 0.5.x, `gspro-wishlist.submit` fired on every click of Send List, even while a send was in
progress. It now fires once per send.

## Staying on a specific version

> To be filled in when GSPRO-31872 ships: whether and how a site can stay on one numbered release instead of `/v1/`,
> and how to switch back to `/v1/` later.

Sites that don't switch keep working on 0.5.x. They don't get fixes or new features.

## Checking that you've switched

View your site's page source and search for `loader.js`. If it's there and `unpkg.com/@goodshuffle` isn't, your site
is on the current version.

> To be decided: how Goodshuffle's support team can confirm which version your site runs.

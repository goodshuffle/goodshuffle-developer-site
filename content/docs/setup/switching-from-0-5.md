---
weight: 80
title: "Switching from 0.5.x"
---

# Switching from 0.5.x

If your site loads the Website Integration from `unpkg.com/@goodshuffle/gspro-wc@0.5...`, you're on version 0.5.x.
Switching to the current version, {{< embed-version >}}, is one change to your site header. On WordPress and Wix the
change is in a different place; see the table below.

## What to change

In your site header, find the two script tags that load `gspro-wc`. They look like this, with your version number in
place of `0.5.7`:

```
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.7/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.5.7/dist/gspro-wc/gspro-wc.js"></script>
```

Replace both with this one tag:

{{< embed-code >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

The new tag adds the release's stylesheet, `gspro-embed.css`, and its script, `gspro-embed.js`, to the page's
`<head>`. You don't add a stylesheet tag. Remove both old tags: the new tag doesn't look for `gspro-wc`, so an old tag
left in place would load a second copy of the Website Integration on the same page.

Leave your `<gspro-wishlist-config>` tag where it is, and save or publish your site.

Where the header lives depends on your site builder:

| Builder | Where to change it |
| --- | --- |
| Squarespace | Code Injection, Header. See [Squarespace]({{< relref "/docs/setup/squarespace" >}}) |
| WordPress | Inside the Goodshuffle plugin. Update the plugin to 0.6.0. You don't edit any tags. See [Updating the plugin]({{< relref "/docs/setup/wordpress#updating-the-plugin" >}}) |
| Wix | No script tags. Change the Server URL on every Goodshuffle Custom Element. See [Wix]({{< relref "/docs/setup/wix" >}}) |
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
- Wishlists your clients already started. The first time the new version loads on your site in a client's browser,
  it moves the wishlist 0.5.x saved in that browser, with its items and dates, into its own storage.

One detail differs. On 0.5.x, `gspro-wishlist.submit` fired on every click of Send List, even while a send was in
progress. It now fires once per send.

## After you switch

The new tag pins version {{< embed-version >}}. Your site stays on it until you change the number in the tag, so a
later release never changes your site by surprise. To move to a newer release, see
[Updating to a newer version]({{< relref "/docs/setup/updating" >}}). To get 1.x updates without editing, see
[Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}).

Sites that don't switch keep working on 0.5.x. They don't get fixes or new features.

## Checking that you've switched

On your published site:

1. Open a page with a gallery. Check that items load and the wishlist button shows.
2. Check the address your site loads:
   - **WordPress**: open the plugin's Advanced Settings. **Your site loads** should show
     `https://embed.goodshuffle.com/releases/1.0.0/loader.js`.
   - **Wix**: open each Goodshuffle Custom Element. Its Server URL should be `{{< embed-url >}}`.
   - **Every other builder**: view the page source and search for `embed.goodshuffle.com`. You should find
     `{{< embed-url >}}`. Then search for `gspro-wc`. If you find it, an old tag is still on the page; remove it.

If you chose [automatic updates]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}), look for
`{{< embed-url alias="v1" >}}` instead.

> To be decided: how Goodshuffle's support team can confirm which version your site runs.

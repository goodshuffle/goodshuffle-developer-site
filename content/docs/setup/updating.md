---
weight: 90
title: "Updating to a newer version"
---

# Updating to a newer version

Every setup snippet on this site pins one release of the Website Integration. The current release is
{{< embed-version >}}, and its script tag is:

{{< embed-code >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

The number in the address is the release. `loader.js` adds two files from that same release folder to the page's
`<head>`: the stylesheet `gspro-embed.css` and the script `gspro-embed.js`. Files in a numbered release folder are
never changed or removed, so your site stays exactly as it is until you change the number.

## Choosing an address

There are three addresses you can load the Website Integration from:

| Address | What your site gets | Choose it if |
| --- | --- | --- |
| A numbered release, such as `{{< embed-url >}}` | That release only. Your site changes when you change the number | You want to check each release before your site gets it. Every setup guide on this site uses this address |
| `{{< embed-url alias="v1" >}}` | The newest 1.x release, automatically. It never moves to 2.x | You want updates without editing your site. This is the right choice for most vendors who want automatic updates. See [Automatic updates with v1](#automatic-updates-with-v1) |
| `{{< embed-url alias="latest" >}}` | The newest release, automatically, including a new major version such as 2.x | You check your site after every release and can change your setup right away when a major version needs it. See [Always the newest release with latest](#always-the-newest-release-with-latest) |

## How to update

1. Check what changed in the new release. See the [Changelog]({{< relref "/docs/resources/changelog" >}}). On
   WordPress, the [WordPress Plugin]({{< relref "/docs/resources/wordpress" >}}) page lists plugin releases.
2. Change the address where your site builder keeps it. See the table below. On most builders, you change the version
   number in the address and nothing else.
3. Save or publish your site. On your published site, check that a gallery shows items, and send a test quote request.

> To be defined: where the release notes for 1.0.0 and later are published. The Changelog page lists releases up to
> 0.5.8.

| Builder | What to change |
| --- | --- |
| Squarespace | The script tag in Code Injection, Header. See [Squarespace]({{< relref "/docs/setup/squarespace" >}}) |
| WordPress | Install the plugin release that loads the version you want. The [WordPress Plugin]({{< relref "/docs/resources/wordpress" >}}) page lists which version each release loads. If Modern JS or Legacy JS in Advanced Settings holds an address, the plugin loads what those fields say, so check **Your site loads** there afterwards. See [Updating the plugin]({{< relref "/docs/setup/wordpress#updating-the-plugin" >}}) |
| Wix | The Server URL on every Goodshuffle Custom Element. See [Wix]({{< relref "/docs/setup/wix" >}}) |
| Showit | The script tag in the Embed Code element in your header canvas. See [Showit]({{< relref "/docs/setup/showit" >}}) |
| GoHighLevel | The script tag in the head tracking code, and in any page's or funnel step's own tracking code. See [GoHighLevel]({{< relref "/docs/setup/gohighlevel" >}}) |
| Lovable | The script tag in `index.html`. See [Lovable]({{< relref "/docs/setup/lovable" >}}) |
| Any other site | The script tag in the page `<head>`. See [Custom Website]({{< relref "/docs/setup/custom-setup" >}}) |

If the address is on your site more than once, change every copy. When a page has two copies, the first one to run
adds its release and the others do nothing. A leftover copy with the old number can keep the old release on that page.

If something goes wrong after updating, put the old number back. The old release stays available at its address.

## Automatic updates with v1

If you'd rather not edit your site for each 1.x release, you can put this address in your script tag in place of the numbered one:

{{< embed-code alias="v1" >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

It's optional. Goodshuffle points `/v1/loader.js` at the current 1.x release, so it adds that release's
`gspro-embed.css` and `gspro-embed.js` from its numbered folder. When Goodshuffle moves it to another 1.x release,
your site follows. The file is cached for up to five minutes, so your site picks up the change within a few minutes,
without an edit. It only ever points at a 1.x release.

Goodshuffle ships breaking changes only as a new major version (2.x), with an upgrade guide. Your site stays on 1.x
until you follow that guide.

The trade-off is that your site changes when a release ships, at a time you don't choose. For most vendors who want
automatic updates, `/v1/` is the address to use.

How to switch depends on your builder:

| Builder | What to change |
| --- | --- |
| WordPress | In Advanced Settings, enter the `/v1/` address in **Modern JS**, leave **Legacy JS** empty, and click **Save Advanced Options**. See [WordPress]({{< relref "/docs/setup/wordpress#automatic-updates-with-v1" >}}) |
| Wix | Set the Server URL of every Goodshuffle Custom Element to the `/v1/` address. Leave no element on a numbered address |
| Every other builder | Replace the address in the script tag with the `/v1/` address, everywhere the tag appears. The table in [How to update](#how-to-update) says where it is |

## Always the newest release with latest

This address always loads the newest release of the Website Integration, whatever its major version:

{{< embed-code alias="latest" >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

Goodshuffle points `/latest/loader.js` at the newest release, so it adds that release's `gspro-embed.css` and
`gspro-embed.js` from its numbered folder. Like `/v1/`, it is cached for up to five minutes, and your site picks up a
new release within a few minutes, without an edit.

> **Warning:** `/latest/` moves to a new major version (2.x, 3.x and later) as soon as Goodshuffle ships it. A new
> major version can include changes that need you to update your setup, such as a renamed attribute or setting. Your
> site loads the new version straight away, before you've made those changes, so parts of your site may stop working
> as before until you follow that version's upgrade guide.

Use `/latest/` only if someone checks your site after every release and can follow an upgrade guide right away. If you
want automatic updates without that risk, use [`/v1/`](#automatic-updates-with-v1). It stays on 1.x.

How to switch depends on your builder:

| Builder | What to change |
| --- | --- |
| WordPress | In Advanced Settings, enter the `/latest/` address in **Modern JS**, leave **Legacy JS** empty, and click **Save Advanced Options**. It works the same way as the `/v1/` address. See [WordPress]({{< relref "/docs/setup/wordpress#always-the-newest-release-with-latest" >}}) |
| Wix | Set the Server URL of every Goodshuffle Custom Element to the `/latest/` address. Leave no element on a numbered or `/v1/` address |
| Every other builder | Replace the address in the script tag with the `/latest/` address, everywhere the tag appears. The table in [How to update](#how-to-update) says where it is |

## Going back to a fixed version

To leave `/v1/` or `/latest/`, put a numbered address back, everywhere the address appears. On WordPress, clear both
Modern JS and Legacy JS and click **Save Advanced Options**. With both empty, the site goes back to the version the
plugin loads by default.

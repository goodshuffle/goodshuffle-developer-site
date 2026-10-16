---
weight: 3
title: "Updating to a newer version"
---

# Updating to a newer version

Every setup snippet on this site pins one release of the Website Integration. The current release is
{{< embed-version >}}, and its script tag is:

{{< embed-code >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

The number in the address is the version. The files at a numbered address never change, so your site stays exactly
as it is until you change that number.

## How to update

1. Check what changed in the new release. See the [Changelog]({{< relref "/docs/resources/changelog" >}}).
2. In your site's script tag, change the version number in the address to the new one. Change nothing else.
3. Save or publish your site, then check a gallery and send a test quote request from your published site.

> To be defined: where the release notes for 1.0.0 and later are published. The Changelog page lists releases up to
> 0.5.8.

Where the tag lives depends on your site builder:

| Builder | What to change |
| --- | --- |
| Squarespace | The script tag in Code Injection, Header. See [Squarespace]({{< relref "/docs/setup/squarespace" >}}) |
| WordPress | Nothing by hand. Update the plugin; each plugin release pins a version. See [WordPress]({{< relref "/docs/setup/wordpress#updating-the-plugin" >}}) |
| Wix | The Server URL on every Goodshuffle Custom Element. See [Wix]({{< relref "/docs/setup/wix" >}}) |
| Showit | The script tag in the Embed Code element in your header canvas. See [Showit]({{< relref "/docs/setup/showit" >}}) |
| GoHighLevel | The script tag in the head tracking code, and in any page's or funnel step's own tracking code. See [GoHighLevel]({{< relref "/docs/setup/gohighlevel" >}}) |
| Lovable | The script tag in `index.html`. See [Lovable]({{< relref "/docs/setup/lovable" >}}) |
| Any other site | The script tag in the page `<head>`. See [Custom Website]({{< relref "/docs/setup/custom-setup" >}}) |

If the tag is on your site more than once, change every copy. When two copies are on one page, only one of them
loads, and it may be the old one.

If something goes wrong after updating, put the old number back. The old release stays available at its address.

## Automatic updates with v1

If you'd rather not edit your site for each fix, you can use this address instead of a numbered one:

{{< embed-code alias="v1" >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

It's optional. `/v1/` serves the newest 1.x release, so your site gets every non-breaking 1.x update
without an edit. A breaking change never ships under `/v1/`: it comes out as a new major version (2.x) with an
upgrade guide, and your site stays on the newest 1.x release until you follow that guide.

The trade-off is that your site changes when a release ships, not when you choose. To go back to a fixed version, put
a numbered address back in the tag.

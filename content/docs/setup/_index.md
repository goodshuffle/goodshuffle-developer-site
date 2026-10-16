---
weight: 5
bookFlatSection: true
title: "Getting Started"
---

# Getting Started

Pick the guide for your site builder:

| Builder | Guide |
| --- | --- |
| Squarespace | [Squarespace Setup]({{< relref "/docs/setup/squarespace" >}}) |
| WordPress | [WordPress Setup]({{< relref "/docs/setup/wordpress" >}}) |
| Wix | [Wix Setup]({{< relref "/docs/setup/wix" >}}) |
| Showit | [Showit Setup]({{< relref "/docs/setup/showit" >}}) |
| GoHighLevel | [GoHighLevel Setup]({{< relref "/docs/setup/gohighlevel" >}}) |
| Lovable | [Lovable Setup]({{< relref "/docs/setup/lovable" >}}) |
| Anything else that lets you edit your page's HTML | [Custom Website Setup]({{< relref "/docs/setup/custom-setup" >}}) |

If your site loads the Website Integration from `unpkg.com`, it's on version 0.5.x. See
[Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}). To move a site that's already set up to a
newer release, see [Updating to a newer version]({{< relref "/docs/setup/updating" >}}).

## How every setup works

Each guide does the same three things in its builder's own way:

1. **Activate the Website Integration** on the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
   in Goodshuffle Pro, and copy your **Public Browser Key**.
2. **Add two tags to your site header**, on every page:

{{< embed-code >}}
<script src="LOADER_URL"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
{{< /embed-code >}}

> The script tag is the only one you need. It adds the release's stylesheet, `gspro-embed.css`, and its script,
> `gspro-embed.js`, to the page's `<head>`, so there's no separate stylesheet tag. It pins version
> {{< embed-version >}}: your site changes only when you change that number. See [Updating to a newer version]({{< relref "/docs/setup/updating" >}}), or
> [Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}) to get 1.x fixes
> without editing.

3. **Put your inventory on a page** with `<gspro-item-gallery>`, `<gspro-item-list>` or `<gspro-item-card>`. See
   [Web Components]({{< relref "/docs/components/item-gallery" >}}).

Replace `YOUR-PUBLIC-WEBSITE-KEY` with your key. Leave the rest of the snippet as shown.

When a client sends their wishlist, it arrives in Goodshuffle Pro as a new project. Find it under Projects, Filters,
Origin = "Website". The sales lead set on the Integrations tab also gets an email.

## When it doesn't work

| What you see | Likely cause |
| --- | --- |
| Nothing at all, not even the wishlist button | The script tag is missing from this page, or was changed when it was pasted |
| The old version still shows after you changed the number | Another copy of the script tag, with the old number, is still on the page. The first copy to run decides which release loads, and the others do nothing. Change every copy |
| The wishlist button shows but no items load | The key is wrong or was regenerated. Copy it again from the Integrations tab |
| Items load on your live site but not in your builder's preview | Inventory loads only on the website address saved for your brand in Goodshuffle Pro, plus a few builder preview addresses. Check your live, published site |
| A gallery shows categories but no items | That's expected until the client picks a category or searches. Give the gallery a `category` to open on one |
| A list shows nothing | A list needs at least one of `category`, `group`, `search` or `tags` |
| An option is on when you set it to `False` | Only lowercase `false` turns an option off |

More answers are in [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

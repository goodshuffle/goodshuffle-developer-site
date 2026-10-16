---
weight: 10
title: Weebly Setup
bookHidden: true
---

# Weebly Setup

## Requirements

You will need...

- A Weebly website
- Your login credentials for the Weebly website
- The ability to copy and paste code-snippets.

## Overview

These are the high-level steps:

1. Activate your Website Integration.
2. Add HTML code snippets to your site's header.
3. Create a page for the basic gallery and embed an HTML code snippet.

## Walk-through

### Activation

If you'd prefer to follow along with a video tutorial, we have one [available here](https://www.youtube.com/watch?v=PGBM8f7CdOQ)!

You can do this from the [Integration Tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Inject in Site Header

#### Add Custom Header Code
1. Go to your Weebly Site Editor
2. Click the button that says "Settings" on the top toolbar
3. Click on the tab marked "SEO" on the left side of the screen
4. Scroll down to the section labelled "Header Code"
5. Paste the following snippet into that box

**PLEASE NOTE! You need to replace the text YOUR-PUBLIC-WEBSITE-KEY below with your Public Browser Key from Goodshuffle Pro (retrieved in the Activation step above).**

{{< embed-code >}}
<script src="LOADER_URL"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
{{< /embed-code >}}

> The script tag adds the styles too; you don't need a stylesheet tag. It pins version {{< embed-version >}}. See
> [Updating to a newer version]({{< relref "/docs/setup/updating" >}}), or
> [Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}) to get 1.x fixes
> without editing.

If your site is on version 0.5.x, replace your two script tags with the one above. See
[Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

No footer code is needed. Older tutorials that mention a footer can be ignored.

### Create a Gallery Page

1. From the top menu, click "Pages"
2. Click the "+" icon next to Pages to create a new page
3. Select Standard Page
4. Give your page a name, such as "Rentals"
5. From the top menu, click "Build"
6. Drag the button that says "Embed Code" into the page section labelled "Drag Elements Here"
7. Click where it says "Click to set custom HTML"
8. Click "Edit Custom HTML" on the popup that appears
9. Paste the following snippet into the box

```
<gspro-item-gallery></gspro-item-gallery>
```

Make sure to publish your changes!

## All Set!

You should now have a gallery page that shows your categories. Items appear once a client picks a category or
searches. To open the gallery on one category, give it a `category`. See
[Item Gallery]({{< relref "/docs/components/item-gallery" >}}).

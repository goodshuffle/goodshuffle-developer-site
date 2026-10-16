---
weight: 20
title: WordPress Setup
---

# WordPress Setup

On WordPress, the Goodshuffle plugin adds the Website Integration to your site for you. You enter your key on its
settings page, and it puts a gallery on the page you choose. Shortcodes add lists and single items anywhere else.

## Requirements

You will need:

- WordPress 5 or later, and an administrator login.
- An active Website Integration on your Goodshuffle Pro account.
- The Goodshuffle Website Integration plugin, version 0.6.0 or later.

> To be filled in when plugin 0.6.0 is released (GSPRO-32532): its download link. Until then, the download on the
> [WordPress Plugin]({{< relref "/docs/resources/wordpress" >}}) page is version 0.5.7, which loads Website Integration
> version 0.5.x.

Plugin 0.6.0 loads Website Integration version 1.0.0, from `https://embed.goodshuffle.com/releases/1.0.0/loader.js`.
You don't paste a script tag: the plugin adds it to every page. Your site moves to a newer Website Integration release
when you install a plugin release that pins a newer one. To get 1.x updates without updating the plugin, see
[Automatic updates with v1](#automatic-updates-with-v1).

## Overview

1. Copy your Public Browser Key from Goodshuffle Pro.
2. Install and activate the plugin.
3. Enter your key and choose your gallery page on the plugin's settings page.
4. Create the gallery page.
5. Send a test quote request.

If your site already has the plugin, update it to 0.6.0. Your settings carry over. See
[Updating the plugin](#updating-the-plugin).

## Walk-through

### 1. Copy your Public Browser Key

In Goodshuffle Pro, open the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
and activate the Website Integration if it isn't active yet. **Copy the Public Browser Key.**

![Integration Tab](/wordpress-website-integration-activation.png)

### 2. Install the plugin

1. Download the plugin `.zip` file. Don't unzip it.
2. In WordPress, go to **Plugins** > **Add New** > **Upload Plugin**.
3. Choose the file and click **Install Now**.
4. Click **Activate Plugin**.

"Goodshuffle Website Integration" now appears in your list of plugins.

### 3. Fill in the settings page

Open the settings page from the **Settings** link under the plugin's name, or from **Settings** > **Goodshuffle**.

1. **Public Browser Key**: paste the key you copied.
2. **Display Gallery on Page**: the slug of the page that will show your gallery. `goodshuffle` is the default and is
   fine for a first test. You can change it later.
3. Tick **Show Categories** and **Show Filters**.
4. Tick **Wishlist** ("Display wishlist on all pages") so the wishlist button shows across your site.
5. Leave the other fields as they are for now.
6. Click **Update Options**.

![Wordpress Settings](/wordpress-settings-screen.png)

The plugin now adds the Website Integration's script tag and your settings to the head of every page on your site.

### 4. Create the gallery page

1. Go to **Pages** > **Add New**.
2. Give the page a title whose slug matches **Display Gallery on Page**, for example "Goodshuffle" for `goodshuffle`.
3. Publish the page.

The plugin puts the gallery above the page's own content. Anything you write on the page shows below the gallery.

![Basic Gallery](/wordpress-basic-gallery.png)

### 5. Send a test quote request

1. Open the gallery page and pick a category.
2. Click the heart on an item to add it to the wishlist.
3. Open the wishlist, choose dates, then **Contact & Venue Info**.
4. Fill in your name and email, then **Send List**.

In Goodshuffle Pro, the request appears as a new project under **Projects**, **Filters**, Origin = "Website".

## Every setting

The settings page has these fields. Each one maps to an attribute on the Website Integration's tags.

| Setting | Default | Same as |
| --- | --- | --- |
| Public Browser Key | Empty | The key in [`data-url`]({{< relref "/docs/components/wishlist-config" >}}) |
| Display Gallery on Page | `goodshuffle` | The page slug that gets the gallery |
| Default Gallery Category | Empty | Gallery `category` |
| Default Gallery Group | Empty | Gallery `group` |
| Default Gallery Search | Empty | Gallery `search` |
| Default Gallery Tags | Empty | Gallery `tags` |
| Default # of Items Listed | `20` | Gallery `size` |
| Scoped Attribute Name | Empty | Gallery `scope-attribute-1-name` |
| Scope Attribute Values | Empty | Gallery `scope-attribute-1-value`. Separate several values with a vertical bar |
| Wishlist Alias | `Wishlist` | `wishlist-alias` |
| Show Categories | Ticked | Gallery `show-categories` |
| Show Filters | Ticked | Gallery `show-filters` |
| Wishlist: Display wishlist on all pages | Not ticked | `wishlist-show-on-all-pages` |
| Scroll Lock: Disable body scroll lock | Not ticked | `disable-body-scroll-lock` |
| Time Selection: Disable time selection | Not ticked | `disable-time-selection` |
| Quantity on Cards | Not ticked | `show-quantity-on-card` |
| Quantity on Detail | Not ticked | `show-quantity-on-detail` |
| Require Phone Numbers | Not ticked | `require-phone-number` |
| Notes Help Text | Empty | `notes-help-text` |

The gallery settings apply to the gallery page only. The wishlist settings apply across your site.

## Advanced Settings

Advanced Settings show below the main settings when you open
`/wp-admin/options-general.php?page=gspro-gallery&advanced=1` on your site. Most sites never change them.

| Field | What it holds |
| --- | --- |
| Data Source | Shows `https://data.goodshuffle.com/vendor` unless someone changed it. Leave it as is |
| Icon URL | Shows the address of the plugin's own `icons.svg` unless someone changed it. The Website Integration doesn't read this setting, so changing it does nothing. To change icons, see [Icons]({{< relref "/docs/customization/icons" >}}) |
| Modern JS | Empty unless you entered an address. The grey placeholder is the plugin's default, `https://embed.goodshuffle.com/releases/1.0.0/loader.js` |
| Legacy JS | Empty unless you entered an address. The plugin's help text says it's "Only for a custom 0.5.x widget build" |
| Your site loads | Read only. Each script address the plugin puts on your pages, exactly as it prints it |

Click **Save Advanced Options** after any change. To put a field back to its default, clear it and save.

### What Modern JS and Legacy JS do

| Modern JS and Legacy JS | Your site loads |
| --- | --- |
| Both empty | `https://embed.goodshuffle.com/releases/1.0.0/loader.js`, the version plugin 0.6.0 pins |
| An address ending in `/loader.js` in either field | That address, in one script tag. The other field is ignored |
| Any other address in either field | The two 0.5.x script tags: Modern JS as `type="module"` and Legacy JS as `nomodule`. An empty field uses the gspro-wc 0.5.7 file |

A few addresses count as an empty field:

- The plugin's own default, `https://embed.goodshuffle.com/releases/1.0.0/loader.js`. If you enter it, the plugin
  doesn't save it, so a later plugin update still moves your site.
- The `unpkg.com` addresses that earlier plugin versions filled in by default. In the plugin's words: "To use one of
  those gspro-wc versions on purpose, enter its jsDelivr address instead."

An `embed.goodshuffle.com` address entered with `http://` is saved and loaded as `https://`.

### Automatic updates with v1

To get non-breaking 1.x updates without updating the plugin:

1. Open Advanced Settings.
2. In **Modern JS**, enter `https://embed.goodshuffle.com/v1/loader.js`.
3. Leave **Legacy JS** empty.
4. Click **Save Advanced Options**.
5. Check that **Your site loads** shows `https://embed.goodshuffle.com/v1/loader.js`.

From then on, plugin updates don't change which version your site loads. To go back to the plugin's pinned version,
clear Modern JS and save. For what `/v1/` does, see
[Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}).

### Staying on one version

To keep a specific release, enter its address in Modern JS, for example
`https://embed.goodshuffle.com/releases/1.0.0/loader.js`. The plugin only saves a version that differs from its own
default. In the help text's words, "entering the current default's address is treated as leaving the field empty". So
to stay on 1.0.0 after a later plugin release moves the default, update the plugin first, then enter the 1.0.0 address.

## Shortcodes

Use these in any page or post. Add them with a **Shortcode** block.

| Shortcode | Shows |
| --- | --- |
| `[gspro-item-list category="decor-rentals"]` | A list of items in a category. Use `category`, `tags`, or both |
| `[gspro-item item-id="9942725a-dcd2-5d33-27b0-44f2ec408d88"]` | A single item card |
| `[gspro-gallery default-category="decor-rentals"]` | The category list next to the first 15 items of that category. No search or paging, and picking a category doesn't change the items |
| `[gspro-wishlist]` | The wishlist. Rarely needed, since the plugin adds it to every page |

For a full gallery with search, filters and paging, use the gallery page from step 4. `[gspro-gallery]` has none of
those.

`[gspro-item-list]` with neither `category` nor `tags` shows nothing. To find a category's value, see
[Item List]({{< relref "/docs/components/item-list" >}}). To find an item's ID, see
[Item Card]({{< relref "/docs/components/item-card" >}}).

Older pages may contain `[gspro-setup]` or `[gspro-item-detail]`. They print nothing, and you can delete them: the
plugin already adds setup and item detail to every page.

## Updating the plugin

1. Download the new version (see Requirements above).
2. Go to **Plugins** > **Add New** > **Upload Plugin**, choose the file and click **Install Now**.
3. When WordPress says the plugin is already installed, click **Replace current with uploaded**. On WordPress versions
   that don't offer this, first deactivate and delete the old plugin in **Plugins**, then upload the new one. Deleting
   the plugin keeps its settings.
4. Open the settings page and check your key is still there.
5. Open Advanced Settings (`/wp-admin/options-general.php?page=gspro-gallery&advanced=1`) and look at **Your site
   loads**.

### What changes when you update to 0.6.0

Every setting carries over. Nothing is renamed or deleted. What your site loads depends on Modern JS and Legacy JS:

- **Never changed.** Your site moves to `https://embed.goodshuffle.com/releases/1.0.0/loader.js`. This includes
  fields that hold the `unpkg.com` address an older plugin filled in. Older plugin versions saved that address
  whenever someone clicked **Save Advanced Options**, and 0.6.0 treats it as empty.
- **An address ending in `/loader.js`.** Your site keeps loading that address.
- **Any other address someone entered**, such as a jsDelivr build. Your site keeps its two 0.5.x script tags. The other
  field, if it's empty or still holds an old plugin default, uses the gspro-wc 0.5.7 file. To move to the new version, clear both fields
  and click **Save Advanced Options**, unless someone set them on purpose.

After updating, **Your site loads** should show `https://embed.goodshuffle.com/releases/1.0.0/loader.js`, or the
`/loader.js` address you chose. If it shows `gspro-wc`, your site is still on 0.5.x.

## Common changes

- **Rename the wishlist**: Wishlist Alias.
- **Require a phone number**: Require Phone Numbers.
- **Hide the venue fields**: in **Appearance** > **Customize** > **Additional CSS**, add
  `.gspro-c-wishlist__venue { display: none !important; }`.
- **Colors and fonts**: see [Colors and Typography]({{< relref "/docs/customization/colors-and-typography" >}}).

## When it doesn't work

- **No gallery on the page.** The page's slug must match Display Gallery on Page exactly.
- **The gallery shows but no items load.** Check the Public Browser Key. If someone regenerated it in Goodshuffle Pro,
  paste the new one and click Update Options.
- **No wishlist button on other pages.** Tick Wishlist ("Display wishlist on all pages").
- **The site still looks like 0.5.x after updating the plugin.** Check **Your site loads** in Advanced Settings. If it
  shows a `gspro-wc` address, Modern JS or Legacy JS holds a custom address. Clear both and save.
- **A shortcode shows as plain text.** Update the plugin. In older versions, `[gspro-item-list]` pointed at
  code that doesn't exist, and WordPress printed the shortcode as text.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

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
- The Goodshuffle Website Integration plugin.

> To be filled in when GSPRO-31872 ships: the version number of the plugin that loads the current Website Integration,
> and its download link. Until that release, the plugin download on the
> [WordPress Plugin]({{< relref "/docs/resources/wordpress" >}}) page is version 0.5.7.

## Overview

1. Copy your Public Browser Key from Goodshuffle Pro.
2. Install and activate the plugin.
3. Enter your key and choose your gallery page on the plugin's settings page.
4. Create the gallery page.
5. Send a test quote request.

If your site already has the plugin, update it to the version above. Your settings carry over. See
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

The plugin now adds the Website Integration to the header of every page on your site.

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

**Advanced Settings** hold Data Source, Icon URL, Modern JS and Legacy JS. They show below the main settings when you
open `/wp-admin/options-general.php?page=gspro-gallery&advanced=1` on your site. Every field shows an address even if
nobody has changed it: when nothing is saved, the field shows the plugin's built-in address. To tell a custom address
from the default, compare each field with this table.

| Field | Built-in address |
| --- | --- |
| Data Source | `https://data.goodshuffle.com/vendor` |
| Icon URL | Your site's address followed by `/wp-content/plugins/gspro-gallery/public/img/icons.svg` |
| Modern JS | To be filled in when GSPRO-31872 ships: the loader address the plugin uses by default |
| Legacy JS | To be filled in when GSPRO-31872 ships: the loader address the plugin uses by default |

A field that matches the table uses the default. To put a field back to its default, clear it and click **Save
Advanced Options**. The plugin deletes the saved address and shows the built-in one again.

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
5. Open Advanced Settings (`/wp-admin/options-general.php?page=gspro-gallery&advanced=1`) and look at **Modern JS** and
   **Legacy JS**.

An address with `@goodshuffle/gspro-wc` in it loads version 0.5.x. Older versions of the plugin show their built-in
0.5.x address in these fields, and clicking **Save Advanced Options** on them saved that address. A saved address
keeps loading, and the site stays on 0.5.x after the update. Clear both fields and click **Save Advanced Options**,
unless someone set them on purpose. Both fields then show the built-in address from the table in
[Every setting](#every-setting).

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
- **A shortcode shows as plain text.** Update the plugin. In older versions, `[gspro-item-list]` pointed at
  code that doesn't exist, and WordPress printed the shortcode as text.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

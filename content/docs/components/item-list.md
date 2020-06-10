---
title: "Item List"
weight: 10
---

# Item List

## Overview

Use the `gspro-item-list` web component to display a list of items on a page.

```
<gspro-item-list search="table | chair" size="20">
</gspro-item-list>
```

You control what is displayed by setting specific attributes on this component.

1. `search` – keyword search on item title and description
2. `tags` – keyword search on item tags
3. `category` – root level category (from Goodshuffle Pro)
4. `group` – sub-categories (from Goodshuffle Pro)

You change the number of items and enable pagination using:

1. `size` – control the number of items to display
2. `route` – used to enable bookmark and sharing friendly pagination.

## Attributes

### search

Use the `search` attribute to get items to find items with a title and
description containing the keywords you specify.

#### Example:

```
<gspro-item-list search="lounge"></gspro-item-list>
```

- Put `-` (minus) in front of a keyword to omit items with that term.
- Put `|` (pipe) in between keywords to include items with either term.
- Use `(a b) | (c -d)` (parenthesis) to group terms together.

#### More Examples:

| What you want...    | What you use... |
| ------------------- | --------------- |
| table AND chair     | `table chair`   |
| table OR chair      | `table | chair` |
| table AND NOT cloth | `table -cloth`  |

#### Q: How do I exclude items?

Answer: Use a minus (e.g. "-cloth") to omit any items containing that keyword.

Example:

```
<gspro-item-list search="table -cloth"></gspro-item-list>
```

#### Q: Are keywords case sensitive?

No. Keyword search is not case sensitive.

#### Q: How do I create a basic search UI?

[Use a `gspro-item-gallery` instead of this web component.]({{< relref "/docs/components/item-gallery" >}})

### `tags`

Use the `tags` attribute to get items using the tags you have added to your items in Goodshuffle Pro. This can help you create collections of items using data that supplements the Goodshuffle Pro taxonomy. This might include:

- seasonality (e.g. fall, winter, spring)
- featured
- event type

_We strongly suggest using tags to supplement the Goodshuffle Pro taxonomy; duplicating it could be very time consuming!_

#### Example:

```
<gspro-item-list tags="wedding"></gspro-item-list>
```

#### Question: are tags case-sensitive?

No.

### `category`

Set this attribute to display items using the Goodshuffle Pro taxonomy for items.

This attribute selects items from a single root category.

#### Example:

```
<gspro-item-list category="decor-rentals">
</gspro-item-list>
```

### `group`

Set this attribute to display items using the Goodshuffle Pro taxonomy for items.

This attribute selects items from a single subcategory.

<gspro-item-list category="decor-rentals">
</gspro-item-list>

### `size`

Use a `size` attribute to control the number of items displayed. By default, a `gspro-item-list` displays fifteen (15) items.

You can display fewer items:

```
<gspro-item-list search="lounge" size="10"></gspro-item-list>
```

...or you can display more items:

```
<gspro-item-list search="lounge" size="50"></gspro-item-list>
```

### `route`

Use the route attribute to enable paginated lists that support bookmarking and sharing.

_Please note: this is an advanced topic. If you intend to show all of your items on a single page, you can safely ignore this._

Use the `route` attribute to enable "paginated" list of items that are sharing and bookmark friendly.

#### Example:

```
<gspro-item-list
  search="posh"
  size="6"
  route="/inventory/:search*"
></gspro-item-list>
```

This will configure the gspro-item-list to read additional properties from a fragment portion of a URL, `from` and `size`, which are used to fetch a "page" of items from Goodshuffle Pro. It will also display links at the bottom of the list for moving to the next and previous page (if they exist).

For example, the `route` in the `<gspro-item-list>` will match the following URL:

https://dz1.goodshuffle.dev/posh/#!/inventory?from=12&size=6

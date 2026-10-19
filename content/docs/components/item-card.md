---
title: "Item Card"
weight: 30
---

# Item Card

## Overview

Use the `gspro-item-card` web component to display a single item. This can be useful for displaying an item inline with other content (e.g. blog posts).

```
<gspro-item-card item-id="9942725a-dcd2-5d33-27b0-44f2ec408d88">
</gspro-item-card>
```

The card shows the item's photo, name and price, and a heart that adds one to the wishlist. Clicking the name opens
item detail. If no item has that ID, or the item isn't shown on your website, the card says "Item Not Found".

## All attributes

| Attribute | Default | What it does |
| --- | --- | --- |
| `item-id` | None | The ID of the item to show |
| `route` | `#!/item/:item` | Accepted so older pages stay valid. It has no effect |
| `item` | None | Set by a gallery or list for the cards it shows. Leave it out |
| `package-quantity` | None | A number the card shows as its quantity, in place of the item's available quantity. Shows only when `show-quantity-on-card` is on in [Wishlist Config]({{< relref "./wishlist-config.md" >}}) |

## Attributes

### `item-id`

Specify the ID of the item you want to display.

#### Q: How do I get the ID of an item?

Open the item in a gallery or list on your site. The page address ends in `#!/item/` followed by the item's ID, then
its name. In `https://example.com/rentals#!/item/9942725a-dcd2-5d33-27b0-44f2ec408d88/Gold-Chiavari-Chair`, the ID is
`9942725a-dcd2-5d33-27b0-44f2ec408d88`.

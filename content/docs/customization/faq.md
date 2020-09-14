---
title: FAQ
weight: 30
---

# FAQ

If you have a question that isn't answered here, ask us in the [blue-chat bubble on https://pro.goodshuffle.com](https://pro.goodshuffle.com).

## How do I hide prices?

You can disable the display of all price related elements using this snippet of CSS:

```
.gspro-o-price {
  display: none !important;
}
```

## How do I hide time selection?

You can disable the display of time selection menus using this snippet of CSS:

```
.gspro-c-item-choices__start-time,
.gspro-c-duration__start-time,
.gspro-c-duration__end-time,
.gspro-o-time-label {
  display: none !important;
}
```

This will disable time selection in the wishlist date picker and item detail overlay. Please note that projects will still have a default time of noon set when a wishlist is submitted.

Jon m.
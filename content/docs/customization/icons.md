---
title: Icons
weight: 30
---

# Icons

You may customize the icon of the item card and the wishlist floating action button. The easiest way to accomplish this is by&hellip;

1. Setting a background image of the `gspro-icon` web component.
1. Hide the built-in SVG.

_Please Note: you should host icon images on a server (or service) you control. Otherwise, changes to it could cause unexpected issues on your website._

## Item Card Add Button

```
/* use an image of your choosing */
gspro-item-card gspro-icon {
  background-image: url("your-url-here");
  background-size: cover;
  background-repeat: no-repeat;
}

/* hide the built-in svg */
gspro-item-card gspro-icon svg {
  display: none;
}
```

## Wishlist Icon

```
/* use an image of your choosing */
gspro-wishlist .gspro-c-wishlist__trigger gspro-icon {
  background-image: url("your-other-url-goes-here");
  background-size: cover;
  background-repeat: no-repeat;
}

/* hide the built-in svg */
gspro-wishlist .gspro-c-wishlist__trigger gspro-icon svg {
  display: none;
}
```

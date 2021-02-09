---
title: Icons
weight: 30
---

# Icons

You may customize the icon of the item card and the wishlist floating action button. The easiest way to accomplish this is by&hellip;

1. Hiding the built-in SVG icons.
1. Setting a background image of the `gspro-icon` web component.

_Please Note: you should host icon images on a server (or service) you control. Otherwise, changes to it could cause unexpected issues on your website._

## Hiding the built-in SVG Icons

Add this to your site's CSS.

``` css
/** Hide the built-in icon **/
.gspro-c-item-card .gspro-c-item-card__add gspro-icon svg,
.gspro-c-wishlist  .gspro-c-wishlist__trigger gspro-icon svg {
  display: none;
}

/** Set the background color of the item card button to white **/
.gspro-c-item-card .gspro-c-item-card__add button {
  background-color: rgba(250,250,250,0.8);
  border: 2px solid rgba(30,30,30,0.8);
}
```

## Set the icon for Item Card Add Button

Upload SVG images to your site and then add this CSS to your site.

_PLEASE NOTE: You will need to change the `background-image` URLs to match the location of the images you have uploaded!_

``` css
/* use an image of your choosing */
.gspro-c-item-card .gspro-c-item-card__add gspro-icon {
  background-image: url("https://your-website-url-here/s/add-no-border-light.svg");
  background-size: contain;
  background-repeat: no-repeat;
}

/* Set the icon for the wishlist floating action button */
.gspro-c-wishlist .gspro-c-wishlist__trigger gspro-icon {
  background-image: url("https://your-website-url-here/s/checklist.svg");
  background-size: cover;
  background-repeat: no-repeat;
}
```

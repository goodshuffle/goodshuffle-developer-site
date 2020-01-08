---
title: Colors & Typography
weight: 10
---

# Colors and Typography

## Overview

Applying your brand colors and typography to webcomponents requires a basic understanding of CSS.

If you're using a website theme created by someone else, it is helpful to understand how web browsers determine which styles are used. You can [learn about CSS specificity from MDN web docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity). In some cases, you may need to adapt our examples to be more "specific" than your website's CSS.

## Item Card Examples

This example provides you with a handful of CSS selectors. Although they focus on colors, you can use these as a starting point to customize a variety of properties. You can easily [experiment with your own customizations](https://jsfiddle.net/goshujomo/j1xd8uos/) by forking this JSFiddle.

```
gspro-item-card {
  background: rgb(250, 250, 250);
}

gspro-item-card:hover {
  background: rgb(255, 255, 255);
}

gspro-item-card .gspro-o-card__title {
  color: #3B3B3B;
}

gspro-item-card .gspro-o-card__subtitle {
  color: #656565;
}

gspro-item-card .gspro-o-card__add button {
  background: #2A2A2A;
}

gspro-item-card .gspro-o-card__add:hover button {
  background: #1A1A1A;
}
```

## Item Detail Examples

```
gspro-item-detail h2.gspro-c-item-details__title {
  color: red;
}
```

## Wishlist Examples

The wishlist has two different states. Initially, it is collapsed, appearing as a floating action button on the bottom-right side of the screen. When clicked, it will enter the expanded state.

This CSS shows you how to apply background and foreground colors in both states. If you use this snippet on your site, you might want to change the hotpink background to something that matches your site's branding.

```
gspro-wishlist[data-mode="collapse"] {
  background: white;
}

gspro-wishlist[data-mode="collapse"] .gspro-c-wishlist__count {
  background: black;
  color: white
}

gspro-wishlist[data-mode="collapse"] use {
  fill: black;
}

gspro-wishlist[data-mode="expand"] {
  background: hotpink;
}
```

## Button Customization

```
button.gspro-o-button {
  background: inherit;
}

button.gspro-o-button:hover {
  background: rgba(255, 255, 255, 0.2);
}

button.gspro-o-button--primary {
  background: #1F1F1F;
}

button.gspro-o-button--primary:hover {
  background: #3F3F3F;
}

button.gspro-o-button--reverse {
  background: white;
  color: hotpink;
}

button.gspro-o-button--reverse:hover {
  background: rgba(255, 255, 255, 0.8);
  color: hotpink;
}

button.gspro-o-button--icon {
  background: inherit;
}

button.gspro-o-button--icon:hover {
  background: rgba(255, 255, 255, 0.2);
}
```

## Using Custom Properties

_Please Note: Although useful, we may elect to change custom property names between minor version updates. We will provide notice of these changes on the Advanced Notice page._

Our webcomponents provide experimental support for CSS custom properties; you can [learn more about custom properties from MDN web docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties).

```
:root {
  --gspro-brand-color: rgba(10, 10, 10, 0.75);
  --gspro-brand-color--hover: rgba(10, 10, 10, 0.75);
  --gspro-font-color--primary: #FF6EB5;
  --gspro-font-color--secondary: #A164E8;
  --gspro-font-family-primary: "Arial";
  --gspro-font-family-secondary: "Courier";
}
```

You can experiment with custom properties by forking this [basic JSFiddle](http://jsfiddle.net/goshujomo/b1uks4n7/).

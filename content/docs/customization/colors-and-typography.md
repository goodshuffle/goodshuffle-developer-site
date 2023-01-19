---
title: Colors & Typography
weight: 10
---

# Colors and Typography

## Overview

Applying your brand colors and typography to web components requires a basic understanding of CSS.

If you're using a website theme created by someone else, it is helpful to understand how web browsers determine which styles are used. You can [learn about CSS specificity from MDN web docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity). In some cases, you may need to adapt our examples to be more "specific" than your website's CSS.

## Naming Conventions

Our web components include classes on most sub-elements to provide you with a concise way to select them an apply your own properties. We prefix all of our class names with `gspro-` to avoid conflicting with other class names from themes and frameworks. Although this makes things a little more verbose, our intention is to work well as many places as possible.

The default styles provided by our web components attempt to be as minimially specific as possible so that the CSS you write is more succinct. The tradeoff is your website's existing CSS may override _our_ default styles; it's possible our examples won't work. So, being familiar with specificity rules is helpful.

## Starting Out

A good way to start customizing your Website Integration theming/branding is by pasting this whole block of CSS inside the appropriate place on your site. Next, use a [color picker](https://www.w3schools.com/colors/colors_picker.asp) to get the perfect colors for your site's look, and replace the placeholder colors with the ones you picked out.

Customizing the Website Integration font is also detailed below, and is a great way to make your integration even more unique.

To learn about adding CSS to your site, the following resources will be of use:
 - [Squarespace](https://support.squarespace.com/hc/en-us/articles/206545567-Using-the-CSS-Editor) 
 - [Wordpress](https://wordpress.com/support/editing-css/)
 - [Showit](https://learn.showit.co/en/articles/905069-blog-formatting-with-css-advanced)

```
/* search button */
.gspro-o-search > .gspro-o-button {
    /* this property changes the background color of the targetted element */
    background: red !important;
    
    /* this property changes the text color of the targetted element */
    color: black !important; 
}

/* filter button */
.gspro-c-item-gallery__toggle-filters  {
    background: green !important;
}

/* category button - mobile only */
.gspro-c-item-gallery__toggle-category {
    background: orange !important;
}

/* card add button color */
gspro-item-card .gspro-o-card__add button {
    background: blue !important;
}

/* card add icon color */
.gspro-c-item-card__add use {
    fill: green !important;
}

/* category text color */
.gspro-o-category {
    color: purple !important; 
}

/* category count badge text color */
.gspro-u-badge {
    color: orange !important;
}

/* wishlist 'cart' count badge*/
gspro-wishlist .gspro-c-wishlist__count {
    background: yellow !important;
    color: purple !important;
}

/* wishlist heart icon color */
gspro-wishlist[data-mode="collapse"] use {
    fill: orange;
}

/* wishlist heart 'cart' background */
.gspro-c-wishlist__trigger {
    background: darkred !important;
}

/* fonts */
:root {
    --gspro-font-family-secondary: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu, Cantarell, Open Sans, Helvetica Neue, sans-serif !important;
    --gspro-font-family-secondary: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu, Cantarell, Open Sans, Helvetica Neue, sans-serif !important;
    --gspro-custom-font-size: 16px;
}
```


## Item Card CSS

This example provides you with a handful of CSS selectors. Although they focus on colors, you can use these as a starting point to customize a variety of properties. You can easily [experiment with your own customizations](https://jsfiddle.net/goshujomo/j1xd8uos/) by forking this JSFiddle.

```
gspro-item-card {
  background: rgb(250, 250, 250);
}

gspro-item-card:hover {
  background: rgb(255, 255, 255);
}

gspro-item-card .gspro-o-card__title {
  color: #1F1F1F;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis
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

## Item Detail CSS

```
gspro-item-detail .gspro-c-item-detail__title {
  color: black;
}

gspro-item-detail .gspro-c-item-detail__price {
  border: 1px solid black;
  color: black;
}
```

## Wishlist CSS

The wishlist has two different states. Initially, it is collapsed, appearing as a floating action button on the bottom-right side of the screen. When clicked, it will enter the expanded state.

This CSS shows you how to apply background and foreground colors in both states. If you use this snippet on your site, you might want to change the "hotpink" background to something that matches your site's branding.

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

## Button CSS

Some web components have button elements. In order to make these look consistent in a variety of web browsers, devices, and operating systems, we define a properties that makes them easy to recognize and select.

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

button.gspro-o-button--warning {
  background: darkorange;
  color: white;
}

button.gspro-o-button--warning:hover {
  background: darkred;
  color: white;
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

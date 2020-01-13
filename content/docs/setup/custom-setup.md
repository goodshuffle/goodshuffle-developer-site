---
weight: 30
bookFlatSection: true
title: "Custom Website Setup"
---

# Setup

**We love a hand-built website!**

Even though you're using the building blocks of our Webcomponent library, we've
tried to make things simple for people just like you.

## Step 1: Add Dependencies

Add the following code into your website `<head>...</head>` element.
It will add our web components library and reference your Goodshuffle Pro inventory.
This is only needed on pages that you intend to display the wishlist or your inventory.

### Required

```
<meta name="gspro-config" content="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY" />
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.2.6/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.2.6/dist/gspro-wc/gspro-wc.js"></script>
```

_Please Note: Your public web site key can be obtained from your Goodshuffle Pro Account Settings._

### Optional

Include this library in the `<head>...</head>` element to mitigate [a common UI issue related to how browsers handle scrolling when a modal item is displayed](https://css-tricks.com/prevent-page-scrolling-when-a-modal-is-open/).

```
<script src="https://unpkg.com/tua-body-scroll-lock"></script>
```

## Step 2: Add Helpers

Add the following code to your website `<body>...</body>` element, prefereably toward the end. It will create:

2. An element used to display item details when an item card is clicked.
1. A floating-action-button that toggles the display of a wishlist.
1. A hidden SVG sprite that is reference by other web components.

```
<div class="gspro-gallery-omni-present">
  <gspro-item-detail
    data-mode="inactive"
    class="gspro-u-fullscreen"
    route="/item/:id/:title*"
  ></gspro-item-detail>
  <gspro-wishlist></gspro-wishlist>
  <gspro-sprite></gspro-sprite>
</div>
```

## Step 3: Test

To test your configuration, add this to a web page:

```
<gspro-item-list search="table | chair"></gspro-item-list>
```

_Please note: you need to an item in your inventory with the word table or chair in order for items to be displayed._

## Troubleshooting

- Are you using a valid public web site key?
- Do you have items in your inventory with the keyword table or chair?
- Is our webcomponent library downloading?

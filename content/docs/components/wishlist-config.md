---
title: "Wishlist Config"
weight: 10
---

# Item List

## Overview

Usage of this element **requires** a Wishlist of version **0.5.0** or greater.

This component is used to change certain settings that affect the Wishlist, or every component of the Wishlist.

Only one of the attributes on this component is required: the `data-url` attribute.

## Usage

Using the `<gspro-wishlist-config>` element is the same as using a `<gspro-item-gallery>`. Certain attributes will be
added inside the tag and will change the corresponding settings. Read more about the options enabled by this component
below.

This element will be placed into your site header during your installation. It should always reside in your site header.

Note that any combination of attributes can be used on one Wishlist config. However, a valid `data-url` is **required**
on every `gspro-wishlist-config`.

## Overriding Sitewide Settings

You can include an additional `gspro-wishlist-config` on specific pages if you want to override a config property you have set for your entire site.

There are two caveats: 
* you **must** include the `data-url` exactly as it appears on your main config element
* you **must* add `disable-body-scroll-lock="true"` on the *page scoped* config element (we do not recommend including this setting on your sitewide config element).

Suppose you have chosen to hide prices sitewide using `hide-prices="true"` on your sitewide config element.
However, you have a page of clearance items where you do want to show prices.
You would include the following snippet in the header of the page where you want to show prices.

```
<gspro-wishlist-config
    hide-prices="false"
    disable-body-scroll-lock="true"
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7">
</gspro-wishlist-config>
```

## Usage Details

### **`data-url`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7">
</gspro-wishlist-config>
```

* This attribute is required to load your Goodshuffle inventory onto your Wishlist.

* Its basic format is `data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"`.

* Note that you will need to replace "YOU-PUBLIC-WEBSITE-KEY" with your unique website key, copied from the Wishlist
  section of the integrations tab in your Goodshuffle Pro account page. It will be a long string of numbers and letters.

### **`disable-body-scroll-lock`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    disable-body-scroll-lock="true">
</gspro-wishlist-config>
```

* The Wishlist comes out of the box with a feature that prevents background scrolling when an item detail component is
  open. This results in a smoother user experience.

* We highly recommend you keep this feature enabled, but you can disable it using this attribute.

* The default value for this attribute is `false`.

### **`disable-time-selection`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    disable-time-selection="true">
</gspro-wishlist-config>
```

* By default, users can select times along with dates on the item-detail popup, as well as during the Wishlist
  submission sequence.

* When enabled, users wil not be able to see those time selection dropdowns or assign a start or end time to their
  Wishlist event.

* The default value for this attribute is `false`.

### **`hide-prices`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    hide-prices="true">
</gspro-wishlist-config>
```

* This will hide all prices on item cards and item details, as well as prevent any rate type selection.

* The default value for this attribute is `false`.

### **`notes-help-text`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    notes-help-text="Tell us how you heard about us!">
</gspro-wishlist-config>
```

* This element lets you add italicized help text under the "Notes" field on the Send Wishlist panel.

* The length of this help text is **hard capped at 140 characters**. 

* By default, there will be no text under the Notes field.

### **`require-phone-number`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    require-phone-number="true">
</gspro-wishlist-config>
```

* This element will require site visitors to submit a phone number on Wishlist checkout.

* The default value for this attribute is `false`.

### **`show-quantity-on-card`/`show-quantity-on-detail`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    show-quantity-on-card="true"
    show-quantity-on-detail="true">
</gspro-wishlist-config>
```

* These elements will show quantity on their respective components. They can be used independently of each other.

* The default value for these attributes is `false`.

### **`wishlist-alias`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    wishlist-alias="Your Cart">
</gspro-wishlist-config>
```

* This attribute determines the label for the Wishlist "cart" that site visitors will see when submitting information to
  generate a quote.

* The default value for this attribute is `Wishlist`.

### **`wishlist-show-on-all-pages`**

```
<gspro-wishlist-config 
    data-url="data-url="https://data.goodshuffle.com/vendor/a1b2c3d4e5f6g7"
    wishlist-show-on-all-pages="false">
</gspro-wishlist-config>
```

* The Wishlist heart icon will **always** show on any page where you have a `<gspro-item-list>`,
  a `<gspro-item-gallery>`, or a `<gspro-item-card>`.

* This attribute determines whether the Wishlist heart icon, representing the "cart", will show on every page of your
  website that does not contain one of the components mentioned in the previous step.

* The default value for this attribute is `true`. You only need to include this attribute if you wish to disable the
  Wishlist appearing on all pages.

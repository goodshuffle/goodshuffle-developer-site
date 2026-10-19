---
title: "Wishlist Config"
weight: 10
---

# Wishlist Config

## Overview

`<gspro-wishlist-config>` connects your site to your Goodshuffle Pro inventory and holds the settings that apply to
every part of the Website Integration. It goes in your site header, once, right after the script tag.

It shows nothing on the page itself. When it loads, it adds the wishlist and the item detail popup to the page for you.

Only `data-url` is required. Add any of the other attributes to the same element:

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    require-phone-number="true"
    show-quantity-on-card="true"
    disable-time-selection="true">
</gspro-wishlist-config>
```

The element reads its attributes once, when the page loads. Changing them later with JavaScript has no effect.

Currency, country, and the date, address and phone formats come from your Goodshuffle Pro account.

Language works differently. The widget shows English unless Goodshuffle has turned on multiple languages for your
Goodshuffle Pro account. No attribute on this tag changes it. To turn it on, ask Goodshuffle. With
them on, clients get a language selector with English, Spanish and French.
The widget uses the language the client picks there. Before they pick one, it uses the browser's language if that's
Spanish or French, and English otherwise.

## All attributes

| Attribute | Default | What it does |
| --- | --- | --- |
| `data-url` | None. Required | Your data address, ending in your Public Browser Key |
| `disable-body-scroll-lock` | `false` | `true` lets the page behind item detail scroll |
| `disable-time-selection` | `false` | `true` hides the time pickers. Clients pick dates only |
| `notes-help-text` | Empty | Help text under the Notes field, up to 140 characters |
| `require-phone-number` | `false` | `true` makes the phone number required |
| `show-quantity-on-card` | `false` | `true` shows available quantity on item cards |
| `show-quantity-on-detail` | `false` | `true` shows available quantity in item detail |
| `wishlist-alias` | `Wishlist` | The name clients see for the wishlist |
| `wishlist-show-on-all-pages` | `true` | `false` shows the wishlist button only on pages with a gallery, list or item card |

**How on/off attributes read.** Only the lowercase word `false` turns an attribute off. The attribute with no value,
or with any other value (`true`, `True`, `yes`, and also `False`), turns it on. To keep an option at its default,
leave the attribute out.

## Usage Details

### **`data-url`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY">
</gspro-wishlist-config>
```

* Required. Without it, no inventory loads.
* Replace `YOUR-PUBLIC-WEBSITE-KEY` with the Public Browser Key from the Integrations tab of your Goodshuffle Pro
  account. It is a long string of letters and numbers.
* If you regenerate the key in Goodshuffle Pro, the old one stops working at once. Put the new key in this attribute
  right away.
* Older sites may set this address with `<meta name="gspro-config" content="...">` instead. That still works. When
  both are present, the attribute wins.

### **`disable-body-scroll-lock`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    disable-body-scroll-lock="true">
</gspro-wishlist-config>
```

* While item detail is open, the page behind it doesn't scroll. That makes the popup easier to use, and we recommend
  keeping it.
* Set this to `true` to turn the lock off.

### **`disable-time-selection`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    disable-time-selection="true">
</gspro-wishlist-config>
```

* By default, clients pick times along with dates in item detail and in the wishlist.
* Set this to `true` and clients pick dates only.

### **`notes-help-text`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    notes-help-text="Tell us how you heard about us!">
</gspro-wishlist-config>
```

* Adds help text under the Notes field on the form clients fill in to send their wishlist.
* Anything past 140 characters is cut off.
* The text shows exactly as you wrote it, whatever language the client picks.

### **`require-phone-number`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    require-phone-number="true">
</gspro-wishlist-config>
```

* Clients must enter a phone number to send their wishlist.

### **`show-quantity-on-card`** and **`show-quantity-on-detail`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    show-quantity-on-card="true"
    show-quantity-on-detail="true">
</gspro-wishlist-config>
```

* Show available quantity on item cards, in item detail, or both. Each works on its own.
* An item whose quantity isn't tracked shows "Contact us for availability".

### **`wishlist-alias`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    wishlist-alias="Your Cart">
</gspro-wishlist-config>
```

* The name clients see for the wishlist, for example "Your Cart" or "Quote Request".
* It shows exactly as you wrote it, whatever language the client picks.

### **`wishlist-show-on-all-pages`**

```
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
    wishlist-show-on-all-pages="false">
</gspro-wishlist-config>
```

* The wishlist button always shows on pages with a `<gspro-item-gallery>`, `<gspro-item-list>` or `<gspro-item-card>`.
* By default it also shows on every other page of your site. Set this to `false` to show it only on those pages.
* The default is `true`.

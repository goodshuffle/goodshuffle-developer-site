---
title: "Listeners"
weight: 30
---

# Listeners

Use of this functionality **requires** a Wishlist version of **0.5.3** or greater.

You are able to dynamically update the content of a `gspro-item-list` or `gspro-item-gallery` by using Javascript.
This extends the functionality of the Wishlist's inherent category, search, and attribute selection and provides the opportunity to build more complicated user interfaces on your site, or allow your clients to choose between a smaller subset of options than provided by the standard gallery.

Usage of this functionality requires knowledge of Javascript, and the ability to add custom Javascript to your website.

The following properties of `gspro-item-list` and `gspro-item-gallery` can be dynamically updated:
`search, tags, category, group, item-attribute-1-name, item-attribute-1-value, item-attribute-2-name, and item-attribute-2-value`.

This is done by using Javascript to get the list or gallery element you want to update, then updating the specific attribute you want to change.
An example of toggling the Color attribute in an item list using a `<select>` dropdown. Note the `onchange` handler in the select statement is the same as the function defined in the Javascript.
It is also worth noting how the `updateColor` function retrieves the element from the page and calls `setAttribute`. This same pattern could be followed to update any of the 

*HTML* 
```
<select onchange="updateColor(event.target.value)">
  <option value="Black">Black</option>
  <option value="White">White</option>
  <option value="White">Red</option>
  <option value="White">Green</option>
  <option value="White">Blue</option>
</select>ym

<gspro-item-list category="furniture-rentals"
item-attribute-1-name="Color"
item-attribute-1-value="Black"></gspro-item-list>
```

*Javscript*
```
  function updateColor(newColor) {
    document.getElementsByTagName("gspro-item-list")[0]
    .setAttribute("item-attribute-1-value", newColor)
  }
```

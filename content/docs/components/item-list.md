---
title: "Item List"
weight: 10
---

# Item List

## Overview

An Item List is used to display inventory when you do not want a search bar. If you want the search bar, read the directions for an [Item Gallery]({{< relref "/docs/components/item-gallery" >}}).

[See an example item list here!](https://dz8.goodshuffle.dev/list)

A code snippet example for a basic Item List with the most popular way to pull inventory (via tags):

```
<gspro-item-list tags="Rustic"></gspro-item-list>
```

Another example showing pulling inventory via category:

```
<gspro-item-list category="tent-canopy-rentals"></gspro-item-list>
```

The minimum requirement for displaying inventory on an item list is **at least one of** `category`, `search`, `tags`, or `group`. 

Additionally, multiple options can be provided to further narrow down the inventory displayed in the list:

```
<gspro-item-list
    group="seating-chair-rentals"
    tags="Rustic"
    item-attribute-1-name="Color"
    item-attribute-1-value="Red | White | Blue">
</gspro-item-list>
```

*This list will display seating and chair rentals, tagged with the 'Rustic' tag, with either a Red, White or Blue 'Color' attribute. Tags and attributes can be set in your [Goodshuffle Pro Inventory tab](https://pro.goodshuffle.com/inventory/index)*

## Usage

You determine the items displayed in a gallery by changing the following controls on the `<gspro-item-list>` component. 

Click the control name to go to usage details.

* [`search`]({{< relref "#search" >}}) – keyword search on item title and description 
* [`tags`]({{< relref "#tags" >}}) – keyword search on item tags
* [`category`]({{< relref "#category" >}}) – root level category (from Goodshuffle Pro)
* [`group`]({{< relref "#group" >}}) – sub-categories (from Goodshuffle Pro)
* [`item-attribute-#`]({{< relref "#item-attribute-" >}}) - filter based on attributes (Color, Shape, Location, etc.)

You change the number of items and enable pagination using:
* [`size`]({{< relref "#size" >}}) – control the number of items that will appear in the list. Defaults to 15 items
* [`route`]({{< relref "#route" >}}) – used to enable bookmark and sharing friendly pagination.

## Usage Details

### **`search`**
```
<gspro-item-list search="lounge"></gspro-item-list>
```

Use the `search` attribute to find items with a title and description containing the keywords you specify.

It’s possible to specify part of an identifier or multiple, by using the keys below.

- Put `-` (minus) in front of a keyword to omit items with that term.
- Put `|` (pipe) in between keywords to include items with either term.
- Use `(a b) | (c -d)` (parenthesis) to group terms together.

#### More Examples:

| What you want...    | What you use... |
| ------------------- | --------------- |
| table AND chair     | `table chair`   |
| table OR chair      | `table | chair` |
| table AND NOT cloth | `table -cloth`  |

#### Q: How do I exclude items?

Answer: Use a minus (e.g. "-cloth") to omit any items containing that keyword.

Example:

```
<gspro-item-list search="table -cloth"></gspro-item-list>
```

#### Q: Are keywords case sensitive?

No. Keyword search is not case sensitive.

#### Q: How do I create a basic search UI?

[Use a `gspro-item-gallery` instead of this web component.]({{< relref "/docs/components/item-gallery" >}})

### **`tags`**
_Note: We strongly suggest using tags to **supplement** the Goodshuffle Pro taxonomy; duplicating it could be very time consuming!_
```
<gspro-item-list tags="wedding"></gspro-item-list>
```

Use the `tags` attribute to get items using the tags you have added to your items in Goodshuffle Pro. This can help you create collections of items using data that supplements the Goodshuffle Pro taxonomy. This might include:

- seasonality (e.g. fall, winter, spring)
- featured
- event type

#### Question: are tags case-sensitive?

No.

#### Question: how do I add multi-word tags a.k.a. tags with spaces in between words?

Wrap them in a single quote `'`.

E.g. `<gspro-item-list tags="'Graduation Party'"></gspro-item-list>`

### **`category`**
```
<gspro-item-list category="decor-rentals">
</gspro-item-list>
```

Set this attribute to display items using the Goodshuffle Pro categorization for items.

This attribute selects items from a single root category.

**Q: How can I find my item categories?**

The easiest way to get the desired categories is to temporarily [add an item gallery]({{< relref "/docs/components/item-gallery" >}}) to your page. Make sure `show-categories` is enabled and there are no other modifications, like so:

`<gspro-item-gallery show-categories="true"></gspro-item-gallery>`.

You can remove this gallery from your page when you are done gathering categories.

Click the name of the category you want to add on the left hand side of the screen.

![Get Category String](/select-category.png)

You will notice that the url of the page has changed based on the category you have selected. This is the value you will include in `category` tag in your item list.

![Category String in URL](/category-url.png)

In this case, the value of the category would be "entertainment-games-rentals", e.g.

```
<gspro-item-list category="entertainment-games-rentals">
</gspro-item-list>
```

For a video tutorial on getting the category of an item, please [see here](https://www.youtube.com/watch?v=drWHmwRsyxw&feature=youtu.be&t=144).

### **`group`**
```
<gspro-item-list group="cable-cord-power-rentals">
</gspro-item-list>
```

Set this attribute to display items using the Goodshuffle Pro sub-categorization for items.

This attribute selects items from a single subcategory.

Groups operate in a very similar way to categories. You can find the value for a specific group by following the steps above for category, but instead clicking on the desired sub category.

![Group String in URL](/group-url.png)

### **`item-attribute-#`**

```
<gspro-item-list
  category="linen-rentals"
  item-attribute-1-name="Warehouse Location"
  item-attribute-1-value="Washington, DC"
  item-attribute-2-name="Color"
  item-attribute-2-value="Red | Blush"
  item-attribute-3-name="Fabric"
  item-attribute-3-value="Cotton"
></gspro-item-list>
```

Up to three custom attributes can be used to filter your `gspro-item-list`.

The `item-attribute-#` filter **MUST** be used with category, search, group, and/or tags

Note: The item attribute `name` and `value` **must match exactly** what is provided in your Goodshuffle Pro inventory, including **case sensitivity** and any special characters.

The `name` and `value` of an item attribute correspond to the number provided in between the dashes. You must have both of these parts for item attribute filtering to work properly.

**Q: Can I add multiple `item-attribute-#-value` for one `item-attribute-#-name`?**

Yes, you can filter for many item attribute values using the pipe `|` symbol. `item-attribute-#-value` using the pipe will include items with **either** item attribute value.

For example, the item list shown above will have items that are red **and** items that are black.

**Q: How can I find the attributes for items in my inventory?**

You can find the attributes for an item by clicking the item in your Goodshuffle Pro inventory and looking under Specs. All lines that are not Primary Category or Sub Category are considered attributes (see below).

You can learn more about adding attributes [here](https://help.goodshuffle.com/en/articles/2114066-attributes-what-they-are-how-to-use-them).

![Category String in URL](/attribute-location.png)

To create an item list that filters based on the height attribute in the above image, the component would look like this:
```
<gspro-item-list 
  category="furniture-rentals"
  item-attribute-1-name="Height"
  item-attribute-1-value="2 ft."
></gspro-item-list>
```

You can use any attribute assigned to items in your Goodshuffle Pro, even custom ones you've created yourself. 

#### **`sort-primary`** 

You can sort any `gspro-item-list` that has an `item-attribute-#-name` and an `item-attribute-#-value` with **at least two values separated by a pipe**. This is done by using the `sort-primary` flag, and passing in the `item-attribute-#` you wish to sort by.

**Example**
```
<gspro-item-list
  category="linen-rentals"
  item-attribute-1-name="Color"
  item-attribute-1-value="Red | Blush | Black"
  item-attribute-2-name="Fabric"
  item-attribute-2-value="Cotton | Polyester"
  sort-primary="item-attribute-1"
></gspro-item-list>
```

In this example, we would get a list of all linen rentals that are Red, Blush, or Black and either Fabric or Polyester. We would see all the Red Linens, then all Blush linens, then all Black linens. 

If you wanted to have all Cotton linens, then all Polyester Linens, simply change `sort-primary="item-attribute-1"` to `sort-primary="item-attribute-2"`. 

The sort flags do not have any impact on which items appear in the item list. They will only affect the order in which those items appear. 

#### **`sort-primary-order`**

You can also sort from right to left by adding the `sort-primary-order="desc"` flag.

### **`size`**

Use a `size` attribute to control the number of items displayed. By default, a `gspro-item-list` displays **fifteen (15)** items.

You can display fewer items:

``` 
<gspro-item-list search="lounge" size="10"></gspro-item-list>
```

...or you can display more items:

``` 
<gspro-item-list search="lounge" size="50"></gspro-item-list>
```

### **`route`**

Use the route attribute to enable paginated lists that support bookmarking and sharing.

_Please note: this is an advanced topic. If you intend to show all of your items on a single page, you can safely ignore this._

Use the `route` attribute to enable "paginated" list of items that are sharing and bookmark friendly.

#### Example:

```
<gspro-item-list
  search="posh"
  size="6"
  route="/inventory/:search*"
></gspro-item-list>
```

This will configure the gspro-item-list to read additional properties from a fragment portion of a URL, `from` and `size`, which are used to fetch a "page" of items from Goodshuffle Pro. It will also display links at the bottom of the list for moving to the next and previous page (if they exist).

For example, the `route` in the `<gspro-item-list>` will match the following URL:

https://dz1.goodshuffle.dev/posh/#!/inventory?from=12&size=6

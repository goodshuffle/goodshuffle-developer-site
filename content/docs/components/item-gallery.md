---
title: "Item Gallery"
weight: 20
---

# Item Gallery

## Overview

Use the `gspro-item-gallery` web component to display a list of items with controls for searching, browsing categories, and filtering items. If you don't need any of these controls, consider using an `gspro-item list` instead. It's worth noting, that this web component provides a superset of attributes provided by `gspro-item-list`. It may help to [learn more about how to use a `gspro-item-list`]({{< relref "./item-list.md" >}}) because the item-list has a subset of item-gallery attributes.

[See an example gallery here!](https://dz8.goodshuffle.dev/gallery)

## Parts of a Gallery

### Search

A text input field with a search button is provided for your site visitors to enter keywords. This must match an item's title and description. Additional fields are also searched (e.g. tags and category) but this may be removed in the future, so please don't rely on it!

### Filters

Filters are populated using the custom attributes you've assigned to items in Goodshuffle Pro. If you don't want an attribute to be displayed, set the attribute to Internal Only in Goodshuffle Pro. Please note: there is a hard limit of 100 choices per group.

You can disable filters entirely by setting the `show-filters` attribute like this:

```
<gspro-item-gallery show-filters="false"></gspro-item-gallery>
```

### Categories

Categories and subcategories are retrieved from Goodshuffle Pro. If you do not want to display a category or the items it contains, you can disable those items in Goodshuffle Pro.

You can also disable categories entirely by setting the `show-categories` attribute like this:

```
<gspro-item-gallery show-categories="false"></gspro-item-gallery>
```

### Customizing Listed Inventory

The gallery displays a list of items that match your initial configuration of the list. As visitors perform searches, choose categories or subcategories, or make filter choices, the item list will be updated.

## Limiting Items Displayed in a Gallery (using Scope)

You can specify the "scope" of items displayed within a gallery by using the following attributes:

- `scope-category`
- `scope-group`
- `scope-tags`
- `scope-search`

Each of these attributes works will constrain the set of items to be displayed. This is useful for creating a page for a set of items (like linens) and providing visitors with a way to filter or search them. For example:

```
<gspro-item-gallery scope-category="linen-rentals"></gspro-item-gallery>
```

Here's another example that limits items to ones with the tags "featured" and "summer" on them.

```
<gspro-item-gallery scope-tags="featured summer"></gspro-item-gallery>
```

## Attributes

### **`category`**

The default category of items to display. Will be overriden by searching or picking a category.

### **`group`**

Note: When using the group flag for a `<gspro-item-gallery>`, you **MUST** also have the appropriate parent category. 
Not doing so will interfere with the filtering of the component. 

The default subcategory of items to display. Will be overriden by searching or picking a category.

### **`tags`**

Display a list of items with the tag(s). Will be overriden by searching, filtering or picking a category.

[Learn more about how to use tags]({{< relref "./item-list.md#tags" >}}).

### **`search`**

Display a list of items with the specified keywords by default. Will be overriden by searching or picking a category.

[Learn more about how to use keywords]({{< relref "./item-list.md#search" >}}).


### **`scope-category`**

Limit the displayed items to a root-level category in Goodshuffle Pro. Supports multiple categories separated by spaces.

### **`scope-group`**

Limit the displayed items to a subcategory in Goodshuffle Pro. Supports multiple subcategories separated by spaces.

### **`scope-search`**

Limit the displayed items to ones that match the given keywords.

[Learn more about how to use keywords]({{< relref "./item-list.md#search" >}}).

### **`scope-tags`**

Limit the displayed items to ones with the given tags.

[Learn more about how to use tags]({{< relref "./item-list.md#tags" >}}).

### **`scope-attribute-#-name / scope-attribute-#-value`**
**`added in v0.5.2`**

Limit the displayed items to ones with the given attributes.

Example:
```
<gspro-item-gallery
    scope-attribute-1-name="Warehouse Location"
    scope-attribute-1-value="Washington, DC"
></gspro-item-gallery>
```

[Learn more about attributes]({{< relref "./item-list.md#item-attribute-" >}}).

### **`sort`**
**`added in v0.5.2`**

**Usage of at least one `scope-attribute-#` with piped `scope-attribute-#-value` values is required to use sort.** 

```
<gspro-item-gallery
    scope-attribute-1-name="Warehouse Location"
    scope-attribute-1-value="Washington, DC | Rosslyn, VA"
    sort-primary="scope-attribute-1"
></gspro-item-gallery>
```

We would then see all the items in the Washington warehouse, then all the items in the Rosslyn warehouse.

[Learn more about sort]({{< relref "./item-list.md#sort-primary" >}}).

### **`show-categories`**

Set to false to hide the category element and button to toggle it. Default to true.

### **`show-filters`**

Set to false to hide the filter element and button to toggle it. Default to true.

### **`size`**

Limit the number of displayed items. Defaults to 15 items.

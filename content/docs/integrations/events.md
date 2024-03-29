---
title: "Events"
weight: 30
---

# Events

Using event emitters requires Website Integration version 0.4.3 or later.

Goodshuffle Website Integration leverages [HTML DOM events](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Events)
to allow you to integrate a wide variety of services into your Website Integration components.

Capturing Website Integration events requires a basic knowledge of Javascript, and the ability to add custom Javascript to your website.

The most common use case for Website Integration events is reporting to Google Analytics. Other common use cases are displaying custom dialogs/modals or integrating with an ad service provider.

Website Integration events come with relevant data to empower your custom logic, add specificity to your analytics, and personalize your custom messages.
This data is accessed with `data.detail` for every event. The specific structure of the `data.detail` payload is detailed below for each event.

Note: some examples below demonstrate reporting to Google Analytics. To report event data from your Website Integration to Google Analytics requires [setting up Google Analytics first](https://developers.google.com/analytics/devguides/collection/analyticsjs).

## Event Types

### Item Card Click

This event occurs when the user clicks on a `<gspro-item-card>` inside of a `<gspro-item-list>` or `<gspro-item-gallery>`.
This event is attached to the opening the modal with the detail view of the item, with a larger image and information about the item.
Common reasons for targetting this event would be using analytics to determine which items are popular, or for tracking how many items a user clicks on before adding an item to their wishlist.

To capture this event, you will use the [`document.addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) Javascript method. The event to target for these `<gspro-item-card>` click events is `gspro-item-card.click`.

Example (with Google Analytics):
```
document.addEventListener("gspro-item-card.click", function(data) {
    // get the item title from the event payload
    var itemName = data.detail.title;
    // report the event to Google Analytics
    gtag('event', 'Click', {
        'event_category': 'Goodshuffle Website Integration',
        'event_label': 'Item Card Click',
        'value': itemName
    });
})
```

In this example, an event listener is being attached to the item card click. When the user clicks to expand an item card, the analytics category (Goodshuffle Website Integration), event label (Item Card Click), and data (the clicked item's name) are all being reported to Google Analytics.

`data.detail` object for `gspro-item-card.click`:
```
{
    attributes: // An array of objects representing the item's attributes
    category: // An object representing the category the item is assigned to
    description: // the item's description
    groups: // An array of objects representing the sub category of the item
    id: // The item's unique ID in your Goodshuffle inventory
    images: // An array of objects representing the images attached to this item
    inventoryType: // The type of item
    price:  // Pricing information about the item
    quantity: // An object representing the amount of the item in your inventory
    rate: // The default payment structure for this item
    related: // Other inventory items flagged as related to the clicked item
    tags: // The tags for the item
    title: // The name of the item that was clicked
    vendorName: // Your business name
    wanted: // the amount of inventory item the user has added to the wishlist
}
```

### Add to Wishlist

This event occurs when the user clicks the "Add to Wishlist" icon (represented by a heart) on a `<gspro-item-card>` inside.
The user can also add items to their wishlist from inside the expanded item detail view and clicks the "Send to Wishlist" button.
These are distinct events from a Website Integration perspective, but correspond to the same event for tracking purposes.

The two events that correspond to adding to wishlist are `gspro-item-card.add` and `gspro-item-detail.add`.
You will want to capture **BOTH** of these events when targetting the "Add to Wishlist" functionality.
Because you will need to capture both events, we recommend putting your handler logic inside its own function.
This will help you ensure that the same logic is being executed by both handlers.

Example (with alert):
```
// define your handler function (in this case presenting an alert)
function handleEvent(data) {
    alert("You have added " + data.detail.want + " quantity of " + data.detail.title + " to your Wishlist!")
}

// add listener for adding to wishlist with "heart icon"
document.addEventListener("gspro-item-card.add", function(data) {
    handleEvent(data)
})

// add listener for adding to wishlist from expanded item detail view
document.addEventListener("gspro-item-detail.add", function(data) {
    handleEvent(data)
})

```

The `data.detail` object of this event is the exact same as the one detailed in the Item Card Click section. You have access to all the same data that you do for the "gspro-item-card.click" event.

### Submit Wishlist

This event occurs when a user submits a wishlist request after filling in their venue and contact information.
You can capture this event by targeting the `gspro-wishlist.submit` event. 

This event happens *immediately* after the submit button is clicked. 
It should not be used for any functionality that might block completion of the request, such as a redirect. 
The 'Submission Complete' event detailed below is fired when the API call to submit the Wishlist completes successfully, and should be used for redirects.

Example (with Google Analytics):
```
// add listener for wishlist submit event
document.addEventListener("gspro-wishlist.submit", function(data) {
    // get our data from the detail object
    var wishlistCount = data.detail.wishlist.length
    var clientFullName = data.detail.contact.firstName + " " + data.detail.contact.lastName
    // construct a message
    var message = clientFullName + " submitted a wishlist with " + wishlistCount + " items."
    // send to Google Analytics
    gtag('event', 'Submission', {
        'event_category': 'Wishlist',
        'event_label': 'Wishlist Submission',
        'value': message
    });
})
```

`data.detail` object for `gspro-wishlist.submit`
```
contact:  // information about the person filling out the Wishlist
venue:    // venue information provided by person submitting the Wishlist
wishlist: // array of objects representing the "cart" of the Wishlist
          // each item is identical to the item detail described above
```

`data.detail.contact` object - provided by user before submission
```
{
    firstName: "John"
    lastName: "Doe"
    email: "john.doe@gmail.com"
    phone: "5555551234"
}
```

`data.details.venue` object - provided by user before submission
```
{
    addressStreet1: "123 Green St"
    addressStreet2: "Suite 101"
    city: "Washington"
    postalCode: "20032"
    state: "DC"
    venueName: "The Place to Be"
}
```

### Submit Complete

Usage of this event **requires** a Website Integration version of **0.5.1** or greater.

This event happens when the API responds successfully, indicating that the wishlist has been received and processed.
You might use this event to redirect to a thank-you page, or open a modal instructing your users on what to expect next.

You can capture this event by targeting the `gspro-wishlist.submit-complete` event.

This event uses the exact same `data.detail` modelling as the 'Submission Complete' event described above.

Example (with a redirect to personalized thank-you page):
```
  document.addEventListener("gspro-wishlist.submit-complete", function (data) {
    var clientFullName = data.detail.contact.firstName + " " + data.detail.contact.lastName;
    location = "https://eventrentals.com/?name=" + clientFullName
  })
```

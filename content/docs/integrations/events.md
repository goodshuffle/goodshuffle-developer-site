---
title: "Events"
weight: 30
---

# Events

The Website Integration tells your page when a client opens an item, adds one to the wishlist, sends their
wishlist, or submits a lead form. It does this with standard
[DOM events](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Events). Any script on your
page can react: report the activity to your analytics, show your own thank-you message, or send the client to a
thank-you page.

Listening for events takes basic JavaScript and a way to add your own script to your site.

| Event | When it fires |
| --- | --- |
| `gspro-item-card.click` | The client clicked an item card to open the item |
| `gspro-item-card.add` | The client clicked the heart on an item card |
| `gspro-item-detail.add` | The client added the item to the wishlist from the item's detail view |
| `gspro-wishlist.submit` | The client clicked Send List and the wishlist is on its way |
| `gspro-wishlist.submit-complete` | Goodshuffle Pro accepted the quote request |
| `gspro-lead-form.submit` | The client submitted a [lead form]({{< relref "/docs/components/lead-form" >}}) and the answers are on their way |
| `gspro-lead-form.submit-complete` | Goodshuffle Pro saved the lead form's response |

> The three item events and the full wishlist entries described here ship with GSPRO-32329. They match version 0.5.x.

Every event bubbles up to `document`. Listen there:

```
document.addEventListener("gspro-wishlist.submit-complete", function (event) {
    console.log(event.detail);
});
```

## Item opened: `gspro-item-card.click`

Fires when the client clicks an item card in a gallery or list, just before the item's detail view opens. Use it to
see which items clients look at.

`event.detail` is the item. See [The item](#the-item) below.

Example (with Google Analytics):

```
document.addEventListener("gspro-item-card.click", function (event) {
    gtag("event", "Click", {
        "event_category": "Goodshuffle Website Integration",
        "event_label": "Item Card Click",
        "value": event.detail.title
    });
});
```

## Item added: `gspro-item-card.add` and `gspro-item-detail.add`

A client can add an item to the wishlist in two places, and each fires its own event:

- `gspro-item-card.add` fires when the client clicks the heart on an item card. `event.detail` is the item, with
  `want` set to `1`.
- `gspro-item-detail.add` fires when the client adds the item from its detail view. `event.detail` is the item, with
  the quantity, price type, dates and time the client chose.

To count every add, listen for both and send them to one function:

```
function itemAdded(event) {
    alert("You added " + event.detail.want + " of " + event.detail.title + " to your wishlist!");
}

document.addEventListener("gspro-item-card.add", itemAdded);
document.addEventListener("gspro-item-detail.add", itemAdded);
```

## Wishlist sent: `gspro-wishlist.submit`

Fires once each time the client sends their wishlist, right after they click Send List and before the request goes
out. Clicking Send List again while a send is still in progress doesn't fire it again. On 0.5.x it fired on every
click.

The send can still fail after this event, for example if the client loses their connection. Use it to count attempts.
Don't redirect from it: leaving the page here can stop the quote request from reaching you. Use
`gspro-wishlist.submit-complete` for anything that must happen only after a successful send.

Example (with Google Analytics):

```
document.addEventListener("gspro-wishlist.submit", function (event) {
    var itemCount = event.detail.wishlist.length;
    gtag("event", "Submission", {
        "event_category": "Wishlist",
        "event_label": "Wishlist Submission",
        "value": itemCount
    });
});
```

Reporting to Google Analytics needs [Google Analytics set up on your site](https://developers.google.com/analytics/devguides/collection/gtagjs) first.

## Quote request accepted: `gspro-wishlist.submit-complete`

Fires when Goodshuffle Pro has accepted the quote request. The client sees the "Sent!" confirmation at the same time,
and 5 seconds later the wishlist empties.

It doesn't fire when the send fails. The client sees an error instead and can try again, and `gspro-wishlist.submit`
fires again when they do.

Example (redirect to a thank-you page):

```
document.addEventListener("gspro-wishlist.submit-complete", function (event) {
    var name = event.detail.contact.firstName || "";
    window.location = "https://example.com/thank-you?name=" + encodeURIComponent(name);
});
```

## Lead form sent: `gspro-lead-form.submit` and `gspro-lead-form.submit-complete`

A [`<gspro-lead-form>`]({{< relref "/docs/components/lead-form" >}}) fires two events, like the wishlist:

- `gspro-lead-form.submit` fires when the client clicks Submit and the answers pass the form's checks, just before
  they're sent. The send can still fail after it. Use it to count attempts, not to redirect.
- `gspro-lead-form.submit-complete` fires when Goodshuffle Pro has saved the response. Use it for anything that must
  happen only after a successful submit, such as sending the client to a thank-you page.

When a send fails, nothing fires. The client sees a message asking them to try again, and `gspro-lead-form.submit`
fires again when they do.

Both carry the same `event.detail`:

| Field | Notes |
| --- | --- |
| `form` | The form's ID, as in its share link: the text after `/c/f/`, as a string |
| `answers` | A copy of the answers sent, as a list of `{ elementLogicalID, value }`, one per answered question. Changing it doesn't change what's sent |

Both fire on the `<gspro-lead-form>` tag. Like the wishlist events, they bubble, are composed and are cancelable, so a
listener on `document` hears them. Calling `preventDefault()` on either has no effect: it doesn't stop the send. With
several forms on a page, use `detail.form` to tell them apart.

Example (with Google Analytics, then a thank-you page):

```
document.addEventListener("gspro-lead-form.submit-complete", function (event) {
    gtag("event", "Submission", {
        "event_category": "Lead Form",
        "event_label": event.detail.form,
        "value": event.detail.answers.length
    });
    window.location = "https://example.com/thank-you";
});
```

## The item

The three item events carry the item as `event.detail`. Each entry in a wishlist event's `detail.wishlist` has the
same fields.

| Field | Notes |
| --- | --- |
| `id` | The item's ID in Goodshuffle Pro |
| `title` | The item's name |
| `description` | The item's description |
| `category` | The category the item is in |
| `groups` | The item's subcategories |
| `tags` | The item's tags |
| `attributes` | The item's attributes, such as size or color |
| `images` | The item's photos |
| `inventoryType` | The kind of item |
| `price` | The item's price details, as your website shows them |
| `quantity` | How many of the item you have |
| `related` | Items marked as related to this one |
| `vendorName` | Your business name |
| `want` | Quantity the client wants |
| `rate` | Price type, such as `HOURLY`, `DAILY` or `FLAT_FEE` |
| `startDate`, `endDate` | Dates as `YYYY-MM-DD`, once the client has picked them |
| `startTime` | Start time, such as `12:00 PM` |
| `hours` | Hours requested, for an `HOURLY` item |

`gspro-item-card.click` fires before the client has chosen anything. Its `want`, dates and time can be missing.

## The `detail` of both wishlist events

`gspro-wishlist.submit` and `gspro-wishlist.submit-complete` carry the same `event.detail`:

```
{
    contact: {                       // what the client typed in "Your Contact Info"
        firstName: "John",
        lastName: "Doe",
        email: "john.doe@example.com",
        phone: "5555551234"
    },
    venue: {                         // "Venue / Delivery Location", all optional
        venueName: "The Place to Be",
        addressStreet1: "123 Green St",
        addressStreet2: "Suite 101",
        city: "Washington",
        state: "DC",
        postalCode: "20032"
    },
    wishlist: [                      // one entry per item, in the order the client added them
        {
            id: "9942725a-dcd2-5d33-27b0-44f2ec408d88",
            title: "Gold Chiavari Chair",
            category: { ... },
            images: [ ... ],
            price: { ... },
            // ...the rest of the item's fields
            want: 40,
            rate: "DAILY",
            startDate: "2026-10-22",
            endDate: "2026-10-24",
            startTime: "12:00 PM"
        }
    ]
}
```

Each `wishlist` entry is the whole item. See [The item](#the-item).

### `contact`

| Field | Notes |
| --- | --- |
| `firstName`, `lastName`, `email` | Required on the form and always filled in |
| `phone` | Filled in when the client gave one. Required when the vendor turns on `require-phone-number` |

An optional field the client left blank can be missing or an empty string. Check before you use it.

### `venue`

| Field | Notes |
| --- | --- |
| `venueName` | The venue's name |
| `addressStreet1`, `addressStreet2` | Street address, two lines |
| `city` | City |
| `state` | State, province or region. Missing for countries whose form has no such field, such as the UK |
| `postalCode` | ZIP or postal code |

Every venue field is optional. Any of them can be missing or empty, and only the fields your country's form shows are
included.

The event's own dates and times aren't in `detail`.

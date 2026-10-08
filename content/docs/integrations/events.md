---
title: "Events"
weight: 30
---

# Events

The Website Integration tells your page when a client sends their wishlist. It does this with standard
[DOM events](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Events), so any script on your
page can react: report the quote request to your analytics, show your own thank-you message, or send the client to a
thank-you page.

Listening for events takes basic JavaScript and a way to add your own script to your site.

| Event | When it fires |
| --- | --- |
| `gspro-wishlist.submit` | The client clicked Send List and the wishlist is on its way |
| `gspro-wishlist.submit-complete` | Goodshuffle Pro accepted the quote request |

Both events fire on the `<gspro-wishlist>` element and bubble up to `document`, so listen on `document`:

```
document.addEventListener("gspro-wishlist.submit-complete", function (event) {
    console.log(event.detail);
});
```

## Wishlist sent: `gspro-wishlist.submit`

Fires once each time the client sends their wishlist, right after they click Send List and before the request goes
out. Clicking Send List again while a send is still in progress doesn't fire it again.

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

## The `detail` of both events

Both events carry the same `event.detail`:

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
            image: "https://...",
            price: { ... },
            minimum: 10,
            want: 40,
            rate: "DAILY",
            startDate: "2026-10-22",
            endDate: "2026-10-24",
            startTime: "12:00 PM"
        }
    ]
}
```

### `contact`

| Field | Notes |
| --- | --- |
| `firstName`, `lastName`, `email` | Required on the form, so always filled in |
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

Every venue field is optional, so any of them can be missing or empty. Only the fields your country's form shows are included.

### `wishlist`

| Field | Always there | Notes |
| --- | --- | --- |
| `id` | Yes | The item's ID in Goodshuffle Pro |
| `title` | Yes | The item's name |
| `want` | Yes | Quantity requested |
| `rate` | Yes | Price type: `HOURLY`, `DAILY`, `FLAT_FEE`, `PURCHASED`, `BY_CONTENTS_ALL`, `BY_CONTENTS_CLIENT_VISIBLE`, or `UNPRICED` for an item with no visible price |
| `image` | No | Address of the item's main photo |
| `price` | No | The item's price details, as your website shows them |
| `minimum` | No | The item's minimum quantity |
| `startDate`, `endDate` | No | Dates as `YYYY-MM-DD` |
| `startTime` | No | Start time, such as `12:00 PM` |
| `hours` | No | Hours requested, for an `HOURLY` item |

The event's own dates and times aren't in `detail`.

## Events from version 0.5.x

Sites on version 0.5.x of the Website Integration also fire `gspro-item-card.click`, `gspro-item-card.add` and
`gspro-item-detail.add` when a client opens an item or adds one to the wishlist.

**The current Website Integration doesn't fire these three events.** If your site listens for them, those listeners
stop running when you switch. See [Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

On 0.5.x, each entry in `detail.wishlist` was the whole item: its category, tags, attributes and the rest. It now holds
only the fields in the table above. A listener that reads `wishlist.length`, `contact` or `venue` works on both.

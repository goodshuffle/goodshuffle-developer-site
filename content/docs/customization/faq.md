---
title: FAQ
weight: 30
---

# FAQ

If you have a question that isn't answered here, ask us in the [blue-chat bubble on https://pro.goodshuffle.com](https://pro.goodshuffle.com).

## How do Packages show on the site?
Packages will show the photos and description of the package, along with any of the contents that you don’t have marked as “hide from contract”. A good example is [here](https://beautifuleventrentals.com/lounge-package/#!/item/9c24926d-0f3a-4aeb-9aa3-efbe63e30fba/Brooklyn%20Lounge%20-%20Styled). 

You can also have packages who show some contents, or none at all. A good example is a tent, which is comprised of many items, but you’d likely only want the client to see the name of the tent as a whole.

Packages are also a create way for you to get lead info about a client’s event. You might consider making a “Graduation Backyard Starter Pack” and including the most common things for those events. Keep in mind: you can put in the description something about the ability to add more things later.


## How do Accessories show on the site?
If you have a hidden accessory (like chalk for a chalkboard) it will not show on the website, but it will add to the project when the wishlist is submitted.

If you have accessories that show on the contract, they will show on the item card and might be a good way to show common upsell items [like this example](https://beautifuleventrentals.com/accent-chairs/#!/item/0eda09d4-1828-3155-309d-084e44cd0b87/Auburn%20Chair).

## How do I change my categories in Goodshuffle Pro?
You can’t change the categories in the software, but can use tags to create any categories you like on your website. 

## How do I create collections on my website?
Also via tags. Items can have multiple tags, therefore showing on several different pages. 

## How do I group items together by color?
To group items together by color, you can use multiple gspro-item-list elements on a single page. 
Each element should query items using tags:

```
<gspro-item-list search=”lounge” tags=”brown”></gspro-item-list>
<gspro-item-list search=”lounge” tags=”red”></gspro-item-list>
<gspro-item-list search=”lounge” tags=”orange”></gspro-item-list>
<gspro-item-list search=”lounge” tags=”white”></gspro-item-list>
<gspro-item-list search=”lounge” tags=”blue”></gspro-item-list>
``` 

Keep in mind that these will display 15 items by default.

## How do I change how many items appear in a list of items?
You can change the number of items that appear in the gspro-item-list and gspro-item-gallery 
components by setting the size attribute (e.g. size=”25”). Please be aware that loading more items 
can take more time to load.

## Why doesn’t the gspro-item-list support pagination by default?
Pagination isn’t supported by default because it is common for people to use 
multiple gspro-item-list components on a single page, this would be confusing 
to website visitors.

## Can Google Search Bot crawl wishlist content?
We have confirmed that Google search bot can crawl wishlist content by using 
Google’s search console and it appears to be neutral with respect to page rank.

## Can I customize the wishlist icon?
Yes, we have a walk-through and some video tutorials for that!

## Do you have preset templates for designs that I can use?
Not currently, but these may be available in the future. However, 
customization with CSS is straightforward for most developers. We follow 
the block element modifier (BEM) convention so that you can override our 
preset theme.

## Can I customize the text or labels?
Not at this time.

## How do I hide prices?

Yes. (we discourage it- feel free to read why in [this article](https://app.intercom.com/a/apps/rl8lfsoi/articles/articles/4180713/show)). However, only with CSS. 
Anyone that can inspect your web page’s source code may be able to see your prices. 
This is the CSS snippet to hide all price data:
:

```
.gspro-o-price {
  display: none !important;
}
```

## Does your website wishlist use cookies?
No. We store website wishlist data using a technology called “Local Storage” 
on modern web browsers. This enables us to preserve a person’s wishlist 
without using cookies. Using cookies requires consent in certain jurisdictions 
and we want to avoid imposing disclosure and consent requirements on your site.


## Does your website wishlist store my inventory data on my server?
No. Data is retrieved from Goodshuffle Pro on demand, although it is cached to improve performance.

## Do you support IE11?
No. Most visitors no longer use IE11.

## Why don’t you support Wix?
* Wix doesn’t allow custom code snippets to be embedded on their sites. They only allow integrations that are part of their official “app marketplace” which makes it impossible for fully customizable integrations like ours to work. You could embed an iFrame, but we strongly advise against it as it will not be the experience for your clients that is intended. 

* Wix users can either set up a simple redirect to another page on one of our supported platforms, or they can fully migrate to a supported platform. Our users who have migrated to Squarespace have reported being equally happy with its user-friendly interface.

## Can I obtain analytics about how people are using my site?
We do not provide this out-of-the-box, however it is something you can enable.

## Can I get Google address autocompletion for venue / delivery location?
No, this would require you to create a Google Developer account and to obtain & configure a Google API key.


## How do I hide time selection?

You can disable the display of time selection menus using this snippet of CSS:

```
.gspro-c-item-choices__start-time,
.gspro-c-duration__start-time,
.gspro-c-duration__end-time,
.gspro-o-time-label {
  display: none !important;
}
```

This will disable time selection in the wishlist date picker and item detail overlay. Please note that projects will still have a default time of noon set when a wishlist is submitted.
---
title: Troubleshooting
weight: 30
---

# Troubleshooting

If you have a question that isn't answered here, ask us in the blue-chat bubble on [https://pro.goodshuffle.com](https://pro.goodshuffle.com).

## Why isn’t my wishlist integration showing at all?
View [this help article](https://help.goodshuffle.com/en/articles/4973679-why-isn-t-my-wishlist-integration-showing-at-all) for common troubleshooting steps.

## Why isn’t a specific item showing?
Make sure it is set to [show on the Wishlist.](https://help.goodshuffle.com/en/articles/4973967-why-isn-t-an-item-showing-in-my-wishlist)

## I updated something in Goodshuffle Pro and the changes aren’t showing up
This is intentional, and a result of caching results to improve performance. [Learn more here](https://help.goodshuffle.com/en/articles/4973980-i-updated-something-in-goodshuffle-pro-and-the-changes-aren-t-showing-up-in-my-wishlist).

## I want to customize icons on WordPress, but I can’t upload a CSV file to my media library!
[View help article](https://help.goodshuffle.com/en/articles/4974017-i-want-to-customize-icons-on-wordpress-but-i-can-t-upload-a-csv-file-to-my-media-library).  

## Why are my images cut-off?
We need to support a variety of image shapes and sizes. [Learn more here.](https://help.goodshuffle.com/en/articles/4974030-why-are-my-images-cut-off-in-my-wishlist)

## Why are my items “temporarily unavailable?”
This usually indicates that you have a [configuration problem](https://help.goodshuffle.com/en/articles/4974044-why-are-my-wishlist-items-temporarily-unavailable). 

## Why do you use SVG images?
They [appear best on high DPI devices](https://help.goodshuffle.com/en/articles/4974050-why-do-you-use-svg-images).

## How long does it take for inventory changes in Goodshuffle Pro to appear on my website?
Changes to your inventory should appear on your website within [a matter of minutes](https://help.goodshuffle.com/en/articles/4974054-how-long-does-it-take-for-inventory-changes-in-goodshuffle-pro-to-appear-on-my-website-wishlist). 

## Why is my `gspro-item-gallery` search button cut-off on mobile devices?
Likely due to theme padding. [Learn how to fix it here.](https://app.intercom.com/a/apps/rl8lfsoi/articles/articles/4993747/show).

## Why are all the categories on the category sidebar not showing on mobile devices?
Likely a result of header "overlapping" the category sidebar. [Learn how to fix it here.](https://app.intercom.com/a/apps/rl8lfsoi/articles/articles/4993992/show).

## How do I disable body scroll locking?
Add `<meta name="gspro-disable-scroll-lock" content="true">` to your site header.

## How do I hide the Wishlist "Heart" Icon on certain pages?
This icon is automatically added to any pages that have a `<gspro-item-list>` or a `<gspro-item-gallery>`.

Additionally, adding the `<gspro-config></gspro-config>` (as detailed in the setup instructions) tag to your site header will load the Wishlist on all pages.

If you wish to have more control over which pages the Wishlist appears on, remove `<gspro-config></gspro-config>` from your site header. Then, add that tag to **ONLY** the pages where you would like your Wishlist Cart to appear.

**NOTE:** Our studies have shown that having the Wishlist Cart available on all pages increases rate of quote generation and conversion. We strongly recommend keeping it enabled on all pages.

## How can I control where in the DOM tree the gspro-item-detail and gspro-wishlist are located?

By default, the Wishlist injects these web components right at the end of the body.
If you want to move those elements elsewhere, simply place the following code snippet in your desired location:

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

These manually added elements will **replace** the ones automatically added to the page, not duplicate them.

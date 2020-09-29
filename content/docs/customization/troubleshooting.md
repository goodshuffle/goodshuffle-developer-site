---
title: Troubleshooting
weight: 30
---

# Troubleshooting

If you have a question that isn't answered here, ask us in the blue-chat bubble on [https://pro.goodshuffle.com](https://pro.goodshuffle.com).

## Why isn’t my wishlist integration showing at all?
* Do you have an active Goodshuffle Pro account and the website wishlist activated? (If payments default on either, the integration will fail)
* Is the required code placed correctly in the header and footer of the website? (Where and how this is done will depend on what website service you’re using, e.g. [Squarespace](https://help.goodshuffle.com/en/articles/3769571-how-can-i-connect-my-goodshuffle-pro-account-with-my-squarespace-site), [Wordpress](https://help.goodshuffle.com/en/articles/3517420-how-can-i-connect-my-goodshuffle-pro-account-with-my-wordpress-site))
* Is your website version up to date?
* Have you set the attributes for the inventory you’d like to pull?
    * *Incorrect*: `<gspro-item-list></gspro-item-list>`
    * **Correct**: `<gspro-item-list category="furniture-rentals"></gspro-item-list>`

## Why isn’t a specific item showing?
* Do you have the item set to show on wishlist? (edit the inventory item in Goodshuffle Pro)
* Do you have the tag properly set/spelled correctly?

## I updated something in Goodshuffle Pro and the changes aren’t showing up
Data is cached using a CDN (content distribution network) in order to minimize the time 
it takes to send data (and reduce the amount of data sent too). It should only take five minutes for this to update, try using a new “incognito” window to view the page. If you want to bypass the cache, you can change the size attribute of the item list to make a request for data that hasn’t been cached.

## I want to customize icons on WordPress, but I can’t upload a CSV file to my media library!
This has to do with the way some WordPress site security is configured. You can use a 
free WordPress plugin to [change these settings](https://wordpress.org/plugins/wp-extra-file-types/). 

## Why are my images cut-off?
We need to support a variety of image shapes and sizes. Images uploaded 
after the wishlist was launched in December of 2019 have an uncropped 
and unpadded image that is ideally sized for high DPI mobile devices. 
Images uploaded before then were automatically “cropped and padded” 
using a landscape dimension. In any case, you can customize the way the 
image fills the available space on the item card [using CSS and the object-fit property](https://css-tricks.com/almanac/properties/o/object-fit/). You can 
either “contain” the image (default) within the image area or “cover” 
it with the image. There are trade-offs for both, but this can be adjusted 
to whatever works best for you.

## Are my item detail “pages” indexed by Google?
No. Even though you can bookmark and share links of item details, these are not separate pages and will not be individually indexed. However, a page with an item list on it will be indexed. You should follow SEO best practices on these pages to draw your visitors to them.

## Why are my items “temporarily unavailable?”
* This usually indicates that you have a configuration problem. Please make sure you 
are using the proper public web key.
* The other cause of this problem has to do with accessing the same page from two 
different domain names. The data cached by a web browser will only work with one 
domain. This is typically seen in squarespace or webflow and is not something your 
visitors will experience since they aren’t accessing your site from inside your Website editing development interface.

## Why do you use SVG images?
These appear best on high-DPI devices and are smaller than JPG or PNG images. 
However, you are free to use any image format you like.

## How long does it take for inventory changes in Goodshuffle Pro to appear on my website?

Changes to your inventory should appear on your website within a matter of minutes. We use content distribution networks to cache wishlist related inventory data, so it is possible to see a delay.

If inventory isn’t displaying as expected, you should:

* Make sure that an item is not hidden for the wishlist
* Confirm that any tags you are using are also added to the item.
* Confirm that any keywords you are using are in the item’s name and description.

---
title: Changelog
weight: 1
---

# Changelog

### [0.5.5] - 2023-1-19

- Added ability to show packages with by contents pricing on Website Integration Pages

## [0.5.4] - 2022-12-22

- Fixed an edge case bug where search results did not properly filter when using `scope-category` or `scope-group`

## [0.5.3] - 2022-12-06

- Added support for [dynamically changing list and gallery properties]({{< relref "../integrations/listeners.md#listeners" >}})
- Improved validation for email addresses
- Improved handling timezones in a specific use case involving Daylight Savings Time
- Prevent individual pool items from appearing in lists or galleries

## [0.5.2] - 2021-12-01

- Added support for [sorting gspro-item-gallery]({{< relref "../components/item-gallery/#sort" >}}) by attributes
- Significantly expanded options provided with the `gspro-wishlist-config` element
  - Added ability to [disable time selection]({{< relref "../components/wishlist-config/#disable-time-selection" >}})
  - Added ability to [show quantities]({{< relref "../components/wishlist-config/#show-quantity-on-cardshow-quantity-on-detail" >}}) on the `gspro-item-detail` and the `gspro-item-card`
  - Added ability to make [phone numbers required]({{< relref "../components/wishlist-config/#require-phone-number" >}}) for Wishlist submission
  - Added ability to [add help text]({{< relref "../components/wishlist-config/#notes-help-text" >}}) under the "Notes" label of the Wishlist submission form

## [0.5.1] - 2021-07-13

- Fixed a rare bug resulting in duplicate wishlist submissions
- Added a new event emitter, [`gspro-wishlist.submit-complete`]({{< relref "../integrations/events.md#submit-complete" >}})

## [0.5.0] - 2021-06-10

- Added behavior to prevent background page scrolling when an item detail popup is open 
    - To disable this functionality, [look here]({{< relref "../customization/troubleshooting.md#how-do-i-disable-body-scroll-locking" >}})
- Improved look and performance of Website Integration components on certain site builders
- Simplified installation process

## [0.4.4] - 2021-02-11

- Added ability to sort `gpsro-item-list` by `item-attribute`
- Added ability to restrict scope of `gspro-item-gallery` by attribute.

## [0.4.3] - 2021-01-07

- Added event emitters to key Website Integration events. See [this page]({{< relref "../integrations/events.md" >}}) on usage.
- Improved SEO optimization. See [this FAQ]({{< relref "../customization/faq/#how-does-the-wishlist-impact-seo-search-engine-optimization" >}}) for more information.

## [0.4.2] - 2020-10-14

- `gspro-item-list` now supports filtering on custom attributes. See our [developer docs]({{< relref "../components/item-list.md#item-attribute-" >}}) for usage.
- Clicking on an item in a `gspro-item-gallery` or `gspro-item-list` will now update the canonical url, title and meta description of a Website Integration integrated site

## [0.4.1] - 2020-09-16

- Update UTM params for Powered by Goodshuffle logo

## [0.4.0] - 2020-05-14

### Changed

- `gspro-item-list` now display narrower cards so that typical websites will display more than one item per row by default.
- `gspro-item-gallery` on mobile uses fixed positioning for categories and filters instead of absolute positioning. This should improve the out-of-the-box setup experience for most people.
- `gspro-wishlist` form labels are now more concise and can be customized using CSS.
- Item cards use an absolute URL to open item detail, this may improve crawlability of item details.

### Added

- `gspro-item-gallery` now support "scoped" category, group, search, and tags.
- `gspro-item-gallery` filter and category elements can be hidden using the `show-filters="false"` and `show-categories="false"` respectively.
- `gspro-item-card` image now sets the alt attribute to any provided caption in Goodshuffle Pro.
- Price related elements can be selected (and hidden) using the `.gspro-o-price` CSS selector.
- Wishlist now has a notes field so that customers can provide additional detail.
- Data queries now include additional information about the library version to help us identify people that should upgrade.

## [0.3.2] - 2020-03-16

### Changed

- Item gallery has fewer default styles. This makes it easier to integrate with other sites (sticky headers are not good out of the box!)

## [0.3.1] - 2020-02-28

### Changed

- Use consistent BEM class names for gspro-item-gallery
- Hide gspro-item-gallery category button on desktop and display the list of categories.

## [0.3.0] - 2020-02-27

### Added

- `gspro-item-gallery` provides search and filtering of items.
- Provide sample selectors to facilitate deprecation of CSS custom properties.
- Provide search example in out-of-the-box HTML and JS.

### Changed

- The default color palette is now black and white. This is a popular choice when people customize the look and feel of the webcomponents, so we've made them the default.
- `gspro-duration` Use neutral colors (instead of Goodshuffle brand blue).
- `gsrpo-item-detail` modal overlay style is included in web component.

### Deprecated

- CSS custom properties should not be used by 3rd-parties to customize sites.
- `.gspro-c-item-card` replaces `.gspro-o-card` (there are no other cards)

## [0.2.6] - 2019-12-19

### Fixed

- Run a clean build and re-release, the previous version appears to be dirty.

## [0.2.5] - 2019-12-19

### Fixed

- `gspro-media-gallery` bug that would add null object to image list

## [0.2.4] - 2019-12-19

### Fixed

- `gspro-media-gallery` bad logic causing images to always hide.

## [0.2.3] - 2019-12-19

### Fixed

- `gspro-item-detail` no longer swallows an error when no images are present.
- `gspro-item-list` and `gspro-categories` host elements no longer have default padding (causes layout issues on mobile)

## [0.2.2] - 2019-12-19

### Changed

- `gspro-item-detail` disabled "contained in" related items (they appear to be wrong in a non-trivial way)
- `gspro-item-list` scroll to top of item list when prev / next link clicked

## [0.2.1] - 2019-12-18

### Changed

- `gspro-item-detail` and `gspro-item-card` quantity now says "Contact us..." when zero quantity available (instead of "unpriced").
- `gspro-item-detail` uses auto overflow (does not always display scrollbars).
- `gspro-item-choices` Change "Start Date" label to "Select Dates".

### Fixed

- Cleaned-up and fixed out-of-the-box JS and CSS samples.

## [0.2.0] - 2019-12-16

### Added

- Provide a `gspro-sprite` component to add remote SVG content to DOM.
- Provide a `close()` method on `gspro-item-detail` that can be invoked from 3rd party javascript.

### Changed

- Make padding of category and item list consistent.

## [0.1.8] - 2019-12-09

### Changed

- Always display date picker in item detail (not just for hourly items)

## [0.1.7] - 2019-12-09

### Fixed

- Media gallery selector (used wrong element name)

## [0.1.6] - 2019-12-05

### Fixed

- Media gallery selector (used wrong element name)

## [0.1.5] - 2019-12-05

### Changed

- Replace classnames that reference 'cart' with 'wishlist' (consistency).
- Provide way to enable renaming the wishlist using meta tag configuration.
- Use a CSS custom property for base units.

### Fixed

- Use BEM convention for `gspro-media-gallery`.

## [0.1.4] - 2019-12-01

### Fixed

- Correct typo in the wishlist message.

## [0.1.3] - 2019-12-01

### Changed

- Ensure items in wishlist have a price.

## [0.1.2] - 2019-11-27

### Fixed

- Require name and email in wishlist.

## [0.1.1] - 2019-11-27

### Changed

- Improved error messaging of wishlist if it fails to send.
- Added BEM classes to wishlist error list.

## [0.1.0] - 2019-11-25

### Added

- Categories – list the relevant categories and subcategories
- Item List – display a list of items using a category or subcategory, keyword search, or tags.
- Item Card – show a single image, title, price, and quantity.
- Item Detail – show an image gallery, description, attributes, and related items.
- Wishlist – provide a way to add items with quantities, datetime range, and contact info.
- Icon – Use a web component to make it easier to work with SVG sprites for icons.
- Duration – Create a web component wrapper for [Flatpickr.js](https://flatpickr.js.org/).
- Use [BEM contentions](http://getbem.com/introduction/).

---
title: Changelog
weight: 1
---

# Changelog

## [0.3.2] - 2020-03-16

### Changed

- Item gallery has fewer default styles. This makes it easier to integrate with other sites (sticky headers are not good out of the box!)

_[Learn more](https://keepachangelog.com/en/1.0.0/) about Changelogs._

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

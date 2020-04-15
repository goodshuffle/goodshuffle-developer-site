---
weight: 20
title: Squarespace Setup
---

# Squarespace Setup

## Requirements

You will need...

- A Squarespace site with the business-level plan.
- Administrative credentials.
- The ability to copy and paste code-snippets.

## Overview

These are the high-level steps:

1. Activate you Website Wishlist Integration.
1. Add HTML code snippets to your site's header and footer.
1. Add custom CSS to your site's design.
1. Create a page for the basic gallery and embed an HTML code snippet.

_If you prefer a narrated walk-through, checkout our [Squarespace Setup Youtube video](https://www.youtube.com/watch?reload=9&v=Ap5zhuijH90&feature=youtu.be)._

## Walk-Through

### Activation

You can do this from the [Integration Tab](https://pro.goodshuffle.com/vendorAccount/index?tab=thirdPartyIntegrations) of your account. **Copy the "Public Browser Key" on this screen for subsequent use.**

![Integration Tab](/wordpress-website-integration-activation.png)

### Inject in Site Header

You can access this by going to "Settings" &gt; "Advanced" &gt; "Code Injection"

**PLEASE NOTE! You need to update "YOUR-WEB-SITE-KEY" with your Public Browser Key from Goodshuffle Pro.**

```
<meta name="gspro-config"
      content="https://data.goodshuffle.com/vendor/YOUR-WEB-SITE-KEY" />
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.3.2/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.3.2/dist/gspro-wc/gspro-wc.js"></script>
<script src="https://unpkg.com/tua-body-scroll-lock"></script>
```

### Inject in Site Footer

You can access this by going to "Settings" &gt; "Advanced" &gt; "Code Injection"

_Be careful not to replace other code that may have been injected for other purposes._

```
<div class="gspro-gallery-omni-present">
  <gspro-wishlist></gspro-wishlist>
  <gspro-item-detail
    data-mode="inactive"
    class="gspro-u-fullscreen"
    route="/item/:id/:title*"></gspro-item-detail>
  <gspro-sprite></gspro-sprite>
</div>

<script>
(function() {
  function initBodyScrollLockListener() {
    if (bodyScrollLock == undefined) {
      return;
    }
    let itemDetail = document.querySelector(
      "gspro-item-detail.gspro-u-fullscreen"
    );
    if (!itemDetail) {
      return;
    }
    itemDetail.addEventListener("gspro-item-detail.mode", ({ detail }) => {
      if (detail == "active") {
        bodyScrollLock.lock(detail);
      } else {
        bodyScrollLock.unlock(detail);
      }
    });
  }

  function initDetailToggle() {
    var detail = document.querySelector("gspro-item-detail.gspro-u-fullscreen");
    if (!detail) {
      return;
    }
    detail.addEventListener("click", e => {
      if (e.target == detail) {
        detail.close();
      }
    });
  }

  document.addEventListener("DOMContentLoaded", () => {
    initBodyScrollLockListener();
    initDetailToggle();
  });
})();
</script>
```

### Create a Gallery Page

1. Create a page to display a basic gallery of items.
2. Insert the following snippet in a `Code` block.

```
<gspro-item-gallery></gspro-item-gallery>
```

## All Set!

You should now have a basic page that displays a list of relevant categories/subcategories and your inventory.

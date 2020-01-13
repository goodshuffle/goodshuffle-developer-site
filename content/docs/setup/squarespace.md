---
weight: 20
title: Squarespace Setup
---

# WordPress Setup

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
<script type="module" src="https://unpkg.com/@goodshuffle/gspro-wc@0.2.6/dist/gspro-wc/gspro-wc.esm.js"></script>
<script nomodule="" src="https://unpkg.com/@goodshuffle/gspro-wc@0.2.6/dist/gspro-wc/gspro-wc.js"></script>
<script src="https://unpkg.com/tua-body-scroll-lock"></script>
```

### Inject in Site Footer

You can access this by going to "Settings" &gt; "Advanced" &gt; "Code Injection"

_Be careful not to replace other code that may have been injected for other purposes._

```
<div class="gspro-gallery-omni-present">
  <gspro-wishlist> </gspro-wishlist>
  <gspro-item-detail
    data-mode="inactive"
    class="gspro-u-fullscreen"
    route="/item/:id/:title*"></gspro-item-detail>
  <gspro-sprite></gspro-sprite>
</div>

<script>
(function() {
  function initCategoryToggle() {
    // Enable category toggle control.
    let toggler = document.querySelector("#gspro-categories-toggle");
    let categories = document.querySelector("#gspro-categories");
    let body = document.querySelector("body");
    if (!toggler || !categories) {
      return;
    }
    console.log("Goodshuffle Website Integration: Enabling category toggle");
    body.addEventListener("click", () => {
      categories.classList.remove("gspro-u-active");
    });

    toggler.addEventListener("click", event => {
      categories.classList.toggle("gspro-u-active");
      event.stopImmediatePropagation();
    });
  }

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
    initCategoryToggle();
    initDetailToggle();
  });
})();
</script>
```

### Add to Site Design

This CSS is used to layout a basic gallery and make the item detail element appear as a modal overlay.

You can access this by going to "Design" &gt; "Custom CSS"

```
/**
 ** Default Goodshuffle Pro Layouts
 **/

/** Basic Category + Item List Page Layout **/

#gspro {
  position: relative;
}

@media screen and (min-width: 767px) {
  #gspro {
    display: flex;
    flex-direction: row;
  }
}

/** Category **/

#gspro gspro-categories {
  min-width: 270px;
  width: 270px;
  background: white;
  display: block;
  transition: visibility 0s linear, opacity 300ms, max-height 1000ms;
}

#gspro gspro-categories[data-mode="inactive"] {
  visibility: hidden;
  max-height: 0vh;
  opacity: 0;
}

#gspro gspro-categories[data-mode="active"] {
  visibility: visible;
  max-height: 100vh;
  opacity: 1;
}

@media screen and (max-width: 767px) {
  #gspro gspro-categories {
    display: none;
  }
  #gspro gspro-categories.gspro-u-active {
    display: block;
    position: absolute;
    top: 0;
    width: 90%;
    max-width: 390px;
    height: 270px;
    overflow-y: scroll;
    box-shadow: 0 4px 5px 0 rgba(0, 0, 0, 0.14), 0 1px 10px 0 rgba(0, 0, 0, 0.12), 0 2px 4px -1px rgba(0, 0, 0, 0.2);
    z-index: 1;
  }
  #gspro gspro-categories.gspro-u-active::-webkit-scrollbar {
    -webkit-appearance: none;
  }
  #gspro gspro-categories.gspro-u-active::-webkit-scrollbar:vertical {
    width: 11px;
  }
  #gspro gspro-categories.gspro-u-active::-webkit-scrollbar-thumb {
    border-radius: 8px;
    border: 2px solid white;
    background-color: rgba(0, 0, 0, 0.5);
  }
}

@media screen and (min-width: 767px) {
  #gspro gspro-categories[data-mode="inactive"] {
    visibility: visible;
    opacity: 1;
    max-height: inherit;
  }
  .gspro-u-hide-desktop {
    display: none;
  }
}

/** Item List Layout **/

#gspro gspro-item-list {
  background: white;
  overflow-y: auto;
  width: 100%;
}

/** Wishlist **/

gspro-wishlist header::before, gspro-wishlist header::after {
  content: none;
}

/** Item Detail Modal **/

gspro-item-detail.gspro-u-fullscreen {
  position: fixed;
  background: white;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 100;
  transition: visibility 0s, opacity 0.5s linear;
  overflow: scroll;
}

gspro-item-detail.gspro-u-fullscreen[data-mode="inactive"] {
  visibility: hidden;
  opacity: 0;
}

gspro-item-detail.gspro-u-fullscreen[data-mode="active"] {
  visibility: visible;
  opacity: 1;
}

@media screen and (min-width: 767px) {
  gspro-item-detail.gspro-u-fullscreen {
    background: rgba(0, 0, 0, 0.3);
    max-height: 100%;
    padding: 0 12px;
  }
  gspro-item-detail.gspro-u-fullscreen>div {
    background: white;
    border-radius: 4px;
    width: 95vw;
    max-width: 980px;
    height: 80vh;
    margin: 10vh auto;
    overflow: auto;
    box-shadow: 0 16px 24px 2px rgba(0, 0, 0, 0.14), 0 6px 30px 5px rgba(0, 0, 0, 0.12), 0 8px 10px -5px rgba(0, 0, 0, 0.2);
  }
}
```

### Create a Gallery Page

1. Create a page to display a basic gallery of items.
2. Insert the following snippet in a `Code` block.

```
<div class="gspro-gallery-viewer" id="gspro">
  <gspro-categories route="/inventory/:category?/:group?"
  ></gspro-categories>
  <gspro-item-list route="/inventory/:category?/:group?"
    category="furniture-rentals"
  ></gspro-item-list>
</div>
```

## All Set!

You should now have a basic page that displays a list of relevant categories/subcategories and your inventory.

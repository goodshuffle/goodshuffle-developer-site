---
weight: 60
title: Lovable Setup
---

# Lovable Setup

A Lovable site is a React app. The snippet goes in the app's `index.html`, and the gallery goes in the page component
that should show your inventory. You can ask Lovable's chat to make both changes, or make them yourself in the code.

## Requirements

You will need:

- A Lovable project, and a way to edit it: Lovable's chat, its code editor, or the GitHub repository it syncs to.
- The address your site is published at.
- An active Website Integration on your Goodshuffle Pro account.

## Overview

1. Copy your Public Browser Key from Goodshuffle Pro.
2. Add the snippet to `index.html`.
3. Add the gallery to a page.
4. Publish, then send a test quote request.
5. Optional: add a lead form.

If your app is on version 0.5.x, replace the two script tags in `index.html`. See
[Switching from 0.5.x]({{< relref "/docs/setup/switching-from-0-5" >}}).

## Walk-through

### 1. Copy your Public Browser Key

In Goodshuffle Pro, open the [Integrations tab](https://pro.goodshuffle.com/app/vendorAccount/index?tab=thirdPartyIntegrations)
and activate the Website Integration if it isn't active yet. **Copy the Public Browser Key.**

![Integration Tab](/wordpress-website-integration-activation.png)

### 2. Add the snippet to `index.html`

The snippet goes inside `<head>` in `index.html`, at the root of the project:

{{< embed-code >}}
<script src="LOADER_URL"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
{{< /embed-code >}}

> The script tag also adds the release's stylesheet, `gspro-embed.css`, so you don't need a stylesheet tag or a
> CSS import. It pins version
> {{< embed-version >}}. See [Updating to a newer version]({{< relref "/docs/setup/updating" >}}), or
> [Automatic updates with v1]({{< relref "/docs/setup/updating#automatic-updates-with-v1" >}}) to get 1.x fixes
> without editing.

Replace `YOUR-PUBLIC-WEBSITE-KEY` with the key you copied.

To do it from Lovable's chat, send a message like this, with the snippet and your key pasted in:

{{< embed-code lang="text" >}}
Add these two tags inside the <head> of index.html, exactly as written.
Don't change them, don't move them into a React component, and don't add anything else:

<script src="LOADER_URL"></script>
<gspro-wishlist-config
    data-url="https://data.goodshuffle.com/vendor/YOUR-PUBLIC-WEBSITE-KEY"
></gspro-wishlist-config>
{{< /embed-code >}}

Check the result in `index.html` afterwards. The tags should be there exactly as above.

To change settings, such as the wishlist's name or a required phone number, add attributes to
`<gspro-wishlist-config>`. See [Wishlist Config]({{< relref "/docs/components/wishlist-config" >}}).

### 3. Add the gallery to a page

In the component for the page that should show your inventory (for example `src/pages/Rentals.tsx`), put the gallery
tag where the gallery should appear:

```
export default function Rentals() {
  return (
    <main>
      <h1>Rentals</h1>
      <gspro-item-gallery></gspro-item-gallery>
    </main>
  );
}
```

Attributes go on the tag as plain text, the same as in HTML: `<gspro-item-list category="decor-rentals"></gspro-item-list>`.

TypeScript doesn't know the `gspro-*` tags and may flag them as errors. Add this file to the project to declare them:

```
// src/gspro-elements.d.ts
import type { DetailedHTMLProps, HTMLAttributes } from "react";

type GsproTag = DetailedHTMLProps<HTMLAttributes<HTMLElement>, HTMLElement> & {
  [attribute: string]: unknown;
};

interface GsproTags {
  "gspro-item-gallery": GsproTag;
  "gspro-item-list": GsproTag;
  "gspro-item-card": GsproTag;
  "gspro-lead-form": GsproTag;
}

declare module "react" {
  namespace JSX {
    interface IntrinsicElements extends GsproTags {}
  }
}

declare global {
  namespace JSX {
    interface IntrinsicElements extends GsproTags {}
  }
}
```

From the chat, you can ask: "On the Rentals page, render `<gspro-item-gallery></gspro-item-gallery>` as a plain HTML
custom element below the heading, and declare the gspro-item-gallery, gspro-item-list, gspro-item-card and
gspro-lead-form tags for TypeScript in src/gspro-elements.d.ts."

### 4. Publish and send a test quote request

1. Publish the project.
2. In Goodshuffle Pro, make sure your brand's website address is the address your site is published at.
3. On the published site, open the gallery page and pick a category.
4. Click the heart on an item to add it to the wishlist.
5. Open the wishlist, choose dates, then **Contact & Venue Info**.
6. Fill in your name and email, then **Send List**.

In Goodshuffle Pro, the request appears as a new project under **Projects**, **Filters**, Origin = "Website".

### 5. Add a lead form

A lead form shows one of your Goodshuffle Pro Custom Forms on a page, styled by your site. See
[Lead Form]({{< relref "/docs/components/lead-form" >}}).

1. In Goodshuffle Pro, open the form and make sure it's published. In its **Share** section, copy the lead form tag.
   It looks like this, with your form's link in `form`:

```
<gspro-lead-form form="https://www.goodshuffle.com/c/f/FORM_ID"></gspro-lead-form>
```

2. In the component for the page where the form should go (for example `src/pages/Contact.tsx`), put the tag where
   the form should appear:

```
export default function Contact() {
  return (
    <main>
      <h1>Contact us</h1>
      <gspro-lead-form form="https://www.goodshuffle.com/c/f/FORM_ID"></gspro-lead-form>
    </main>
  );
}
```

3. Make sure `src/gspro-elements.d.ts` lists `"gspro-lead-form"`. If your project doesn't have that file yet, add it
   as shown in step 3.
4. Publish the project.
5. On the published site, fill in the form and click **Submit**. The response shows in the form's **Responses** in
   Goodshuffle Pro.

<!-- GSPRO-32473: submit and Responses for the lead form land with GSPRO-32473. Confirm this check then. -->

From the chat, you can ask this, with your own form tag pasted in: "On the Contact page, render
`<gspro-lead-form form="https://www.goodshuffle.com/c/f/FORM_ID"></gspro-lead-form>` exactly as written, as a plain
HTML custom element below the heading, and declare gspro-lead-form for TypeScript in src/gspro-elements.d.ts."

The form needs only the script tag from step 2. If you only want forms on your site, put just this line in the
`<head>` of `index.html`. You can leave out `<gspro-wishlist-config>`:

{{< embed-code >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

## Things to know on Lovable

- **Test on the published site.** Inventory loads on the website address saved for your brand in Goodshuffle Pro.
  Lovable's in-editor preview runs on another address, and the gallery may stay empty there.
- **Keep the snippet in `index.html`.** React doesn't reliably run a `<script>` tag that a component renders. Keep the
  script tag out of your components.
- **The address hash.** The Website Integration keeps the client's place in the catalog after `#!` in the page
  address. If your app's router also uses the hash (`HashRouter`), the two clash. Use a router that doesn't use the
  hash, such as `BrowserRouter`.
- **Later AI edits.** Lovable's chat can rewrite `index.html` or the page while making other changes. If the gallery
  disappears after an edit, check that both tags are still there.

## When it doesn't work

- **No wishlist button.** Check that both tags are in the `<head>` of `index.html` and that you published.
- **The gallery shows nothing.** Check that the page renders `<gspro-item-gallery>` and that you're on the published
  site.
- **The button shows but no items load.** Check the key, and that your brand's website address in Goodshuffle Pro
  matches the published address.

See also [Getting Started]({{< relref "/docs/setup" >}}) and [Troubleshooting]({{< relref "/docs/customization/troubleshooting" >}}).

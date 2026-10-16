---
title: "Lead Form"
weight: 40
---

# Lead Form

<!-- Release: confirm which Website Integration release first includes <gspro-lead-form> (GSPRO-32472). If it's later
than params.embed.version in config.toml, move the version (and the WordPress plugin's pin) before this page publishes. -->

## Overview

Use the `gspro-lead-form` web component to show one of your Goodshuffle Pro Custom Forms on a page of your own site.
It's the same form your share link opens, but it sits inside your page and takes your site's font and CSS.

```
<gspro-lead-form form="https://www.goodshuffle.com/c/f/FORM_ID"></gspro-lead-form>
```

When a client submits the form, the response lands in the form's **Responses** in Goodshuffle Pro, the same as a
response sent from the share link. See [After the client submits](#after-the-client-submits).

The form needs only the Website Integration's script tag on the page:

{{< embed-code >}}
<script src="LOADER_URL"></script>
{{< /embed-code >}}

It doesn't need the `<gspro-wishlist-config>` settings tag. If your site already has the snippet from your
[setup guide]({{< relref "/docs/setup" >}}), the script tag is already there: just add the form tag to a page. A page
can hold several forms, each with its own tag.

## All attributes

| Attribute | Default | What it does |
| --- | --- | --- |
| `form` | None. Required | The form's share link, `https://www.goodshuffle.com/c/f/FORM_ID` |

## Attributes

### `form`

The form to show. Paste the form's share link exactly as Goodshuffle Pro gives it.

#### Q: Where do I find the share link?

1. In Goodshuffle Pro, open the form. Make sure it's published.
2. Go to its **Share** section.
3. Copy the **Website Integration code**. It's the `<gspro-lead-form>` tag, with the form's share link already in
   `form`.

The Share section also has the form's **Embed code**, an iframe. See [Lead form or Embed code](#lead-form-or-embed-code)
below.

<!-- GSPRO-32476 adds the "Website Integration code" row to the form's Share section (goodshuffle PR #9099), next to
the iframe "Embed code". Match the labels above to that screen once it ships. -->

The form's ID on its own also works, for example `form="FORM_ID"`. The share link is the safer choice: it's what
Goodshuffle Pro gives you, so there's nothing to edit.

Only a Goodshuffle share link works: an `https://` address on `goodshuffle.com` whose path is `/c/f/` followed by the
form's ID. Any other address shows [This form isn't available](#this-form-isnt-available).

Changing `form` later, for example with JavaScript, loads the other form in its place.

A project-specific link, one that ends in `?p=` and a number, isn't supported here. The form still shows, but its
answers are filed against the form only, not the project, and the browser console shows a warning. Use the form's
plain share link.

<!-- GSPRO-32471: the attribute's format (share link or ID, and which hosts) and whether a vendor's page can load the
form cross-site are both pending that decision. form-attribute.ts is the one place the rule lives; update this
section to match when GSPRO-32471 is decided. -->

## This form isn't available

In place of the form, the tag shows "This form isn't available." when:

- `form` is missing, or isn't a Goodshuffle share link or form ID;
- the form doesn't exist, isn't published, or is archived;
- your Goodshuffle Pro account doesn't have Custom Forms;
- the form can't be reached, for example because the client is offline, or Goodshuffle Pro didn't answer within
  15 seconds;
- the answer from Goodshuffle Pro isn't a form.

To fix it, publish the form (or restore it) in Goodshuffle Pro, then copy its Website Integration code again from the Share section.

While the form loads, the tag is empty. To hide the message instead of showing it, see
[Styling](#styling).

<!-- GSPRO-32471: how a vendor's page reaches marketplace (cross-site access) isn't settled. Until it is, don't promise
the form loads in a builder's editor preview. Test on the published site, as the setup guides say. -->

## Styling

The form takes your page's font and fills the width of the column it sits in. In a narrow column, side-by-side fields,
such as a date range or city, state and ZIP, stack.

Every part has a class you can style with your site's CSS:

| Class | On |
| --- | --- |
| `gspro-c-lead-form` | The `<gspro-lead-form>` tag itself |
| `is-loading`, `is-ready`, `is-unavailable` | Also on the tag, one at a time: the form is loading, showing, or unavailable |
| `gspro-c-lead-form__form` | The box that holds every question and the Submit button (a `<div>`, not a `<form>`) |
| `gspro-c-lead-form__question` | Each question |
| `gspro-c-lead-form__label` | A question's label |
| `gspro-c-lead-form__input` | A question's field. For an address, a date range, a date and time range, or a group of checkboxes, radio buttons or Yes/No choices, the wrapper around the group |
| `gspro-c-lead-form__error` | A question's error message, such as "This field is required." |
| `gspro-c-lead-form__submit` | The Submit button |
| `gspro-c-lead-form__confirmation` | The message shown after a successful submit |
| `gspro-c-lead-form__upload-fallback` | The "Open the form on Goodshuffle to attach files" link on a file question, when the upload can't run from your page |
| `gspro-c-lead-form__unavailable` | The "This form isn't available." message |

<!-- The form-level submit error (above Submit) has no documented class; add a row if it gets one. -->

For example, add this to your site's CSS:

```
/* Labels in bold */
.gspro-c-lead-form__label {
    font-weight: 600;
}

/* Text fields with your brand's border color. On a group (checkboxes, radio buttons,
   Yes/No, an address or a range) the class is on the wrapper, so this doesn't reach
   the controls inside it. */
.gspro-c-lead-form__input {
    border-color: #b89b72;
}

/* The Submit button in your brand's colors */
.gspro-c-lead-form__submit {
    background: #2f4f4f;
    color: #ffffff;
}

/* Error messages in your own red */
.gspro-c-lead-form__error {
    color: #b00020;
}

/* Show nothing at all when the form isn't available */
.gspro-c-lead-form.is-unavailable {
    display: none;
}
```

Your site's rules on these classes win over most of the form's own styles. Two of the form's rules are more specific
than a single class: the one that gives labels, headings, buttons and fields your page's font, and the one that keeps
text fields within the column's width (`min-width` and `max-width`). So a rule like
`.gspro-c-lead-form__label { font-family: ... }` or `.gspro-c-lead-form__input { max-width: ... }` doesn't apply. Start the rule with the tag name instead, for example
`gspro-lead-form .gspro-c-lead-form__label`. That matches the form's rule, and yours wins because the Website
Integration's stylesheet comes first on the page. The same works when your theme's rules are more specific. See
[Colors and Typography]({{< relref "/docs/customization/colors-and-typography" >}}).

## Questions

The form shows your questions in the order you set them in the form builder, with the same required questions
and the same rules for when a question shows.

Address questions are typed by hand. If your page already loads Google Maps Places for your own use, the address
field suggests addresses as the client types.

Clients attach files right in the form, and the files upload straight to Goodshuffle's file storage. The file types
and sizes allowed are the same as on the form's share page.

If the client's browser can't upload from your page, the question says "Couldn't upload from this page." and shows a
link, "Open the form on Goodshuffle to attach files". The link opens the form's share page in a new tab. The answers
the client already gave on your page stay as they are.

## After the client submits

When the client clicks **Submit**, the form checks the answers first and shows an error under any question that needs
fixing. Then it sends them. The Submit button can't be pressed again while the answers are on their way.

- **Sent.** The form is replaced by your confirmation message, as you set it on the form in Goodshuffle Pro, or by a
  default one if you didn't set any. The response shows in the form's **Responses**.
- **Not sent**, for example because the client lost their connection. A message asks the client to try again. Nothing
  they typed is lost.

To react to a submit with your own script, for example to report it to your analytics or send the client to a
thank-you page, see [Events]({{< relref "/docs/integrations/events" >}}).

## Languages

The form's own text shows in English, Spanish or French: the Submit button, the required marker, error messages,
field placeholders, the calendar for a single-date question, the address fields, the file field, the "try again"
message, the default confirmation's title and text, and the "This form isn't available." message.

Date range, date and time, date and time range, and time questions use the browser's own date and time fields. Those
follow the language of the client's browser, not the form's.

Your questions, answer choices, help text, content blocks and your own confirmation message show exactly as you wrote
them, in any language.

The form uses the same language as the rest of the Website Integration. That is English, unless multiple languages
are turned on for your Goodshuffle Pro account and the page also has the
[`<gspro-wishlist-config>`]({{< relref "/docs/components/wishlist-config" >}}) settings tag. Then it's the language
the client picked in the language selector, or their browser's language if that's Spanish or French.

## Lead form or Embed code

The form's Share section in Goodshuffle Pro offers two ways to put the form on your site:

| | Lead form (`<gspro-lead-form>`) | Embed code (iframe) |
| --- | --- | --- |
| Needs | The Website Integration's script tag on the page | Nothing else |
| Looks | Like your site: your font and your CSS | Like the form's share page, in a box on your page |
| Events | [`gspro-lead-form.submit` and `submit-complete`]({{< relref "/docs/integrations/events" >}}) | None |

Use the **Embed code** for the quickest setup, or if your site doesn't use the Website Integration. Paste it where
the form should go. Use the lead form when you want the form to match your site.

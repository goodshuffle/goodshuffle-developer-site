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
response sent from the share link.

<!-- GSPRO-32473: submit, the confirmation and the events aren't built yet. Until then a submit that passes
validation shows the form's error message. Confirm this paragraph when GSPRO-32473 lands. -->

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
3. Copy the lead form tag shown there. It already holds the form's share link in `form`.

The Share section also has the form's **Embed code**, an iframe. See [Lead form or Embed code](#lead-form-or-embed-code)
below.

<!-- GSPRO-32476 adds the lead form tag to the form's Share section, next to the iframe "Embed code". Match the labels
above to that screen once it ships. -->

The form's ID on its own also works, for example `form="FORM_ID"`. The share link is the safer choice: it's what
Goodshuffle Pro gives you, so there's nothing to edit.

Only a Goodshuffle share link works: an `https://` address on `goodshuffle.com` whose path is `/c/f/` followed by the
form's ID. Any other address shows [This form isn't available](#this-form-isnt-available).

Changing `form` later, for example with JavaScript, loads the other form in its place.

## This form isn't available

In place of the form, the tag shows "This form isn't available." when:

- `form` is missing, or isn't a Goodshuffle share link or form ID;
- the form doesn't exist, isn't published, or is archived;
- the form can't be reached, for example because the client is offline, or Goodshuffle Pro didn't answer within
  15 seconds.

To fix it, publish the form (or restore it) in Goodshuffle Pro, then copy its tag again from the Share section.

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
| `gspro-c-lead-form__form` | The form |
| `gspro-c-lead-form__question` | Each question |
| `gspro-c-lead-form__label` | A question's label |
| `gspro-c-lead-form__input` | A question's field. For an address or a date range, the group of fields |
| `gspro-c-lead-form__error` | A question's error message, such as "This field is required." |
| `gspro-c-lead-form__submit` | The Submit button |
| `gspro-c-lead-form__confirmation` | The message shown after a successful submit |
| `gspro-c-lead-form__unavailable` | The "This form isn't available." message |

<!-- GSPRO-32473: gspro-c-lead-form__confirmation shows only once submit is built. Confirm the row then. -->

For example, add this to your site's CSS:

```
/* Labels in bold */
.gspro-c-lead-form__label {
    font-weight: 600;
}

/* Fields with your brand's border color */
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

Your site's rules on these classes win over the form's own styles. If a rule doesn't apply, your theme may be more
specific. Make the rule more specific too, for example `gspro-lead-form .gspro-c-lead-form__submit`. See
[Colors and Typography]({{< relref "/docs/customization/colors-and-typography" >}}).

## Questions

The form shows your questions in the order you set them in the form builder, with the same required questions
and the same rules for when a question shows.

Address questions are typed by hand. If your page already loads Google Maps Places for your own use, the address
field suggests addresses as the client types.

<!-- GSPRO-32474: file upload questions aren't built in the component yet (picking a file does nothing). Add a short
note about file questions here when GSPRO-32474 lands. Don't say uploads work until then. -->

## Languages

The form's own text shows in English, Spanish or French: the Submit button, the required marker, error messages,
field placeholders, the date picker, the address fields and the "This form isn't available." message.

Your questions, answer choices, help text and content blocks show exactly as you wrote them, in any language.

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

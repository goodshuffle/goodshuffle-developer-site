# GSPRO-32477: Lead form docs on the developer site

Epic GSPRO-32449 (Lead Forms component). The branch is `kyser/GSPRO-32477/lead-form-docs`, cut from
`kyser/GSPRO-32449/lead-forms-component`, which equals `kyser/GSPRO-31876/builder-guides` at 721ca662. It builds on
the GSPRO-31876 builder guides and reuses their pinned snippet (`params.embed` in `config.toml`, the `embed-code`
shortcode).

## Goal

A vendor on any of the six supported builders can follow one short step and show a published Goodshuffle Custom Form
on their own page with `<gspro-lead-form>`, styled by their site, with responses landing in the form's Responses.

## Sources

| Source | Used for |
|---|---|
| marketplace `origin/kyser/GSPRO-32472/lead-form-element`, `docs/plans/2026-10-15-GSPRO-32472-lead-form-element.md` | The tag, its one attribute, one build file, no settings tag needed, documented class names, states, sizing |
| `src/embed/lead-form/form-attribute.ts` | What `form` accepts: an https share link `/c/f/FORM_ID` on `goodshuffle.com` / `goodshuffle.dev` (or a subdomain), or a bare form ID read against `https://www.goodshuffle.com`. Anything else is unavailable |
| `src/embed/lead-form/view.tsx`, `api.ts` | `is-loading` / `is-ready` / `is-unavailable` on the tag; the unavailable message for a bad attribute, a 404 (unknown, unpublished, archived), a network failure, or no answer in 15 seconds (`LOAD_TIMEOUT_MS`). Changing `form` loads the other form. Several forms per page |
| `src/embed/lead-form/form.tsx`, `CustomFormRenderer/form-labels.ts` | The `gspro-c-lead-form__*` part classes; vendor-written text is never translated |
| `src/embed/lead-form/labels.ts`, `src/i18n/locales/{en,es,fr}/embed.json` | The form's own text in en/es/fr; "This form isn't available." and its translations |
| `src/embed/i18n/language.ts`, `use-language.ts` | The language follows the Website Integration: English unless the account has multiple languages on, which the widget learns from the settings tag |
| `src/embed/styles/embed.css` | The form takes the page's font; it fills its column and stacks side-by-side rows below 32rem; vendor CSS on the documented classes wins |
| `src/embed/app/wishlist/send.ts` | `gspro-wishlist.submit` / `submit-complete` are `bubbles`, `composed` and `cancelable`; the lead form's events are planned to match |
| wp-gspro-gallery `origin/kyser/GSPRO-32532/pinned-widget-address`, `includes/class-gspro-gallery.php` | The plugin adds the script tag to every page whenever it's active (`gspro_on`, set on activation), so a WordPress page needs only the tag in a Custom HTML block |

## Pages

| Path (`content/docs/`) | Change |
|---|---|
| `components/lead-form.md` | New, weight 40, beside Item Card, Item Gallery, Item List and Wishlist Config. The `form` attribute and where to copy it (the form's Share section), script tag only, every class name with a restyling example, the unavailable state, languages, Lead form or Embed code |
| `integrations/events.md` | `gspro-lead-form.submit` and `gspro-lead-form.submit-complete` in the table and a section with `detail: {form, answers}` and the flags |
| `setup/squarespace.md`, `wordpress.md`, `wix.md`, `showit.md`, `gohighlevel.md`, `lovable.md` | An "Add a lead form" step after the test quote request, in each guide's own way of placing HTML; Overview lists it |
| `setup/custom-setup.md`, `setup/_index.md` | One short lead form step / line, pointing at the component page |

## Decisions

| Decision | Choice | Why |
|---|---|---|
| Where the step goes | Last numbered step in each guide, marked optional in the Overview | The catalog steps and the test quote request stay as they are; a form-only vendor reads the one step |
| Form-only sites | Each step says the form needs only the script tag, and shows the script line alone through `embed-code` | The view reads no settings; the loader address stays in one place |
| Snippet value | `form="https://www.goodshuffle.com/c/f/FORM_ID"`, copied from the Share section | Ticket. The bare ID is mentioned on the component page only |
| Wix | A Custom Element with Tag Name `gspro-lead-form` and attribute `form`, same Server URL | That's how the guide places every other tag |
| Lovable | The tag in a page component; `gspro-lead-form` added to the existing `src/gspro-elements.d.ts` snippet | The guide's existing pattern. `EmbedElement` has no `form` property, so React sets it as an attribute |
| Restyling | Plain CSS on the documented classes, with one example block | The form's styles sit in cascade layers or under `:where()`, so the vendor's unlayered rules on these classes win |
| Pending tickets | HTML comments in the source, not visible text | Ticket asks for comments. Hugo 0.62.1's Goldmark (no `unsafe`) prints them as `<!-- raw HTML omitted -->`, so nothing shows on the page |

## Pending other tickets (HTML comments in the source)

- **GSPRO-32473 (submit, confirmation, events)** and **GSPRO-32474 (file upload)** are built (marketplace
  `origin/kyser/GSPRO-32473/lead-form-submit` at 397a1ea4, `kyser/GSPRO-32474/lead-form-file-upload` at 37a0e025).
  Their comments are replaced with real content: "After the client submits" and file questions on the component
  page, the events' timing, `detail` (`form`, a copy of `answers`), no effect from `preventDefault()`, and each
  guide's Responses check. A `?p=` project link isn't supported in the tag.
- **GSPRO-32471 (cross-site access).** Whether marketplace answers a vendor's page, and whether builder preview
  addresses work. Comment on the component page.
- **GSPRO-32476 (Share section).** The exact labels in the form's Share section. Comment on the component page.
- **Release.** Which Website Integration release first ships `<gspro-lead-form>`. If it's later than
  `params.embed.version`, bump the version (and the WordPress plugin's pin) before these pages publish. Comment on the
  component page and the WordPress step.

## Acceptance criteria

- Each supported builder's guide includes adding a lead form: done in the source.
- Following the step on a fresh site shows the form and a submission lands in the form's Responses: can't be proven
  here. Cross-site loading is GSPRO-32471, and no release with the tag is live yet. The
  steps follow each guide's existing, reviewed placement of HTML.

## Not done here

- Building the site: Hugo isn't installed here and isn't to be installed. Pages are checked by reading, against the
  shortcodes and `relref` forms the existing pages use.
- Pushing or opening a PR.

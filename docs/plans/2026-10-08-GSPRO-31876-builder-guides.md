# GSPRO-31876: Setup guide for each site builder

Epic GSPRO-31790 (Website Integration Rebuild). Repo `goodshuffle-developer-site` (Hugo, `book`
theme, Netlify). The branch is `kyser/GSPRO-31876/builder-guides`, cut from the feature branch
`kyser/GSPRO-31790/website-integration-rebuild`, which was cut from `origin/master` on 2026-10-08.
The repo had no `docs/plans/` folder; this file starts it. It sits outside `content/`, so Hugo
doesn't publish it.

## Goal

A vendor on Squarespace, WordPress, Wix, Showit, GoHighLevel or Lovable can follow one page and end
up with a working catalog and a quote request that lands in Goodshuffle Pro. Every snippet pins one exact
release, `https://embed.goodshuffle.com/releases/VERSION/loader.js`, with host and version set once in
`config.toml` (pinning per the ticket's 2026-10-14 change after Brandon's review; host and version 1.0.0 decided by
Kyser on 2026-10-15). `/v1/loader.js` is an opt-in, explained in one section. The reference pages list every attribute with the default the rebuilt
widget actually uses, and the Events page gives the exact `detail` of the two submit events.

## Sources

| Source | Used for |
|---|---|
| Requirements 4130111489, "Vendors follow a setup guide for their site builder" | The six builders, the new script address |
| Solution Architecture 4130471937, Migration and compatibility | What each kind of vendor changes when switching |
| Hosting proposal 4140761090 (draft) | The loader is one plain script that adds the release's JS and CSS; numbered releases stay published. Was NEED CONFIRMATION; the loader behavior is now checked against `release.mjs` (below) |
| `wwi` skill (agent-rules PR #53) section 5 and `references/help-articles.md` | Activation, key, the platform quirks the help center covers |
| marketplace `kyser/GSPRO-32057/legacy-elements` | `src/main/react-client/src/embed/elements/attributes.ts` (every attribute and default), `app/settings.ts` (config fallbacks), `app/wishlist/send.ts`, `payload.ts` and `entry.ts` (events and entry shape), `app/catalog/query.ts` (what loads when), plan `2026-10-03-GSPRO-31877-host-page-tests.md` (where each builder takes the snippet) |
| wp-gspro-gallery PR #20 (GSPRO-31875, head `1737a52`) | Security fixes and shortcodes: the main settings page labels, the four shortcodes and the two retired ones (`class-gspro-gallery-shortcodes.php`) |
| wp-gspro-gallery PR #21 (GSPRO-32532, plugin 0.6.0, head `febb485`) | Everything about which widget the plugin loads: the pinned default `GSPRO_GALLERY_WIDGET_LOADER_URL` (`https://embed.goodshuffle.com/releases/1.0.0/loader.js`), Advanced Settings labels and help text and the "Your site loads" row (`admin/partials/gspro-gallery-admin-display.php`), the Modern JS / Legacy JS behavior table, old unpkg defaults counting as empty, https for `embed.goodshuffle.com`, the `/v1/` opt-in and upgrade behavior (PR body, `docs/plans/2026-10-15-GSPRO-32532-pinned-widget-address.md`, `docs/testing/README.md`). Icon URL unchanged and unread since gspro-wc 0.2 |
| marketplace `kyser/GSPRO-31870/wishlist-cart` (also in `kyser/GSPRO-32329/legacy-events`), `src/main/react-client/src/embed/app/wishlist/storage.ts` | Wishlists carry over: `migrateLegacy()` moves the cart 0.5.x saved under `gspro.wishlist` to the vendor's own key on first load. gspro-wc has used the `gspro.wishlist` key since 2019 (`gspro-wishlist.tsx:17`) |
| `wir-testing-findings.md` | Real failure modes: origin check, key rotation, boolean parsing |
| Git history of `content/docs/setup/showit.md` (removed in 860c083) | Showit editor steps |
| marketplace PR #450 (`fix/embed-release-publishing`), `src/main/react-client/scripts/embed/release.mjs` | What `loader.js` does: `loaderSource()` adds `<link rel="stylesheet" href=".../releases/VERSION/gspro-embed.css">` and `<script src=".../releases/VERSION/gspro-embed.js">` to `<head>`, does nothing if the bundle is already on the page, and works as a plain script or `type="module"`. Release folders are create-only and never deleted; `/v1/loader.js` points at the newest 1.x release only |
| GSPRO-32532 | The WordPress plugin release (0.6.0, PR #21) that pins the widget address. Its download link is still to come |

## Pages

| Path (`content/docs/`) | Change |
|---|---|
| `setup/_index.md` | Lists the six builders, the shared pinned snippet and what the one tag does |
| `setup/switching-from-0-5.md` | New. Replace the two script tags with the one pinned tag; nothing else changes, with the one approved difference (submit fires once per send, GSPRO-31871). The check after switching is per builder: the widget renders, and the address shows in the page source (WordPress: "Your site loads"; Wix: each element's Server URL) |
| `setup/updating.md` | New. Where each builder keeps the address, with WordPress and Wix spelled out; changelog link (plus the WordPress Plugin page for plugin releases); the opt-in "Automatic updates with v1" section every guide links to, with how to switch on WordPress, Wix and the rest |
| `setup/squarespace.md` | Rewritten on the pinned snippet |
| `setup/wordpress.md` | Rewritten. Settings page, gallery page and shortcodes match PR #20 (GSPRO-31875). Which widget loads, Advanced Settings, the `/v1/` opt-in, staying on a version and what happens on upgrade match PR #21 (GSPRO-32532, plugin 0.6.0). Only the 0.6.0 download link is still a placeholder |
| `resources/wordpress.md` | Placeholder for the 0.6.0 download link and date; says 0.6.0 loads 1.0.0 |
| `setup/wix.md` | Rewritten. The Custom Element's Server URL is the pinned loader; no `custom-elements/index.js` |
| `setup/showit.md` | Restored (it was emptied in 860c083) on the pinned snippet |
| `setup/gohighlevel.md` | New |
| `setup/lovable.md` | New |
| `setup/weebly.md`, `setup/custom-setup.md` | Same pages, pinned snippet, current Integrations link, gallery behavior stated correctly. `custom-setup.md` says what the loader does |
| `components/*.md` | An "All attributes" table per tag from `attributes.ts`; Wishlist Config's wrong `# Item List` heading fixed; "added in v0.5.x" markers removed |
| `integrations/events.md` | Every 0.5.11 event vendors listen for (`gspro-item-card.click`, `gspro-item-card.add`, `gspro-item-detail.add`, `gspro-wishlist.submit`, `submit-complete`) with 0.5.11's full `detail`, stated as available (the page publishes after GSPRO-32329) |
| `integrations/listeners.md` | The "requires 0.5.3 or greater" line removed. The rebuild re-reads every observed attribute on change (`embed-element.ts` `attributeChangedCallback`) |
| `_index.md` (home) | Links to every builder guide, the switching page and the updating page |

Outside `content/`: `config.toml` gets `[params.embed]` (`host`, `version`); `layouts/partials/embed/loader-url.html`
builds the address from them; shortcodes `embed-code` (a code block, `LOADER_URL` in its inner text replaced),
`embed-url` and `embed-version` (inline) all go through that partial.

## Decisions

| Decision | Choice | Why |
|---|---|---|
| Snippet tag (Kyser, 2026-10-15) | `<script src="https://embed.goodshuffle.com/releases/1.0.0/loader.js"></script>`, no `type` | Ticket changed 2026-10-14: pin an exact version, no forced latest. Host and version 1.0.0 decided by Kyser. `loaderSource()` in marketplace PR #450 `release.mjs` only appends a `<link>` and a `<script>` to `<head>`, so it runs the same as a plain script or `type="module"` |
| Version in one place | `params.embed.host` and `params.embed.version` in `config.toml`, rendered by the `embed-code` / `embed-url` / `embed-version` shortcodes through one partial | Fenced code in Markdown can't read site params. A release changes `version` and nothing else |
| `/v1/` | Opt-in only, one section ("Automatic updates with v1" on `setup/updating.md`), linked from every builder guide. No page uses it as the default | Ticket: `/v1/` gets non-breaking 1.x updates; a breaking change ships as a new major with an upgrade guide. `v1Decision()` moves `/v1/` only to a newer 1.x release |
| CSS | No separate stylesheet tag. The pages say the one tag adds the styles | `loaderSource()` appends `<link rel="stylesheet">` for the release's `gspro-embed.css` before the bundle |
| Changelog link | `setup/updating.md` links the existing Changelog page, with "To be defined: where the release notes for 1.0.0 and later are published" | The Changelog page exists but stops at 0.5.8; no 1.x release-notes location has been named |
| WordPress Advanced Settings | Describe plugin 0.6.0 (PR #21): Modern JS and Legacy JS are empty unless customized, the "Your site loads" row, the three-row behavior table, the old unpkg defaults and the pinned address counting as empty, `/v1/` via Modern JS with Legacy JS empty, and upgrade behavior. Help text is quoted from `gspro-gallery-admin-display.php`. Icon URL is described as having no effect | PR #20's behavior (every field pre-filled, a saved 0.5.7 address keeps loading) no longer applies once 0.6.0 ships, and 0.6.0 is the version the guide tells vendors to install |
| WordPress addresses written out | The WordPress pages write `https://embed.goodshuffle.com/releases/1.0.0/loader.js` literally, outside the `embed-*` shortcodes | The plugin pins its own address in `GSPRO_GALLERY_WIDGET_LOADER_URL`. If `params.embed.version` moves first, the plugin still loads 1.0.0 until a new plugin release, so the WordPress page has to name the plugin's version |
| Loader wording | Every page says the tag adds `gspro-embed.css` and `gspro-embed.js` from the same release folder to `<head>`. Where it matters (custom setup, Wix, updating, the troubleshooting table) it says the first copy on a page decides the release, and that the loader doesn't detect the 0.5.x `gspro-wc` scripts | `loaderSource()` returns early only if `script[data-gspro-embed]` or `script[src$="/gspro-embed.js"]` is already on the page. `/v1/loader.js` is the newest 1.x release's loader, cached 5 minutes (`ALIAS_CACHE`) |
| Menu order | Setup pages in steps of 10, matching the other sections: Squarespace 10, WordPress 20, Wix 30, Showit 40, GoHighLevel 50, Lovable 60, Custom 70, Switching 80, Updating 90 | Same order as the Getting Started table and the home page. Weebly stays hidden at 10. The empty `setup/getting-started.md` stub gets `bookHidden: true` so the menu doesn't show a blank second "Getting Started" |
| Builder guide wording | Squarespace, Showit, GoHighLevel, Lovable, Weebly and Wix say "Goodshuffle's script" and "the version". The precise terms (loader, release folder, `gspro-embed.css` / `.js`) stay on `custom-setup.md` and `updating.md` | Vendors on a builder don't need the mechanism to follow the steps |
| Language on Wishlist Config | "Ask Goodshuffle to turn it on" in place of the `multiLanguageEnabled` flag name | It's a vendor feature flag (`VendorFeatureFlags.multiLanguageEnabled` in gscore); the goodshuffle app only reads it, so a vendor can't set it themselves |
| Wishlists carry over | Kept on "Switching from 0.5.x", worded as what the code does | `migrateLegacy()` in GSPRO-31870's `storage.ts` (see Sources). It ships before these docs publish, because GSPRO-32329, which these docs wait on, contains it |
| Events (Kyser, 2026-10-08) | The docs describe the restored events: every 0.5.11 event, with 0.5.11's full `detail`, including whole items in `detail.wishlist`. The pages state them as available and publish after GSPRO-32329. "Switching from 0.5.x" says replace the two script tags and nothing else changes | GSPRO-32329 restores what the rebuild had dropped. The one approved difference stays documented: `gspro-wishlist.submit` fires once per send (GSPRO-31871) |
| Monitoring (Kyser, 2026-10-08) | "To be decided", with no ticket key | Where the adoption view and error alert are built is undecided. The earlier ticket for it was deleted on purpose and isn't cited |
| Attributes the widget sets or ignores | Listed, marked "set by the widget" or "accepted, no effect" | The ticket asks for every attribute. `hide-quantity` and `total` are parsed but never read in `src/embed/app`. The card's `route` and the gallery's and list's `item-card-route` are passed along but never read: `itemLink()` in `card.tsx` always builds `#!/item/{id}/{slug}`. The list's `filters` is never set by the gallery (`catalog-results.tsx` passes only `item-card-route`), and a string attribute is never a valid filter object, so `catalogView()` treats it as null. `package-quantity` does work: `card.tsx` passes it to `quantityText()`, which shows it in place of the available quantity when `show-quantity-on-card` is on |
| Events `detail` example | A `DAILY` entry with no `hours` | `hours` is set only for `HOURLY` items: `gspro-item-choices` in 0.5.11, `withRate()` and `withDefaults()` in `app/wishlist/entry.ts` in the rebuild |
| When a gallery loads items | Only with `category`, `group`, `search`, `tags` or `scope-category`/`-group`/`-search`/`-tags` | `shouldLoad('gallery')` in `catalog/query.ts`. The `scope-attribute-#` pair narrows a load but doesn't start one |
| Boolean attributes | Documented: only the lowercase string `false` turns one off | `parseAttribute` in `attributes.ts`. Wix's help article sets `require-phone-number` to `True`, which works; `False` would also turn it on |
| Builder preview addresses | Every guide says to test on the published domain; the preview may stay empty | The only source for the deployed origin allowlist (wwi skill section 7) names `wixstudio.io` and `wix-development-sites.org`; nothing shows the classic Wix Editor preview host, or Showit's, GoHighLevel's or Lovable's, is allowed |
| Old version markers | "added in v0.5.x" markers and the listeners page's "0.5.3 or greater" removed | They describe 0.5.x history, not the release a vendor runs. The only version the setup pages name is the pinned one, from `params.embed.version`. `switching-from-0-5.md` and the WordPress download history still name 0.5.x, because they are about leaving it |
| Shortcodes | `relref` and `raw-html`, which existing pages use, plus this repo's own `embed-code`, `embed-url` and `embed-version` | The `book` theme submodule isn't checked out here and Hugo isn't installed, so the theme's `hint` and friends can't be checked. The new shortcodes use only Hugo built-ins available in 0.62.1 (`partial` with `return`, `replace`, `trim`, `highlight`, `default`, `errorf`) |
| One set of event dates (GSPRO-32177) | Not documented | Not built on the branch the docs are written from |
| Weebly | Kept hidden (`bookHidden: true`), snippet updated | It isn't one of the six supported builders; the page still exists for vendors who have it bookmarked |
| Showit, GoHighLevel, Lovable editor steps | Described by the builder's element and setting names, plus what the code needs | Builder menus move; the code placement (head vs. page body) is what the host-page tests (GSPRO-31877) prove |

## Open before this ships

### Events wait on GSPRO-32329

Settled by Kyser on 2026-10-08: GSPRO-32329 restores every 0.5.11 event with its full `detail`.
`events.md` and `switching-from-0-5.md` describe that behavior as available, with no ticket
reference, because a vendor can't act on one. They're accurate once GSPRO-32329 merges, so this
branch publishes after it.

### Acceptance criteria not met

- **AC1: following each guide on a fresh site produces a working catalog and a quote request in
  GSP.** Not done. Every snippet loads `https://embed.goodshuffle.com/releases/1.0.0/loader.js`,
  which exists only once GSPRO-31872 publishes release 1.0.0. `requireParityGate()` in
  `release.mjs` allows a 1.x release once `PARITY_GATED=true`; marketplace #452 sets it, behind the
  browser gates, so 1.0.0 can publish once those gates pass.
- **AC2: CX has reviewed each guide against the top HubSpot questions.** Not done, for the same
  reason: CX can't check a guide whose snippet doesn't load yet.
- **AC3: every snippet pins the same current version, set in one place.** Met in the source:
  `params.embed.version` in `config.toml`, read by every snippet through the `embed-*` shortcodes.
  Not confirmed in a build (see below).

AC1 and AC2 stay open until 1.0.0 is live on `embed.goodshuffle.com`, each guide has been walked
end to end on all six builders, and CX signs off. This branch can't close them. Its PR is a draft
and says so.

## Not done here

- Publishing. `master` and `preview` deploy publicly; this branch goes up as a draft PR and nothing
  merges until release 1.0.0 is live at the pinned address.
- Building the site. Hugo isn't installed and isn't to be installed here, so the pages were checked
  by reading the front matter and shortcodes of existing pages, and the new shortcodes against Hugo
  0.62.1's template functions, not by a build. The `embed-*` shortcodes have never been rendered.
- AC1 and AC2, above.

## Placeholders

Hosting was decided on 2026-10-15 (host `embed.goodshuffle.com`, pinned 1.0.0, one-tag loader), so
the `EMBED_HOST` placeholders and every "To be filled in when GSPRO-31872 ships" note are gone.
These are what's left, each marked in the page:

- **The WordPress plugin 0.6.0 download link and date** (`setup/wordpress.md` Requirements,
  `resources/wordpress.md` Current Version). "To be filled in when plugin 0.6.0 is released
  (GSPRO-32532)". The version (0.6.0) and the widget it pins (1.0.0) come from PR #21 and are
  written in. PR #21 leaves the zip and upload until widget 1.0.0 is live.
- **Where release notes for 1.0.0 and later are published** (`setup/updating.md`). "To be
  defined". The page links the existing Changelog, which stops at 0.5.8.
- **How support confirms which version a vendor's site runs** (`switching-from-0-5.md`). To be
  decided, along with where the adoption view and error alert are built. No ticket yet.

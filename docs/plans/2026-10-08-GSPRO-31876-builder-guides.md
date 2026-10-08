# GSPRO-31876: Setup guide for each site builder

Epic GSPRO-31790 (Website Integration Rebuild). Repo `goodshuffle-developer-site` (Hugo, `book`
theme, Netlify). The branch is `kyser/GSPRO-31876/builder-guides`, cut from the feature branch
`kyser/GSPRO-31790/website-integration-rebuild`, which was cut from `origin/master` on 2026-10-08.
The repo had no `docs/plans/` folder; this file starts it. It sits outside `content/`, so Hugo
doesn't publish it.

## Goal

A vendor on Squarespace, WordPress, Wix, Showit, GoHighLevel or Lovable can follow one page and end
up with a working catalog and a quote request that lands in Goodshuffle Pro. Every snippet uses the
unversioned `/v1/` address. The reference pages list every attribute with the default the rebuilt
widget actually uses, and the Events page gives the exact `detail` of the two submit events.

## Sources

| Source | Used for |
|---|---|
| Requirements 4130111489, "Vendors follow a setup guide for their site builder" | The six builders, the new script address |
| Solution Architecture 4130471937, Migration and compatibility | What each kind of vendor changes when switching |
| Hosting proposal 4140761090 (draft) | The loader is one plain script that adds the release's JS and CSS; numbered releases stay published. All of it is still NEED CONFIRMATION |
| `wwi` skill (agent-rules PR #53) section 5 and `references/help-articles.md` | Activation, key, the platform quirks the help center covers |
| marketplace `kyser/GSPRO-32057/legacy-elements` | `src/main/react-client/src/embed/elements/attributes.ts` (every attribute and default), `app/settings.ts` (config fallbacks), `app/wishlist/send.ts`, `payload.ts` and `entry.ts` (events and entry shape), `app/catalog/query.ts` (what loads when), plan `2026-10-03-GSPRO-31877-host-page-tests.md` (where each builder takes the snippet) |
| wp-gspro-gallery PR #20 (head `1737a52`) | Settings page labels, shortcodes, Advanced Settings built-in addresses (`admin-display.php`), what is held for GSPRO-31872 |
| `wir-testing-findings.md` | Real failure modes: origin check, key rotation, boolean parsing |
| Git history of `content/docs/setup/showit.md` (removed in 860c083) | Showit editor steps |

## Pages

| Path (`content/docs/`) | Change |
|---|---|
| `setup/_index.md` | Lists the six builders, the shared snippet and the placeholder note |
| `setup/switching-from-0-5.md` | New. Replace the two script tags with one; what stays; what is different |
| `setup/squarespace.md` | Rewritten on the `/v1/` snippet |
| `setup/wordpress.md` | Rewritten to match wp-gspro-gallery PR #20: settings page, gallery page, shortcodes |
| `setup/wix.md` | Rewritten. The Custom Element's Server URL is the loader; no `custom-elements/index.js` |
| `setup/showit.md` | Restored (it was emptied in 860c083) on the `/v1/` snippet |
| `setup/gohighlevel.md` | New |
| `setup/lovable.md` | New |
| `setup/weebly.md`, `setup/custom-setup.md` | Same pages, `/v1/` snippet, current Integrations link, gallery behavior stated correctly |
| `components/*.md` | An "All attributes" table per tag from `attributes.ts`; Wishlist Config's wrong `# Item List` heading fixed; "added in v0.5.x" markers removed |
| `integrations/events.md` | `gspro-wishlist.submit` and `submit-complete` with their exact `detail`; the 0.5.x item events marked as not fired by the rebuild |
| `integrations/listeners.md` | The "requires 0.5.3 or greater" line removed. The rebuild re-reads every observed attribute on change (`embed-element.ts` `attributeChangedCallback`) |
| `_index.md` (home) | Links to every builder guide and the switching page |

## Decisions

| Decision | Choice | Why |
|---|---|---|
| Snippet tag | `<script src="https://EMBED_HOST/v1/loader.js"></script>`, no `type` | GSPRO-31872's acceptance asks for the loader to work as a plain script and as a module. The loader doesn't exist yet, so the pages don't state it as fact; it's a placeholder until GSPRO-31872 ships |
| CSS | No separate stylesheet tag in the snippet. Every page's placeholder note says whether the tag adds the styles is to be filled in when GSPRO-31872 ships | The draft hosting proposal has the loader adding the release's JS and CSS, still NEED CONFIRMATION. The bundle doesn't add its CSS by itself: `place-stylesheet.ts` only moves a `<link>` that is already on the page. So no page presents the one-tag snippet as final |
| WordPress Advanced Settings | List each field's built-in address and how to reset it | Every field is pre-filled with its default (`get_option(..., $default)`), so "leave it empty" can't be followed. Clearing a field and saving deletes the option. 0.5.7 behaved the same, so a vendor who ever saved that form has the 0.5.7 address stored, and it keeps loading after the update |
| "Switching from 0.5.x" | Says what changes beyond the script tag. **Open: needs a recorded decision before this ships** (see below) | The rebuild doesn't fire `gspro-item-card.click`, `gspro-item-card.add` or `gspro-item-detail.add` (`card.tsx` header, `store.ts` header); `detail.wishlist` holds slim entries instead of whole items (`payload.ts eventDetail`); `gspro-wishlist.submit` fires once per send. A guide that hides this breaks vendors' analytics silently |
| Attributes the widget sets or ignores | Listed, marked "set by the widget" or "accepted, no effect" | The ticket asks for every attribute. `hide-quantity` and `total` are parsed but never read in `src/embed/app`. The card's `route` and the gallery's and list's `item-card-route` are passed along but never read: `itemLink()` in `card.tsx` always builds `#!/item/{id}/{slug}`. The list's `filters` is never set by the gallery (`catalog-results.tsx` passes only `item-card-route`), and a string attribute is never a valid filter object, so `catalogView()` treats it as null. `package-quantity` does work: `card.tsx` passes it to `quantityText()`, which shows it in place of the available quantity when `show-quantity-on-card` is on |
| Events `detail` example | A `DAILY` entry with no `hours` | `withRate()` in `app/wishlist/entry.ts` drops `hours` for any non-`HOURLY` rate, and `withDefaults()` adds it only for `HOURLY` |
| When a gallery loads items | Only with `category`, `group`, `search`, `tags` or `scope-category`/`-group`/`-search`/`-tags` | `shouldLoad('gallery')` in `catalog/query.ts`. The `scope-attribute-#` pair narrows a load but doesn't start one |
| Boolean attributes | Documented: only the lowercase string `false` turns one off | `parseAttribute` in `attributes.ts`. Wix's help article sets `require-phone-number` to `True`, which works; `False` would also turn it on |
| Builder preview addresses | Every guide says to test on the published domain; the preview may stay empty | The only source for the deployed origin allowlist (wwi skill section 7) names `wixstudio.io` and `wix-development-sites.org`; nothing shows the classic Wix Editor preview host, or Showit's, GoHighLevel's or Lovable's, is allowed |
| No pinned versions on pages | "added in v0.5.x" markers and the listeners page's "0.5.3 or greater" removed | The ticket: "No page names a pinned version". `switching-from-0-5.md` and the WordPress download history still name 0.5.x, because they are about leaving it |
| Shortcodes | Only `relref` and `raw-html`, which existing pages use | The `book` theme submodule isn't checked out here and Hugo isn't installed, so `hint` and friends can't be checked |
| One set of event dates (GSPRO-32177) | Not documented | Not built on the branch the docs are written from |
| Weebly | Kept hidden (`bookHidden: true`), snippet updated | It isn't one of the six supported builders; the page still exists for vendors who have it bookmarked |
| Showit, GoHighLevel, Lovable editor steps | Described by the builder's element and setting names, plus what the code needs | Builder menus move; the code placement (head vs. page body) is what the host-page tests (GSPRO-31877) prove |

## Open before this ships

### Switching from 0.5.x: the docs and the Requirements disagree

The ticket says the Switching page is "replace the two script tags, nothing else changes".
Requirements (Proposed New) say "existing pages, settings tag, options, events, and style classes
work unchanged after the switch". The rebuild doesn't meet that, and the pages say so, following
the code:

- `gspro-item-card.click`, `gspro-item-card.add` and `gspro-item-detail.add` no longer fire.
- Each `detail.wishlist` entry is slim (the fields in the Events table), not the whole item.
- `gspro-wishlist.submit` fires once per send; a second click during a send doesn't fire it again.

Before this branch merges, one of these has to happen on the record:

- Requirements and the ticket are updated to say these three things change, or
- the regression is accepted in Requirements' Intentional Regressions, or
- the rebuild brings the three events and full entries back, and `switching-from-0-5.md` and
  `events.md` drop the "what is different" sections.

Until then, `switching-from-0-5.md` and `events.md` describe the code as built.

### Acceptance criteria not met

- **AC1: following each guide on a fresh site produces a working catalog and a quote request in
  GSP.** Not done. Every snippet loads `https://EMBED_HOST/v1/loader.js`, which loads nothing
  until GSPRO-31872 ships. GSPRO-31872 is still Requirements Needed and blocked on the hosting
  decision.
- **AC2: CX has reviewed each guide against the top HubSpot questions.** Not done, for the same
  reason: CX can't check a guide whose snippet doesn't load.

Both stay open until GSPRO-31872 lands, each guide has been walked end to end on all six builders,
and CX signs off. This branch can't close them.

## Not done here

- Publishing. `master` and `preview` deploy publicly; this branch is not pushed and nothing merges
  until GSPRO-31872 replaces `EMBED_HOST`.
- Building the site. Hugo isn't installed and isn't to be installed here, so the pages were checked
  by reading the front matter and shortcodes of existing pages, not by a build.
- AC1 and AC2, above.

## Placeholders

Nothing about hosting or monitoring is decided yet, so those facts are placeholders, each marked
in the page as "To be filled in when GSPRO-31872 ships" (or GSPRO-32235). This is every one:

- **The script host.** Every snippet uses `https://EMBED_HOST/v1/loader.js`, with a "Placeholder
  address" note: `setup/_index.md`, `custom-setup.md`, `squarespace.md`, `wix.md` (as the Server
  URL), `showit.md`, `gohighlevel.md`, `lovable.md`, `weebly.md`, `switching-from-0-5.md`.
  `setup/wordpress.md` has no snippet; the plugin loads the script.
- **Whether the tag adds the styles itself or needs a stylesheet tag.** In the same "Placeholder
  address" note on `setup/_index.md`, `squarespace.md`, `wix.md`, `showit.md`, `gohighlevel.md`,
  `lovable.md`, `weebly.md`; in its own note on `custom-setup.md`; in the script-tag row of
  `switching-from-0-5.md`.
- **Whether the loader works both with and without `type="module"`** (`custom-setup.md`).
- **Pinning a numbered release, and switching back to `/v1/`** (`switching-from-0-5.md`).
- **The WordPress plugin version and download link** (`setup/wordpress.md` Requirements,
  `resources/wordpress.md` Current Version). GSPRO-31875's release waits on GSPRO-31872.
- **The WordPress plugin's built-in Modern JS and Legacy JS addresses** (`setup/wordpress.md`,
  Every setting). PR #20 still defaults to the 0.5.7 `unpkg.com` addresses, with a
  `TODO(GSPRO-31872)` to switch them to `/v1/loader.js`.
- **How support confirms which version a vendor's site runs** (`switching-from-0-5.md`,
  GSPRO-32235).

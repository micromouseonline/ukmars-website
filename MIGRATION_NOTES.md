# WordPress -> Hugo migration notes (2026-11-10)

## Sources
- `../export/` (wordpress-to-hugo-exporter): unchanged. Used for images and 4 unpublished items only.
- Live REST API (`/wp-json/wp/v2/pages|posts|categories|tags`): used for body HTML, page hierarchy, titles, dates.

## Exporter problems found
- All 42 YouTube embeds dropped (empty wrappers). Recovered from API.
- Two duplicate slugs (`drag-race`, `line-follower`) collapsed: one of each page lost. Recovered from API.
- Page hierarchy lost (flat `slug/index.md`); 77 of 105 pages are nested on live site. Rebuilt.
- Bodies mostly raw WP/plugin HTML (ez-toc, Kadence, Stackable, Spectra). Converted to markdown.
- Theme junk in front matter (`ocean_*`, `stackable_*`). Dropped.
- Events Manager events (`/events/...`) not exported at all.

## Output layout
- `content/<live path>/index.md`; pages with child pages are `_index.md`.
- `content/posts/<year>-<slug>.md`, explicit `url:` = live permalink (`/YYYY/MM/slug/`).
- `content/posts/draft-*`: 2 posts not published on live site (`draft: true`).
- `static/ukmars/wp-content/uploads/<year>/`: images, same URLs as live. Plugin junk dirs not copied.
- `content/events/<slug>/index.md`: 66 Events Manager events, from event page HTML + per-event iCal (`/events/<slug>/ical/`). Front matter: event_start, event_end (Europe/London local), location, event_categories. Category pages at `/events/categories/<slug>/` (taxonomy `event_categories`). `buildFuture: true` so upcoming events build.
- Removed: authors-guide section, placeholder-images draft, gutenberg-editor draft post.
- Front matter: title, date, lastmod, weight (WP menu_order), wp_id, categories/tags.
- Heading anchors kept as `{#Old_Id}` so old `#anchor` links work.
- Videos: `{{< youtube ID >}}`. Captioned images: `{{< figure >}}`.

## Verified
- Hugo 0.92 builds (with throwaway layouts), exit 0.
- All 159 live page/post URLs and all 66 event URLs (event sitemap) produce a page at the same path.
- 16 links to old/moved page paths rewritten.

## Outstanding
- Broken links: `/events/techfest/` in past-events-old (404 on live too), `/322eccf2-...` (draft post).
- Raw HTML left (complex tables, cookie policy, Google Maps iframe): `gemini-parts-and-materials`, `cookie-policy`, `platformio-vscode-windows`, `megacon`, `past-events-old`. Needs `unsafe: true` (set).
- WP page `/tags/` and `/categories/` collide with Hugo taxonomy URLs (their content becomes taxonomy list page content).
- Some stackable/kadence "headings" became plain paragraphs (e.g. "The Maze" on micromouse page).
- `events-page`, `past-events`, `events-calendar`, `calendar` are static snapshots of plugin-generated lists; should become Hugo list templates.
- Event location pages (`/locations/<venue>/`) not converted; location kept as text on each event.
- No theme, menus, or homepage layout yet. Menus not readable via API (auth needed).
- Featured images not carried over.

## Hextra copy (site-hextra/)
- Theme: `themes/hextra`, git clone of tag v0.13.0. Needs Hugo extended >= 0.146 (tested 0.169.0).
- Config: `hugo.yaml` (replaces config.yaml). Menu = live menu + News (/blog/) + Search.
- Sidebar (`type: docs` cascade): contests, projects, resources, regular-events, gemini-operating-guide, gemini-circuit-diagrams, gemini-developer-notes.
- News: `content/posts/_index.md` served at `/blog/`, `type: blog`. Old placeholder `/blog/` page removed.
- Events: `layouts/events/{list,single}.html`, partials `event-list.html`, `event-details.html`, shortcode `{{< event-list scope="upcoming|past|all" category="..." limit="N" >}}`.
  events-page, past-events, calendar, events-calendar now use the shortcode (live, not snapshots).
- Branding: logo + favicon from old uploads; `i18n/en.yaml` copyright; `assets/css/custom.css` event styles.
- `static/` is hard-linked to `../site/static` (no extra disk use).

## GitHub (site-hextra = repo micromouseonline/ukmars-website)
- static/ pruned to the 404 files referenced by content (77 MB). Full uploads remain in ../export/ and ../site/static/.
- Videos removed (too large for GitHub): `2022/09/TechFest-2019-with-Logo.mp4` (196 MB, linked from 4 events),
  `2022/04/chrisMinos.mp4` (78 MB, posts/2022-minos-2022-presentations.md). TODO: upload to YouTube, replace links with `{{< youtube ID >}}`.
- `layouts/_shortcodes/figure.html` overrides Hugo's figure so root paths work under a sub-path baseURL.
- Preview mode: `params.preview: true` + `cascade: noindex` in hugo.yaml.
- Cutover TODO: DNS for ukmars.org -> GitHub Pages, set custom domain in repo Pages settings, remove preview settings.

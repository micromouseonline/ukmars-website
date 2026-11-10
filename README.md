# UKMARS website

Hugo site for ukmars.org (UK Micromouse and Robotics Society), using the
[Hextra](https://github.com/imfing/hextra) theme. Migrated from WordPress; see
`MIGRATION_NOTES.md`.

## Local preview

Requires Hugo extended 0.146 or newer (CI uses 0.169.0).

    git clone --recurse-submodules https://github.com/micromouseonline/ukmars-website.git
    cd ukmars-website
    hugo server

Open http://localhost:1313/. Pages reload on save.

## Layout

- `content/` pages, `content/posts/` news (served at `/blog/`), `content/events/` events.
- `static/ukmars/wp-content/uploads/` images and files, same URLs as the old site.
- `layouts/` site templates and shortcodes (events, figure, latest posts).
- `themes/hextra` theme, git submodule pinned to a release tag.

## Events

One folder per event: `content/events/<slug>/index.md` with front matter

    title: 2027 Main Contest
    date: '2027-03-20T10:00:00'
    event_start: '2027-03-20T10:00:00'   # UK local time
    event_end: '2027-03-20T16:00:00'
    location: Venue, address
    event_categories: [Public Events]

Lists update automatically. Shortcode: `{{< event-list scope="upcoming|past|all" limit="5" >}}`.

## Deploy

Every push to `main` builds and deploys to GitHub Pages
(`.github/workflows/hugo.yaml`). Preview: https://micromouseonline.github.io/ukmars-website/

The site is in preview mode (no search engine indexing): see `params.preview`
and the `cascade` block in `hugo.yaml`.

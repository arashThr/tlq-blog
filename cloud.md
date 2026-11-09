# TLQ theme

Notes for how this weblog is built. Change a setting in the one place named here, then reuse it. Do not copy the value into another template.

## Layout

The page is a warm desk. The left column is the sheet. The right column is the shelf.

- Home lists recent notes, newest first. It does not print a whole note.
- A note’s own page prints the full note, with its picture or the colored plate.
- Archive stays a dated list of the notes section (`params.section`, `/blog` on this site). Tag pages use that same list.
- The right column keeps About, the menu, On the shelf, and, when configured, Elsewhere and The show.

Mainroad (https://hugothemes.gitlab.io/mainroad/) is the reference for the home list only: title, date, a short excerpt, and a link to the note. The desk, the colors, and the right-hand column stay as they are.

## Where to change behavior

Edit the site `hugo.toml` under `[params]`. If a key is missing there, `themes/tlq/hugo.toml` supplies it. Templates do not read these keys themselves. They call `layouts/_partials/config.html`, which resolves one set of values.

| Key | What it does |
| --- | --- |
| `tagline` | Line under the wordmark, and the footer |
| `description` | Line under the tagline, and the home page’s meta description |
| `about` | About panel. Markdown is fine |
| `byline` | Footer name. Blank uses the site title |
| `podcast_url` | Shows The show panel when set |
| `podcast_label` | Label on that panel |
| `links` | Elsewhere panel. Each entry needs `name` and `url` |
| `fonts_url` | Stylesheet for the families named in CSS |
| `home_paginate` | Notes on the home page before it adds newer/older pages |
| `archive_paginate` | Notes on an archive or tag page before it pages |
| `recent_count` | Titles in On the shelf |
| `excerpt_words` | Words kept from a note that has no description |
| `section` | Content folder treated as notes, for example `blog` |

A note’s `description` in front matter becomes its home excerpt. With no description, the excerpt is the opening paragraph (the next one too, if the first is very short), cut at `excerpt_words`.

If `image`, `featured_image`, or `cover` points at a file under `static/` that is not there yet, the note page uses the colored plate and the home list skips the picture.

## Where to change the look

Edit the `:root` block at the top of `themes/tlq/assets/css/main.css`. Every other rule uses `var(--…)`. Recoloring the desk, the plate, the tags, or the sidebar tints happens in that block.

Two cousins of that palette are not CSS variables:

- `theme-color` in `layouts/_partials/head.html` should stay the same hex as `--wash`.
- `themes/tlq/static/favicon.svg` is its own drawing.

`--serif` and `--sans` name the fonts. `fonts_url` has to load those same families.

## Templates

Hugo 0.146 or newer. `layouts/baseof.html` wraps every page. Kind templates only define `main`. Partials live in `layouts/_partials/`.

Home is `layouts/home.html`. Each row is `layouts/_partials/note-card.html`. The full note is `layouts/_partials/post.html`.

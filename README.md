# Gallery & Lightbox — a standalone Hugo component

A responsive image gallery for Hugo page bundles, with an optional
lightbox. Works as a **grid** (thumbnails that open full-size in a
lightbox) or a **carousel** (Swiper-powered slider, with or without the
lightbox on click). Not tied to any particular theme or content type —
drop it into any Hugo site with page-bundle images.

Originally extracted from the [Apartments Hugo theme](https://propertysuitehq.com/themes/apartments),
where it powers floorplan and photo galleries — but there's nothing
apartment-specific about it.

## Install

1. Copy `layouts/_partials/gallery.html` and `layouts/shortcodes/gallery.html`
   into your site's own `layouts/` folder (or your theme's, if you're
   building one).
2. Copy `static/css/gallery.css` into your site's `static/css/`, and add
   `<link rel="stylesheet" href="/css/gallery.css">` to your `<head>`.
3. Add the Fancybox (and, if you want carousels, Swiper) CDN tags from
   `layouts/_partials/assets.html` to your site's head/footer partials —
   that file is documentation, not something you call with `partial`.

## Usage

### From a template (e.g. a `single.html` layout)

```go-html-template
{{ partial "gallery.html" (dict
  "images" .Params.gallery
  "page" .
  "layout" "grid"
  "columns" 3
) }}
```

Where a page's front matter has something like:

```yaml
gallery:
  - filename: "living-room.jpg"
    caption: "Living room"
    alt: "Living room with large window"
  - filename: "kitchen.jpg"
    caption: "Kitchen"
    alt: "Kitchen with island"
```

...and `living-room.jpg` / `kitchen.jpg` live alongside that page's
`index.md` as a Hugo page bundle.

### From Markdown content, via the shortcode

```md
{{</* gallery layout="carousel" columns="3" */>}}
- filename: living-room.jpg
  caption: "Living room"
  alt: "Living room with large window"
- filename: kitchen.jpg
  caption: "Kitchen"
  alt: "Kitchen with island"
{{</* /gallery */>}}
```

## Params

| Param | Default | Notes |
|---|---|---|
| `images` | — (required) | List of `{filename, caption, alt}` |
| `page` | — (required) | Pass `.` (or `.Page` in a partial call) |
| `resources` | `page.Resources` | Override if images live elsewhere |
| `layout` | `"grid"` | `"grid"` or `"carousel"` |
| `columns` | `3` | Desktop column/slide count |
| `thumbWidth` | `260` | Grid thumbnail width in px |
| `disableLightbox` | `false` | Set `true` to skip the lightbox entirely |
| `groupID` | slug of page title | Keeps multiple galleries on one page from cross-cycling in the lightbox |

## Requirements

- Hugo (any recent version — no Extended/Sass required, plain CSS)
- Fancybox (via CDN, see `assets.html`) for the lightbox
- Swiper (via CDN, see `assets.html`) — only if you use `layout="carousel"`

## License

MIT — see `LICENSE`.

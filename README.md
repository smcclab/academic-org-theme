# academic-org-theme

This is a Jekyll Theme for creating website for academic conferences, groups, and organisations. Having an advanced blog layout page, a complicated landing page, or providing lots of "profile"-style social media links is less important than providing clear and consistent pages.

This theme started out from a basic theme I developed for [my homepage](https://charlesmartin.au), and then for the [NIME community](https://nime.org).

## Installation

Add this line to your Jekyll site's `Gemfile`:

```ruby
gem "academic-org-theme"
```

And add this line to your Jekyll site's `_config.yml`:

```yaml
theme: academic-org-theme
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install academic-org-theme

## Usage

The theme ships with a small set of layouts, a navigation-driven top bar, and a data-pipeline that generates one page per row in `_data/proceedings.csv` and `_data/sessions.yml`. Most consuming sites can get started by setting a handful of config keys and adding Markdown pages that use `layout: page`.

### Required config

A minimal `_config.yml` for a theme consumer looks like this:

```yaml
title: My Conference 2026
tagline: A short subtitle shown under the site title.
description: >-
  Longer description used by jekyll-seo-tag for meta tags and feeds.
url: "https://example.org"
baseurl: ""

logo: /assets/logo.svg      # shown in the top-left of the nav
favicon: /assets/logo.svg
footer_copyright: My Conference

plugins:
  - jekyll-datapage-generator
  - jekyll-seo-tag

navigation_header:
  - title: Home
    url: /
  - title: Call
    url: /call/
  - title: Program
    url: /program/
  - title: Committee
    url: /committee/
```

Adding a page does **not** add it to the nav — update `navigation_header` too.

### Layouts

| Layout | When to use |
| --- | --- |
| `page` | Standard content page with optional feature image. Wraps `default`. |
| `post` | Blog-style post with title/date. Wraps `default`. |
| `default` | Raw outer shell (nav + footer + scripts). Use when you need full control of the page body. |
| `proceeding_entry` | Auto-applied to each row of `_data/proceedings.csv` by the data-page generator. |
| `session_entry` | Auto-applied to each row of `_data/sessions.yml` by the data-page generator. |

Example page front matter:

```yaml
---
title: Call for Papers
layout: page
feature_image: assets/hero.jpg
# Or, for a dark-mode aware hero:
# feature_image_light: assets/hero-light.jpg
# feature_image_dark: assets/hero-dark.jpg
---
```

### Data-driven pages: proceedings and sessions

The theme's headline feature is automatic generation of one page per paper and one page per session, with cross-links between them. This is driven by `jekyll-datapage-generator` and configured under `page_gen:` in `_config.yml` (see the demo config in this repo for the canonical setup).

- **`_data/proceedings.csv`** → `/proceedings/<id>.html`. Columns include `id`, `title`, `authors`, `abstract`, `session_code`, `session_position`, `paper_url`, `video_url`, `slides_url`, `image_url`, `type`, `format`, `duration`, `presence`, `speaker`, `location`.
- **`_data/sessions.yml`** → `/sessions/<id>.html`. Keys include `id`, `title`, `subtitle`, `chair`, `date`, `start`, `end`, `location`, `type`, `allDay`.

A paper is linked to a session by matching `session_code` against a session's `id`. `session_code` may be a comma-separated list, so a single paper/artwork can appear in multiple sessions. Within a session, entries are ordered by `session_position`.

To link between generated pages from a template, use the `datapage_url` filter:

```liquid
<a href="{{ entry.id | datapage_url: 'sessions' | relative_url }}">{{ entry.title }}</a>
```

The string argument (`"sessions"` or `"proceedings"`) must match the `data:` key under `page_gen:`.

### Program page

`program.md` in this repo renders a FullCalendar view by `jsonify`-ing `site.data.sessions` and injecting a `url` for each generated session page. Copy it into your consuming site as a starting point if you want the same calendar.

### Committee page

`_data/committee.yml` is a flat list of `{name, aff, im, role, url}` entries. `committee.md` iterates it to render a cards grid.

### Feature images and dark mode

`feature_image` renders a single hero image. For a dark-mode-aware hero, set `feature_image_light` and `feature_image_dark` instead — a small script in `_includes/scripts.html` swaps the image based on the user's system preference.

### SEO

The theme includes [`jekyll-seo-tag`](https://github.com/jekyll/jekyll-seo-tag/) for metadata in page headers. See its [usage page](https://github.com/jekyll/jekyll-seo-tag/blob/master/docs/usage.md) for the front-matter keys it consumes (`title`, `description`, `image`, `author`, and so on).

### Styling

Styles live in `assets/styles.scss` on top of Bootstrap 5.3.0-alpha2. To override theme styles in a consuming site, create your own `assets/styles.scss` with the same path — Jekyll will prefer the site's copy over the one from the gem. `_sass/` is available for partials if you want to split things up.

## External (CDN) dependencies

`_includes/head.html` loads the following stylesheets and scripts from public CDNs. If you would rather self-host (for privacy, reliability, or offline builds), download the corresponding versions and replace the `<link>` / `<script>` URLs with a `{% link assets/... %}` path.

| Dependency | Version | Source |
| --- | --- | --- |
| Font Awesome | 6.7.2 | `cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/` |
| Academicons | 1.9.4 | `cdnjs.cloudflare.com/ajax/libs/academicons/1.9.4/` |
| Bootstrap CSS | 5.3.0-alpha2 | `cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha2/` |
| lite-youtube | 1.x | `cdn.jsdelivr.net/npm/@justinribeiro/lite-youtube@1/` |

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/smcclab/academic-org-theme. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](https://www.contributor-covenant.org/) code of conduct.

## Development

To set up your environment to develop this theme, run `bundle install`.

Your theme is setup just like a normal Jekyll site! To test your theme, run `bundle exec jekyll serve` and open your browser at `http://localhost:4000`. This starts a Jekyll server using your theme. Add pages, documents, data, etc. like normal to test your theme's contents. As you make modifications to your theme and to your content, your site will regenerate and you should see the changes in the browser after a refresh, just like normal.

When your theme is released, only the files in `_layouts`, `_includes`, `_sass` and `assets` tracked with Git will be bundled.
To add a custom directory to your theme-gem, please edit the regexp in `academic-org-theme.gemspec` accordingly.

## License

The theme is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

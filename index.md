---
title: Academic Org Theme
layout: page
feature_image: assets/charles-martin-ventilation.jpg
---

**Academic Org Theme** is a Jekyll theme for academic conferences, research groups, and small organisations. It aims for clear and consistent pages over visual flourish — the design assumption is that visitors come here to find a specific paper, a session time, or a committee contact, not to scroll through marketing copy.

The site you're reading right now is a working demo of the theme, built from the same repo that publishes the gem. The **Program**, **Committee**, and per-paper pages under `/proceedings/` are generated from two data files (`_data/sessions.yml` and `_data/proceedings.csv`); no per-paper HTML is written by hand. See the [README on GitHub](https://github.com/smcclab/academic-org-theme) for the consuming-site usage guide.

## What the theme gives you

- A Bootstrap-based responsive layout with a configurable top navigation, optional feature images, and dark-mode-aware heroes.
- A data-driven pipeline that turns a CSV of papers and a YAML of sessions into cross-linked per-paper and per-session pages.
- A FullCalendar-backed program page that renders straight from your sessions data.
- A committee page that renders from a flat YAML list.
- SEO metadata via `jekyll-seo-tag`, and standard Markdown/Kramdown rendering for prose content.

## Where this came from

The theme started as a small layout for [Charles Martin's homepage](https://charlesmartin.au) and was then extended to handle the needs of the [NIME community](https://nime.org) — proceedings listings, sessions, and committee pages that multiple conference years could share. It's now packaged as a gem so other organisations can adopt the same structure without forking.

---

The sections below exist to demo the theme's Markdown rendering. They're useful if you're evaluating the typography before adopting the theme.

## Typography

This is a paragraph with **bold text**, *italicized text*, and `inline code`. You can also use ~~strikethrough~~ text.

### Unordered list

- Item 1
- Item 2
  - Subitem 2.1
  - Subitem 2.2
- Item 3

### Ordered list

1. First item
2. Second item
3. Third item
   1. Subitem 3.1
   2. Subitem 3.2

## Links

[This is a link to Google](https://www.google.com)

## Blockquotes

> This is a blockquote. It can span multiple lines and can contain other markdown elements.
>
> - Like this list item
> - And another one

## Code blocks

```python
def hello_world():
    print("Hello, world!")

hello_world()
```

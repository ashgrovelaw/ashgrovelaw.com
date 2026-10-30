# ashgrovelaw.com

The website for Ashgrove Law, an employment and small-business law firm in Columbus, Ohio.
Live at https://ashgrovelaw.com.

## Stack

- Jekyll, built by GitHub Pages (the `github-pages` gem pins the exact Jekyll and plugin
  versions GitHub uses)
- Our own layout in `_layouts/` and `_includes/`; no theme
- Plugins: `jekyll-seo-tag` (titles, descriptions, canonical URLs, Open Graph) and
  `jekyll-feed` (the Insights RSS feed). GitHub Pages only runs the plugins on its
  allow-list, so check https://pages.github.com/versions/ before adding one.
- Plain CSS in `assets/css/site.css`; SVG images in `assets/img/`

## Running it locally

You need Ruby 3.1 or newer and Bundler.

```bash
bundle install
bundle exec jekyll serve     # http://localhost:4000, rebuilds on save
```

To check a production build:

```bash
JEKYLL_ENV=production bundle exec jekyll build    # output in _site/
```

No Ruby? Docker works too:

```bash
docker run --rm -it -p 4000:4000 -v "$PWD":/site -w /site ruby:3.3 \
  sh -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"
```

## Where things live

```
_config.yml                 site title, URL, firm address/phone, plugins, permalinks
_layouts/default.html       page shell: <head>, header, footer
_layouts/page.html          standard inner page (hero + body + consultation banner)
_layouts/post.html          Insights article
_includes/head.html         meta tags, SEO tag, stylesheet
_includes/legal-service.html  LegalService structured data (reads the firm details in _config.yml)
_includes/header.html       main navigation
_includes/footer.html       footer and attorney-advertising disclaimer
index.html                  home
practice-areas/*/index.md   one page per practice area
attorneys/index.html        attorney bios (portraits in assets/img/attorneys/)
what-to-expect/index.md     consultations, fees and retainers
insights/index.html         Insights index (lists _posts automatically)
_posts/                     Insights articles
contact/index.html          address, phone, directions
CNAME                       custom domain for GitHub Pages
```

The firm's address, phone number, email and hours live once, in `_config.yml` under
`firm:`, and the footer, contact page and structured data all read them from there.

### Adding an Insights article

Create `_posts/YYYY-MM-DD-short-slug.md` with this front matter:

```yaml
---
layout: post
title: "The headline"
author: Rachel Nguyen
description: One or two sentences for search results and the Insights index.
---
```

It appears at `/insights/short-slug/`, on the Insights index, on the home page (if it is
one of the three newest) and in the feed.

### Every page needs

A `title` and a `description` in its front matter. `jekyll-seo-tag` turns them into the
`<title>` (with " | Ashgrove Law" appended) and the meta description.

### Attorney advertising

Anything describing results or fees must stay consistent with the Ohio Rules of
Professional Conduct (Rules 7.1 to 7.3). Run copy changes about fees or outcomes past
Diane before they go live.

## Deploying

GitHub Pages builds the `main` branch of `ashgrovelaw/ashgrovelaw.com` automatically
("Deploy from a branch", `main`, `/ (root)`). Every push to `main` is live in a minute or
two; there is no staging site, so preview locally first and use a pull request for
anything bigger than a typo. The custom domain comes from the `CNAME` file, and HTTPS is
enforced in the repository's Pages settings.

Questions: ask Alana.

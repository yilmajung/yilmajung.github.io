# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based academic personal website for Wooyong Jung, hosted on GitHub Pages at https://yilmajung.github.io. It uses the Journal theme and showcases research projects, blog posts, and professional information.

## Build Commands

```bash
# Install dependencies
bundle install

# Run local development server
bundle exec jekyll serve

# Build for production
bundle exec jekyll build
```

The site uses Jekyll 3.8.5 with plugins: jekyll-paginate and jekyll-sitemap.

## Architecture

### Content Collections

The site uses three Jekyll collections defined in `_config.yml`:
- **_posts/** - Blog posts with URL pattern `/blog/:slug`
- **_projects/** - Research project pages with URL pattern `/project/:slug`
- **_pages/** - Static pages (about, contact, cv) with URL pattern `/:name`

Posts and projects often have parallel content (same project in both collections with slightly different formats).

### Configuration Structure

- **_config.yml** - Jekyll configuration, collections, and permalink patterns
- **_data/settings.yml** - Site-wide settings including:
  - Navigation menu items
  - Social media links
  - Color scheme and typography settings
  - Contact form configuration (Formspree)

### Template Hierarchy

Layouts in `_layouts/`:
- `default.html` - Base template with header, footer, MathJax support
- `page.html`, `post.html`, `project.html` - Extend default for specific content types

Partials in `_includes/`:
- `header.html` - Site navigation
- `footer.html` - Footer content
- `socials.html` - Social media icon links
- `contact-form.html` - Formspree-powered contact form

### Styling

SCSS files in `_sass/` compile through `css/style.scss`. The stylesheet pulls variables from `_data/settings.yml` using Liquid templating, allowing centralized control of colors, fonts, and spacing.

### Front Matter Patterns

Blog posts and projects use:
```yaml
---
title: 'Post Title'
date: YYYY-MM-DD 00:00:00
featured_image: '/images/...'
excerpt: Brief description
---
```

Projects may include a `subtitle` field for additional context.

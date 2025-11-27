# Copilot instructions for sentongo.github.io

Role: You are an AI coding assistant (coding agent) helping maintain a small Jekyll-based personal website deployed via GitHub Pages. Focus on minimal, correct edits that respect Jekyll/Liquid conventions and the repository's structure.

Big picture
- Site type: Jekyll static site served on GitHub Pages. Source lives in the repo root; GitHub Pages builds the site from `main` automatically.
- Key files: `_config.yml` (site metadata and `permalink: /blog/:title/`), layout templates under `_layouts/`, and page content under top-level markdown files and `_posts/`.

Where to make changes
- Global markup & shell: edit `_layouts/default.html` (header, footer, site chrome) and `_layouts/_includes/head.html` (meta tags, stylesheet includes).
- Home view: update `_layouts/_includes/_layouts/home.html` (hero, recent posts loop).
- Post template: update `_layouts/_includes/_layouts/_layouts/post.html` (article structure).
- Static assets: templates reference `assets/css/style.css`, `assets/js/theme-toggle.js`, and `assets/cv/Paul_CV.pdf`. Ensure assets follow this path (create `assets/` if missing).

Templating & patterns to preserve
- Liquid: the site uses standard Liquid tags and filters (e.g., `{{ site.title }}`, `{{ content }}`, `{% for post in site.posts %}`, `| relative_url`, `| strip_html | truncate`). Preserve use of `relative_url` when generating links.
- Site variables: `site.title`, `site.author`, `site.time` and `page.*` are used throughout — prefer these over hard-coded values.
- Permalinks: rely on `_config.yml`'s `permalink: /blog/:title/` rather than changing URLs inline.

Adding content
- New pages: add top-level markdown files like `index.md`, `about.md`, `blog.md` with YAML front matter (`layout:` as needed).
- New posts: add files to `_posts/` named `YYYY-MM-DD-title.md` with front matter including `layout: post` and `title:`. The templates expect `post.excerpt` for summaries.

Local preview & build (discoverable/explicit)
- GitHub Pages will build on push — to preview locally you need Jekyll:
  - If a `Gemfile` exists: `bundle install` then `bundle exec jekyll serve --livereload`.
  - If no Ruby environment is configured, use Docker (reproducible):
    `docker run --rm -v "$PWD":/srv/jekyll -p 4000:4000 jekyll/jekyll:4 jekyll serve --watch --livereload`
- After serving, open `http://localhost:4000` to verify layout, links, and `theme-toggle.js` behavior.

Repository-specific cautions
- The repository references `assets/` paths in templates but `assets/` may not be present. If assets are missing, add them at the expected locations rather than changing template paths.
- Keep the header nav links using `{{ '/' | relative_url }}` and similar filters to preserve correct baseurl behavior.

Files to check in a PR
- `_config.yml`, `_layouts/default.html`, `_layouts/_includes/head.html`, `_layouts/_includes/_layouts/home.html`, `_layouts/_includes/_layouts/_layouts/post.html`, any new files under `assets/`, and any `_posts/*` you add.

Examples (practical snippets)
- Add a post front matter minimal example:
  ```yaml
  ---
  layout: post
  title: "My New Post"
  date: 2025-11-27 09:00:00 +0000
  ---
  ```
- Preserve link creation style when linking to the CV:
  `{{ '/assets/cv/Paul_CV.pdf' | relative_url }}`

If anything here is unclear or you want the instructions to emphasize different workflow tools (for example, using `gh-pages` branch or CI), tell me which workflows to include and I'll update this file.

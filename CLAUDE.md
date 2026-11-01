# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

- `quarto render`: build the site into `_site/`
- `quarto preview`: run the dev server with live reload

There are no tests or linters. CI runs the same render on every pull request.

## Architecture

- `_quarto.yml` holds the shared site config. `_host.yml` holds host-specific settings and is merged in through `metadata-files`. To move hosts, change `_host.yml` and `.github/workflows/publish.yml`.
- `project.render` lists what Quarto builds. It excludes `CLAUDE.md`, because Quarto would otherwise publish every markdown file in the project as a page.
- Merging to `main` publishes the site: `.github/workflows/publish.yml` renders it and deploys to GitHub Pages. Pull requests only render.
- Pages: `index.md` is About (the home page), `cv.md` is the CV, and `musings/index.md` is the blog listing.
- Each post is `musings/<slug>/index.md`, with `title` and `date` in its front matter and any images beside it. The folder name sets the URL, `/musings/<slug>/`, so don't rename a folder once it's published. The listing picks up new posts automatically and builds previews from the first paragraph, or from `description` if set. There are no categories.
- `styles.css` draws the painting and the content frame. It's plain CSS rather than SCSS so its `url()` stays relative to the file; Quarto compiles theme SCSS into `site_libs/`, which would change what that path resolves against.
- The hide-on-scroll navbar comes from `navbar: pinned: false` in `_quarto.yml` (Quarto's built-in Headroom), not custom JavaScript.

## Repository

- Remote: `origin` is https://github.com/dchristman/dchristman.github.io (public)
- Live site: https://dchristman.github.io
- Default branch: `main`

## Instructions

Never commit to main; always work on a branch named after the issue
Always run the build (and check the page in the dev server) before saying a task is done
Open a pull request that references the issue number
Explain non-obvious decisions in the pull request description
Stack: Quarto website with a blog, hosted on GitHub Pages; keep host-specific settings in one place so the site can move hosts later

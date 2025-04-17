# LYI Monolith Documentation

This directory contains the documentation files that are published to GitHub Pages.

## Contents

- `apis.md` - API endpoints documentation
- `models.md` - Database model documentation

## GitHub Pages Setup

The documentation is automatically published to GitHub Pages using GitHub Actions. The workflow is defined in `.github/workflows/github-pages.yml`.

## How to View Documentation

Once published, the documentation will be available at:

`https://[username].github.io/lyi-monolith/`

## Local Development

To preview the documentation locally, you can use Jekyll:

1. Install Ruby and Jekyll (follow instructions at https://jekyllrb.com/docs/installation/)
2. Run:
   ```
   bundle install
   bundle exec jekyll serve
   ```
3. Open your browser to `http://localhost:4000` 
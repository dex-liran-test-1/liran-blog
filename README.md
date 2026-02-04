# Liran's Blog

A personal blog built with Hugo and styled with the Terminal theme for a retro/tech aesthetic.

## 🚀 Quick Start

### Prerequisites

- [Hugo](https://gohugo.io/installation/) (Extended version recommended)
- Git

### Local Development

1. Clone the repository:
```bash
git clone https://github.com/dex-liran-test-1/liran-blog.git
cd liran-blog
```

2. Start the Hugo development server:
```bash
hugo server -D
```

3. Open your browser to `http://localhost:1313`

The site will automatically reload when you make changes to content or configuration.

## 📝 Creating Content

### New Blog Post

```bash
hugo new posts/my-post-title.md
```

This creates a new post in `content/posts/` with front matter. Edit the file to add your content.

### Front Matter Example

```yaml
---
title: "My Post Title"
date: 2024-02-04
draft: false
description: "A brief description of the post"
tags: ["tag1", "tag2"]
---
```

## 🎨 Theme

This site uses the [Terminal theme](https://github.com/panr/hugo-theme-terminal) by panr. It provides:
- Retro terminal aesthetic
- Syntax highlighting for code blocks
- Fast, lightweight design
- Dark mode by default
- Responsive layout

## ⚙️ Configuration

Site configuration is in `hugo.toml`. Key settings:

- **baseURL**: Set to your domain (currently `https://liran.blog/`)
- **title**: Site title
- **params**: Theme-specific parameters and SEO settings
- **menu**: Navigation menu items
- **markup**: Syntax highlighting configuration

## 📦 Building for Production

Build the static site:

```bash
hugo
```

This generates the site in the `public/` directory, ready to deploy.

## 🚢 Deployment Options

### Option 1: GitHub Pages

1. Enable GitHub Pages in repository settings
2. Set source to GitHub Actions
3. Add this workflow file (`.github/workflows/hugo.yml`):

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true
      - name: Build
        run: hugo --minify
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Option 2: Netlify

1. Connect your GitHub repository to Netlify
2. Build command: `hugo --minify`
3. Publish directory: `public`

### Option 3: Vercel

1. Import project from GitHub
2. Framework preset: Hugo
3. Build command: `hugo --minify`
4. Output directory: `public`

### Option 4: Self-hosted

1. Build the site: `hugo --minify`
2. Copy the `public/` directory to your web server
3. Point your web server to serve the static files

## 🔧 Customization

### Changing Theme Colors

Edit `hugo.toml`:

```toml
[params]
  themeColor = "green"  # Options: orange, red, blue, green
```

### Adding Social Links

Add to `hugo.toml`:

```toml
[[params.social]]
  name = "github"
  url = "https://github.com/yourusername"
```

### Syntax Highlighting

Syntax highlighting is pre-configured using the Monokai style. To change:

```toml
[markup.highlight]
  style = "monokai"  # Other options: dracula, nord, github, etc.
```

## 📄 License

This blog content is © Liran Cohen. The Terminal theme is MIT licensed.

## 🤝 Contributing

Found a typo or issue? Feel free to open an issue or PR!

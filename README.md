# UIX Guides Jekyll

A documentation site built with Jekyll using the beautiful [Yat theme](https://github.com/jeffreytse/jekyll-theme-yat).

## Features

- Modern responsive design with beautiful night/dark mode
- Full layouts: home, post, tags, archive and about
- Beautiful syntax highlighting
- SEO optimized
- Sitemap and RSS feed support
- Advanced markdown features with Jekyll Spaceship

## Setup

### Prerequisites

- Ruby (version 2.5 or higher)
- Bundler
- Git

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/Lint-Free-Technology/uix-guides-jekyll.git
   cd uix-guides-jekyll
   ```

2. Install dependencies:
   ```bash
   bundle install
   ```

3. Run the local server:
   ```bash
   bundle exec jekyll serve
   ```

4. Visit `http://localhost:4000` in your browser

### Deployment

This site uses GitHub Actions for automatic deployment to GitHub Pages:

- Pushes to `main` or `master` branch automatically trigger deployment
- The workflow uses [jekyll-deploy-action](https://github.com/jeffreytse/jekyll-deploy-action)
- Built site is deployed to the `gh-pages` branch
- Configure GitHub Pages in repository settings to use the `gh-pages` branch

### Theme

This site uses the [jekyll-theme-yat](https://github.com/jeffreytse/jekyll-theme-yat) theme via remote theme functionality, making it compatible with GitHub Pages.

## Customization

Edit `_config.yml` to customize:
- Site title, description, and author
- Theme colors and appearance
- Navigation and features
- Plugins and integrations

## Adding Content

- Create new posts in `_posts/` directory
- Add pages as `.md` files in the root or custom directories
- Follow Jekyll front matter format

## License

This project follows the MIT license as per the Yat theme.
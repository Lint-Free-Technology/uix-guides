# UIX Guides Jekyll

A documentation site built with Jekyll using the beautiful [Yat theme](https://github.com/jeffreytse/jekyll-theme-yat).

## Setup

### Prerequisites

- Ruby (3.4.8)
- Bundler
- Git

   *GitHub action uses Ruby 3.4.8. If you use MacOS/Linux you can use rbenv to nanage your ruby installs. Repo has `.ruby-version` file set to 3.4.8*

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

This project build CI follows the MIT license as per the [YAT theme](https://github.com/jeffreytse/jekyll-theme-yat/blob/master/LICENSE.txt).

All content contributions licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

# UIX Guides

A guides site for UI eXtension built with Jekyll using the [Yat theme](https://github.com/jeffreytse/jekyll-theme-yat).

## Setup

### Prerequisites

- Ruby (3.4.8)
- Bundler
- Git

   *GitHub action uses Ruby 3.4.8. If you use MacOS/Linux you can use rbenv to manage your ruby installs. Repo has `.ruby-version` file set to 3.4.8*

### Local Development

1. Clone the repository:

   ```bash
   git clone https://github.com/Lint-Free-Technology/uix-guides.git
   cd uix-guides
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

Manual deployment via action workflow. Te workflow uses [jekyll-deploy-action](https://github.com/jeffreytse/jekyll-deploy-action)

### Theme

This site uses the [jekyll-theme-yat](https://github.com/jeffreytse/jekyll-theme-yat) theme via remote theme functionality, making it compatible with GitHub Pages.

## Adding Content

- Create new markdown `.md` posts in `_posts/` directory in directories of main project directory. These directories become categories.
- Name markdown file `YYYY-MM-DD-<descriptive short name>.md`
- Save any images to `assets/<category>/YYYY-MM-DD-<descriptive short name>.png` and use in post from this location.
- Follow Jekyll front matter format
  - `title:`
  - `excerpt_image:` if required
  - `tags:` list

## License

This project build CI follows the MIT license as per the [YAT theme](https://github.com/jeffreytse/jekyll-theme-yat/blob/master/LICENSE.txt).

All content contributions licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

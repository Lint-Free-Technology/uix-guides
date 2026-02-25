---
title: Contributing to UI eXtension guides
tags:
  - community
---
Contribution to UI eXtension guides is most welcome. To view your edits locally you will need [ruby](https://www.ruby-lang.org/en/) as the site is built with Jekyll. If you don't have ruby then don't let that stop you from contributing. Simply follow the guide writing your post in markdown and any suggested edits will be made when you submit your pull request.

## Creating a post

Fork the repository and either work online in GitHub desktop or in your favorite development environment.

- Create new markdown `.md` posts in `_posts/` directory in directories of main project directory. These directories become categories. e.g. `elements/_posts`
- Name markdown file `YYYY-MM-DD-<descriptive short name>.md`
- Save any images to `assets/<category>/YYYY-MM-DD-<descriptive short name>.png` and use in post from this location.
- Follow Jekyll front matter format
  - `title:`
  - `excerpt_image:` if required
  - `tags:` list

Submit a PR against the `contrib` branch.

## Setup for local development

### Prerequisites

- Ruby (3.4.8)
- Bundler
- Git

   *GitHub action uses Ruby 3.4.8. If you use MacOS/Linux you can use rbenv to manage your ruby installs. Repo has `.ruby-version` file set to 3.4.8*

### Build steps

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

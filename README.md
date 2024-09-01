# Aggregated Model Descriptions


This repository, prior to the creation of the associated website, via `tree`:

```
.
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── _typos.toml
├── poetry.lock
└── pyproject.toml

1 directory, 6 files
```

The website contained within this repository was created in the following manner:

(__first__) `quarto create project blog .`, which produces:


```
.
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── _quarto.yml
├── _typos.toml
├── about.qmd
├── index.qmd
├── poetry.lock
├── posts
│   ├── _metadata.yml
│   ├── post-with-code
│   │   ├── image.jpg
│   │   └── index.qmd
│   └── welcome
│       ├── index.qmd
│       └── thumbnail.jpg
├── profile.jpg
├── pyproject.toml
└── styles.css

4 directories, 16 files
```

(__next__) Create a `404.qmd` page for pages that are not found:

```
---
title: Page Not Found
---

The page you requested cannot be found (perhaps it was moved or renamed).

You may want to try searching to find the page's new location.

The content of this `404` page is source from Quarto's suggested Page Not Found description, which can be located here (<https://quarto.org/docs/websites/website-navigation.html#pages-404>).
```

(__next__) Enter `touch .nojekyll`

(__next__) On the GitHub interface, go to `settings`, click `Actions`, click `General`, unclick the default _Read repository contents and packages permissions_ and then click _Read and write permissions_, click `Save`.

(__next__) In `./.github/workflows/` create a file called `publish.yaml` and add the following to it:

```
on:
  workflow_dispatch:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2

      - name: Render and Publish
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

(__next__) Run `quarto publish gh-pages`, which will


```
? Publish site to https://AFg6K7h4fhy2.github.io/Aggregated-Model-Descriptions/ using gh-pages? (Y/n) › Yes
Switched to a new branch 'gh-pages'
No .pre-commit-config.yaml file was found
- To temporarily silence this, run `PRE_COMMIT_ALLOW_NO_CONFIG=1 git ...`
- To permanently silence this, install pre-commit with the --allow-missing-config option
- To uninstall pre-commit run `pre-commit uninstall`
Your branch is up to date with 'origin/main'.
```

(__next__) On the GitHub interface, go into `settings`, click `Pages`, have `source` set as _Deploy from a branch_, and have `Branch` set as `main`, click `Save`.

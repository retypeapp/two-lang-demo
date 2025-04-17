# Welcome

This project demonstrates configuring multiple Retype projects and deploying to separate sub-folders within the same GitHub Pages hosted website.

See also:
  - [French](/fr/) documentation
  - [Korean](/ko/) documentation

## Workflow

The following `.github/workflows/retype-action.yml` is used:

```shell
name: Publish Retype powered website to GitHub Pages
on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  publish:
    name: Publish to retype branch

    runs-on: ubuntu-latest

    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: retypeapp/action-build@latest
        with:
            config: fr/retype.yml
            subdir: fr

      - uses: retypeapp/action-build@latest
        with:
            config: ko/retype.yml
            subdir: ko

      - uses: retypeapp/action-build@latest

      - uses: retypeapp/action-github-pages@latest
        with:
          update-branch: true
```
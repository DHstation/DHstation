name: Gerar animacao da snake

on:
  schedule:
    - cron: "0 3 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Gerar SVGs
        uses: Platane/snk@v3
        id: snake-gif
        with:
          github_user_name: DHstation
          outputs: |
            dist/snake.svg
            dist/snake-dark.svg?palette=github-dark

      - name: Publicar na branch output
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

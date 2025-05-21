name: Generate Snake

on:
  schedule:
    - cron: "0 0 * * *" # runs every day at midnight
  workflow_dispatch:

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk@master
        with:
          github_user_name: <your-github-username>
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake.gif

      - name: Push snake animation
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

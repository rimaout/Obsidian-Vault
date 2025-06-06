---
created: 2024-03-19T17:15
related:
  - "[[My Quartz Setup Process]]"
completed: 
Main Moc: "[[Tech MOC]]"
updated: 2025-04-13T15:06
---
---
>[!note] Normal Version (no [[Git Submodules]] for content)
>```yaml
>name: Deploy Quartz site to GitHub Pages
> 
>on:
>  push:
>    branches:
>      - v4
> 
>permissions:
>  contents: read
>  pages: write
>  id-token: write
> 
>concurrency:
>  group: "pages"
>  cancel-in-progress: false
> 
>jobs:
>  build:
>    runs-on: ubuntu-22.04
>    steps:
>      - uses: actions/checkout@v3
>        with:
>          fetch-depth: 0 # Fetch all history for git info
>      - uses: actions/setup-node@v3
>        with:
>          node-version: 20
>      - name: Install Dependencies
>        run: npm ci
>      - name: Build Quartz
>        run: npx quartz build
>      - name: Upload artifact
>        uses: actions/upload-pages-artifact@v2
>        with:
>          path: public
> 
>  deploy:
>    needs: build
>    environment:
>      name: github-pages
>      url: ${{ steps.deployment.outputs.page_url }}
>    runs-on: ubuntu-latest
>    steps:
>      - name: Deploy to GitHub Pages
>        id: deployment
>        uses: actions/deploy-pages@v2
>```

>[!note] Submodule Version:
>edit, replace lines 21-23 with this:
>```yaml
>      - uses: actions/checkout@v4
>        with:
>          fetch-depth: 0 # Fetch all history for git info
>          submodules: true # Fetch all submodules
>```

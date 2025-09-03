# 🚀 Docusaurus Deployment Guide (GitHub Pages)

This repository hosts a **Docusaurus static site** deployed to **GitHub Pages** at:  
👉 [https://mise-fein.github.io](https://mise-fein.github.io)

---

## 📂 Branching Strategy

Since this repo is named `mise-fein.github.io` (a **user site**), GitHub Pages requires that the **`main` branch** contains the **built static site**.

- `source` → contains the Docusaurus project (source code).  
- `main` → contains the built static site (auto-generated, do not edit manually).  

---

## ⚙️ Setup

### 1. Clone the repo
```bash
git clone https://github.com/mise-fein/mise-fein.github.io.git
cd mise-fein.github.io
```
### 2. Install dependencies
```bash
npm install
```
## 🛠 Configuration
In `docusaurus.config.js`, make sure these values are set:

```js

module.exports = {
  title: 'My Website',
  tagline: 'Documentation made easy',

  url: 'https://mise-fein.github.io', // GitHub Pages URL
  baseUrl: '/',                       // root, since this is a user site

  organizationName: 'mise-fein',      // GitHub username
  projectName: 'mise-fein.github.io', // Repo name
  deploymentBranch: 'main',           // built files go to `main`

  onBrokenLinks: 'warn',
  onBrokenMarkdownLinks: 'warn',
};
```

## 🚀 Deployment Steps
### 1. Work on source branch
Make all edits and commits on the source branch:

```bash
git checkout source
```
### 2. Build & Deploy
Run:

```bash
npm run deploy
```
This will:

`Run npm run build` (generates static files into build/).

Push the contents of build/ to the main branch.

GitHub Pages serves the site from main.

## ⚡ Scripts
In package.json:

```json

"scripts": {
  "start": "docusaurus start",
  "build": "docusaurus build",
  "serve": "docusaurus serve",
  "deploy": "cross-env GIT_USER=mise-fein docusaurus deploy"
}
```
`cross-env` ensures GIT_USER works on both Windows & Linux.

## ✅ GitHub Pages Settings
Go to Repo → Settings → Pages.

Set:

Source = Deploy from a branch

Branch = main

Folder = / (root)

Save.

Your site will be live `at https://mise-fein.github.io.`

## 🔧 Troubleshooting
Error: Please set the GIT_USER environment variable
→ Use `cross-env` in package.json or enable useSSH: true in docusaurus.config.js.

Error: Broken links found
→ Fix the links or use:

```js

onBrokenLinks: 'warn',
onBrokenMarkdownLinks: 'warn',
```
Error: You cannot deploy from this branch (main)
→ Always work on source branch. main is reserved for built files only.

## 🌟 Workflow Summary
Develop in source branch

Deploy with npm run deploy

GitHub Pages serves from main branch
### Auto Deploy
Add GitHub Actions Workflow

In your repo, create this file:

`.github/workflows/deploy.yml`

```yaml
name: Deploy Docusaurus to GitHub Pages

on:
  push:
    branches:
      - source   # 👈 Auto deploy only when pushing to source branch

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v4
        with:
          fetch-depth: 0   # full history needed for gh-pages

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18  # Docusaurus works best with Node 18

      - name: Install dependencies
        run: npm install

      - name: Build website
        run: npm run build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build
          publish_branch: main   # 👈 deploy to main branch
```

## ⚡ Step 3: Commit & Push
```bash
git add .github/workflows/deploy.yml
git commit -m "Add auto deploy workflow"
git push origin source
```

## Everytime you make change in your site
Save your changes locally

Commit the changes
```bash
git add .
git commit -m "Update docs (example: intro.md)"
```

Push to GitHub
```bash
git push origin source
```
Why?

Your Docusaurus project is stored in GitHub

GitHub Actions (or your deploy script) runs only when you push commits

The deployment workflow takes the latest source branch, builds it, and publishes it to gh-pages

So if you don’t commit & push, GitHub won’t know your site has changed → no auto-deploy.

## ⚡ Quick cycle to remember:

- npm run start → Preview locally (instant feedback)
- Edit until happy
- git add . && git commit -m "..." && git push → Trigger deploy

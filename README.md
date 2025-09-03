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

That’s it 🚀

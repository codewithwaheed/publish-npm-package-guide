# How to Publish Your First NPM Package

This repository provides a step-by-step guide on publishing your first NPM package and automating the release process using GitHub Actions.

## Prerequisites

Ensure you have the following:

- **Node.js and NPM**
- **Git and GitHub account**
- **NPM account**

## Step-by-Step Guide

### Step 1: Initialize Your Project

Start by creating a new project and initializing it with NPM:

```bash
mkdir my-first-package
cd my-first-package
npm init -y
```

### Step 2: Write Your Code

In the `index.js` file, write a simple function:

```javascript
function greet(name) {
  return `Hello, ${name}! Welcome to my first NPM package.`;
}

module.exports = greet;
```

### Step 3: Publish Your Package

Login to NPM and publish your package:

```bash
npm login
npm publish
```

### Step 4: Automate with GitHub Actions

To automate the package publishing process, add the following GitHub Actions workflow in `.github/workflows/publish.yml`:

```yaml
name: Publish NPM Package
on:
  push:
    branches:
      - main
  release:
    types: [created]
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: "14"
          registry-url: "https://registry.npmjs.org/"
      - run: npm install
      - run: npm test
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### Step 5: Tag Releases

Create and push tags to manage your package versions:

```bash
git tag v1.0.0
git push origin v1.0.0
```

Then, create a release on GitHub, which will trigger GitHub Actions to automatically publish your package to NPM.

---

## Example: `zorx-react` Library

As a practical example, check out my `zorx-react` library, which follows the same publishing flow:

- GitHub: [zorx-react](https://github.com/codewithwaheed/zorx)
- NPM: [zorx-react](https://www.npmjs.com/package/zrox-react)

The `zorx-react` library is a simple utility to demonstrate the process of publishing a package and using continuous deployment with GitHub Actions.

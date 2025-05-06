<img width="946" alt="image" src="https://github.com/user-attachments/assets/beaf82ce-3cdd-4c2f-86e8-dc852824f80f" />

<img width="937" alt="image" src="https://github.com/user-attachments/assets/9e55c0e3-69ae-4f61-a737-e3990e7f141e" />

Husky makes it simple to set up and maintain  hooks directly from  project, without messing with .git/hooks manually.
Installing Dependencies
npm install --save-dev husky lint-staged prettier eslint @commitlint/{cli,config-conventional}
Enabled Husky -> npx husky install
Added a post-install script to your package.json
"scripts": {
  "prepare": "husky install"
}
Configured Pre-commit Hooks -> ESLint and Prettier
npx eslint --init
{
  "semi": true,
  "singleQuote": true
}
Setting Up lint-staged in package.json
"lint-staged": {
  "**/*.js": [
    "eslint --fix",
    "prettier --write"
  ]
  GitHub Actions Workflow
  name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  lint:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Use Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - run: npm ci
    - run: npx eslint .




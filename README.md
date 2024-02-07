# SHARED LIBRARY

- [SHARED LIBRARY](#shared-library)
  - [Resources](#resources)
  - [What technologies are we using?](#what-technologies-are-we-using)
  - [How to add action in Github Workflow?](#how-to-add-action-in-github-workflow)
  - [How to use private package from Github?](#how-to-use-private-package-from-github)

## Resources

- [Udemy Link - Section 5: Microservices Helper Library](https://www.udemy.com/course/microservices-with-nodejs-react-typescript-and-kubernetes)

## What technologies are we using?

- [NPM Cloudinary](https://www.npmjs.com/package/cloudinary)
- [NPM HTTP Status Code ](https://www.npmjs.com/package/http-status-codes)
- [NPM Winston](https://www.npmjs.com/package/winston)
- [NPM Winston Elasticsearch](https://www.npmjs.com/package/winston-elasticsearch)

## How to add action in Github Workflow?

```yml
//.github/workflows/publish.yml

name: Publish
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
jobs:
  publish:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
        with:
          node-version: '20.x'
      - run: npm install
      - run: npm run build
      - run: |
          echo @<your-github-username>:https://npm.pkg.github.com/ > build/.npmrc
          echo '//npm.pkg.github.com/:_authToken=${NPM_TOKEN}' >> build/.npmrc
      - run: npm publish
        working-directory: ./build
        env:
          NPM_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## How to use private package from Github?

- Run `npm i <package_name>`
- Then add `.npmrc` in root folder

```.npmrc
@uzochukwueddie:registry=https://npm.pkg.github.com/uzochukwueddie
//npm.pkg.github.com/:_authToken=${NPM_TOKEN}
```

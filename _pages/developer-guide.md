---
title: ''
layout: single
permalink: '/developer-guide'
---

# Developer Guide <!-- omit in toc -->

- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [Development](#development)
  - [Dev Script](#dev-script)
  - [Sass](#sass)
  - [ESLint](#eslint)
  - [Testing](#testing)
- [Pull Requests](#pull-requests)
  - [Pull Request Messages](#pull-request-messages)
  - [Checks](#checks)
  - [Review](#review)
- [Deployment](#deployment)

## Getting Started

To install this project, follow these steps:

1. Clone the [Manoa Link](https://github.com/uhmanoalink/manoa-link) repository to your local machine

    `git clone https://github.com/uhmanoalink/manoa-link.git`

    *Note: You can also use the GitHub Desktop app*

2. Install [Meteor](https://docs.meteor.com/install.html)

    *We recommend using Node 14 and disabling security checks for the root directory.*

3. `cd` into the app directory

    *The* `app/` *directory is where npm and Meteor packages are installed.*

4. Install dependencies with `meteor npm install`

    *Make sure you are in the app directory before you install packages.*

5. Start the app with `meteor npm start`

    *In Meteor, npm commands should be run starting with* `meteor`. *According to the docs, it is especially important to ensure the build for certain binaries is consistent. For more information, [see the docs](https://docs.meteor.com/commandline.html#meteornpm).*

    *There is another script, which may be more helpful while in development. [See below](#dev-script) for more information.*

6. The app should be running at [http://localhost:3000](http://localhost:3000)

## Contributing

Before working on bug fixes or new features, check the [latest project board](https://github.com/orgs/uhmanoalink/projects) to see in-progress/ready-for-review issues. If the issue is not listed, please create a new issue and link it to the Project under "Todo".

Once you start working on an issue, move that issue to "In Progress" and assign yourself to it.

## Development

### Dev Script

If working with Sass, it is advised to run `meteor npm run dev` instead of `meteor npm start`. This makes Sass watch your `.scss` files for changes and automatically recompile, so you don't need to manually restart the app to see them.

Note: `meteor npm run dev` and `npm run dev` will do the same thing, but it is recommended to use `meteor npm` to stay consistent with other scripts.

### Sass

Our sass files are organized in the following way:

```bash
├── app
│   ├── client
│   │   ├── scss
│   │   │   ├── components
│   │   │   │   ├── __components.scss
│   │   │   │   ├── _**.scss
│   │   │   ├── globals
│   │   │   │   ├── __globals.scss
│   │   │   │   ├── _colors.scss
│   │   │   │   ├── _typography.scss
│   │   │   │   ├── _utilities.scss
│   │   │   │   └── _variables.scss
│   │   │   └── pages
│   │   │       ├── __pages.scss
│   │   │       ├── _**.scss
│   │   ├── style.scss
│   │   ├── style.css
│   │   ├── style.css.map
```

Each subdirectory has its own "import file" that imports the others in that subdirectory.

E.g. `__globals.scss`:

```scss
@import "./colors";
@import "./typography";
@import './variables';
@import './utilities';
```

Components and pages should have their own Sass files. Imported Sass files should start with an underscore (_) to mark it as a "partial", meaning a file that will only be imported. Be sure to import your new Sass file in the appropriate "import file".

The main `style.scss` file imports the "import files". It is automatically compiled to `style.css` once if you start the app with `meteor npm start`, and continuously if you run `meteor npm run dev`.

Note: You do not need to do anything with the `style.css` or `style.css.map` files.

### ESLint

We use [ESLint](https://eslint.org) to check and enforce our code style.

Run `meteor npm run lint` to check for errors.

### Testing

We use [Testcafe](https://testcafe.io) to test our app. When working on a new feature, make sure that current tests pass and you write new tests. Make sure your tests follow the same format of the other tests.

Run `meteor npm run testcafe` to run all the tests.

## Pull Requests

When you are ready to submit your changes for review, please create a draft pull request. Then follow these steps before you mark it ready for review:

- [ ] Assign yourself to the PR
- [ ] Add the label "work in progress"
- [ ] Check to make sure the correct issue is linked to the PR
- [ ] Add the PR to the project board, under "In Progress", and remove the orignal issue from the board
  - Since the two are linked, we prefer to have the PR on the board since it will have more information.
- [ ] Fill in the required PR message sections

### Pull Request Messages

All pull requests should have the following sections filled out:

1. PR Description
   1. Write a description of the new changes
   2. Include pictures of new features (if will help to explain)
   3. Include any documentation for new components or functions
2. Checklist
   1. You followed style guidelines
   2. You added tests
   3. Old tests pass
   4. If your changes depend on other changes, those changes have already been merged
3. Additional Context or Relevant Issues
   1. Where can further work be done?
   2. Why were tests not necessary for this part?
   3. Is this issue blocked by another?
4. Issue Link
   1. Though it should be linked under "Development", please link the issue here as well

### Checks

We automatically make sure the changes still pass ESLint and Testcafe checks, and merging is prevented if the checks do not pass.

### Review

Once you are confident that your changes work and all the checks pass, follow these steps:

- [ ] Mark the PR as "Ready for review"
- [ ] Move it in the project board to "Code Review / Merge Requests"
- [ ] Replace the label "work in progress" with "final review"
- [ ] Add at least 2 reviewers (only 1 review is needed)

## Deployment

The app is deployed using [Meteor Up](https://meteor-up.com/). Since the required files, `mup.js` and `settings.json`, contain sensitive information, they are stored in GitHub as environment secrets.

Deployment to DigitalOcean via mup is triggered automatically on pushes to the main branch.

Deployment takes roughly 5-10 minutes, but will be visible at [https://manoalink.site](https://manoalink.site).

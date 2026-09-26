# semantic-release-demo
A personal learning repo to understand how **semantic-release** works — not a real project.

## What is semantic-release?

`semantic-release` automates version management and package publishing based on
[Conventional Commits](https://www.conventionalcommits.org/). Instead of manually
deciding the next version number, it reads your commit messages (`fix:`, `feat:`,
`BREAKING CHANGE:`, etc.) and automatically:

- Determines the next semantic version (major/minor/patch)
- Generates a `CHANGELOG.md`
- Tags the release and publishes it (npm, GitHub Releases, etc.)

This removes manual versioning and keeps releases consistent with actual code changes.

## What this repo tests

- Running `semantic-release` from a **Jenkins pipeline** (see `Jenkinsfile`)
- Triggering releases only on `main` and `develop` branches
- A `DRY_RUN` parameter to preview version bumps and changelog output without publishing
- `.releaserc` configuration for release rules and plugins
- Commit message conventions driving automatic version bumps (currently at v1.1.4)

## Jenkins pipeline

The pipeline:
1. Installs dependencies (`npm ci`)
2. Runs `semantic-release` (dry-run or real, based on the `DRY_RUN` parameter) only on `main`/`develop`

## Status

Learning/reference repo — not intended for production use.

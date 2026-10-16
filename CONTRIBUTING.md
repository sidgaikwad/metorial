# Contributing Guide

First off — thank you for your interest in contributing to this project!  
We welcome contributions from everyone and truly appreciate your help in improving Metorial's integrations.

## What Can You Contribute?

Most contributors want to **add a new integration**. Integrations live in the [`integrations/`](./integrations) directory and are built on the [`slates`](https://www.npmjs.com/package/slates) framework.
You may also contribute bug fixes, docs, or improvements to the shared packages in [`packages/`](./packages).

## Prerequisites

Before getting started, please make sure you have the following installed:

- [**Bun**](https://bun.sh/) `>=1.4.0` — this repo pins `bun@1.4.0` (see `packageManager` in `package.json`)
- [**Node.js**](https://nodejs.org/) `>=18` — CI runs Node 20

Integrations are TypeScript packages, so Docker and Nixpacks are not needed.

## Setup Instructions

Follow these steps to get your environment ready and contribute:

1. **Fork this repository**  
   Click the "Fork" button at the top right of the repo page to create your own copy.

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/metorial.git
   cd metorial
   ```

3. **Install dependencies**
   ```bash
   bun install
   ```

4. **Build the shared packages**  
   Integrations depend on the workspace packages, so build them before building an integration:
   ```bash
   bun run packages:build
   ```

## Before You Submit

1. Make sure your code follows any existing conventions and structure.
2. Build your changes and fix any errors or warnings.
3. Commit your changes with a clear message:
   ```bash
   git commit -m "Add new integration: <name>"
   ```
4. Push your branch to your fork:
   ```bash
   git push origin your-branch-name
   ```

## Opening a Pull Request

- Go to your fork on GitHub.
- Click **"Compare & pull request"**.
- Fill in the [pull request template](./.github/PULL_REQUEST_TEMPLATE.md) — summary, changes, and any related issues.
- Hit **"Create pull request"**.

One of the maintainers will review your contribution and work with you to get it merged.

## Need Help?

If you run into issues or have questions:
- Check our [issues](https://github.com/metorial/metorial/issues) page — someone else may have run into the same thing.
- Or feel free to open a new issue!

Thanks again for contributing ❤️

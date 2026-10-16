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

## Adding a New Integration

There is no scaffolding command. The easiest way to start is to copy an existing integration that resembles what you're building and rename it:

```bash
cp -r integrations/1password integrations/your-integration
```

Each integration directory looks like this:

```
integrations/<name>/
├── slate.json           # Integration manifest (validated against ../../slate.schema.json)
├── package.json         # @slates-integrations/<name>
├── tsconfig.json
├── vitest.config.ts
├── logo.png             # or logo.svg
├── README.md
├── docs/
│   └── SPEC.md
└── src/
    ├── index.ts         # Entry point
    ├── auth.ts          # Authentication
    ├── config.ts        # Configuration schema
    ├── spec.ts          # Integration spec
    ├── lib/             # API client and shared helpers
    ├── tools/           # One file per tool
    └── tools.schema.test.ts
```

### `slate.json`

The manifest that describes your integration. It is validated against [`slate.schema.json`](./slate.schema.json):

```json
{
  "name": "@metorial/your-integration",
  "description": "A clear, specific description of what this integration does and which operations it exposes.",
  "categories": ["apis-and-http-requests"],
  "skills": ["do the first thing", "do the second thing"],
  "logoUrl": "https://provider-logos.metorial-cdn.com/your-integration.png"
}
```

### `package.json`

Keep the name under the `@slates-integrations/` scope and keep the `build`, `test` and `typecheck` scripts:

```json
{
  "name": "@slates-integrations/your-integration",
  "main": "src/index.ts",
  "type": "module",
  "scripts": {
    "build": "bunx @vercel/ncc build src/index.ts -o dist -m -s",
    "test": "vitest run --config vitest.config.ts --passWithNoTests",
    "typecheck": "tsc --noEmit"
  }
}
```

## Developing and Testing Locally

Build, test and typecheck a single integration from its own directory:

```bash
cd integrations/your-integration
bun run build
bun run test
bun run typecheck
```

The repo also ships a CLI for exercising an integration interactively. Run it through the root script, passing the integration name first:

```bash
bun run integrations:cli your-integration setup
bun run integrations:cli your-integration tools list
bun run integrations:cli your-integration tools get <toolId>
bun run integrations:cli your-integration tools call <toolId>
```

Run the test suites of all integrations:

```bash
bun run integrations:cli test
```

## Before You Submit

1. Make sure your code follows any existing conventions and structure.
2. Format and lint with [Biome](https://biomejs.dev/):
   ```bash
   bun run biome:check
   ```
3. Reproduce the CI check locally. Every pull request that is ready for review runs [`changed-integrations-pr.yml`](./.github/workflows/changed-integrations-pr.yml), which builds the integrations your PR touched and diffs their tool schemas against the base branch:
   ```bash
   bun run packages:build
   bun run integrations:validate-pr -- --base <base-branch-or-sha>
   ```
4. Commit your changes with a clear message:
   ```bash
   git commit -m "Add new integration: <name>"
   ```
5. Push your branch to your fork:
   ```bash
   git push origin your-branch-name
   ```

## Opening a Pull Request

- Go to your fork on GitHub.
- Click **"Compare & pull request"**.
- Fill in the [pull request template](./.github/PULL_REQUEST_TEMPLATE.md) — summary, changes, and any related issues.
- Hit **"Create pull request"**.

Draft pull requests skip the integration validation workflow; it runs once the PR is marked ready for review and posts its report as a comment.

One of the maintainers will review your contribution and work with you to get it merged.

## Need Help?

If you run into issues or have questions:
- Check our [issues](https://github.com/metorial/metorial/issues) page — someone else may have run into the same thing.
- Or feel free to open a new issue!

Thanks again for contributing ❤️

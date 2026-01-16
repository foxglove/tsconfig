# @foxglove/tsconfig

[![npm version](https://img.shields.io/npm/v/@foxglove/tsconfig.svg?style=flat)](https://www.npmjs.com/package/@foxglove/tsconfig)

Base tsconfig for Foxglove projects.

## Requirements

- TypeScript v5.8+

## Installation

```sh
yarn add -D @foxglove/tsconfig
```

## Usage

Choose the config that matches your environment:

### Node.js applications and published libraries

Uses `module: "NodeNext"`, which enforces Node.js ESM rules.

Use `node.json` for published libraries, even if your library will be used in bundled apps. Bundlers consume Node-style packages natively, just remember to avoid Node-specific APIs like `fs` or `process`.

Relative imports must include explicit file extensions (e.g., `import { foo } from "./bar.ts"`).

```json
{
  "extends": "@foxglove/tsconfig/node.json",
  "include": ["./src/**/*"],
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
  }
}
```

> [!TIP]
> `base.json` uses `target: "ESNext"`. For published libraries, you may wish to set a lower target (e.g., `"ES2022"` for Node 18).

### Bundled applications (Webpack, Vite, esbuild, etc)

Uses `module: "Preserve"`, which enables optimizations for code consumed directly by a bundler.

Supports extensionless relative imports (e.g., `import { foo } from "./bar"`).

```json
{
  "extends": "@foxglove/tsconfig/bundler.json",
  "include": ["./src/**/*"],
  "compilerOptions": {
    "noEmit": true,
    "lib": ["ESNext", "DOM"]
  }
}
```

### Base config

Provides strict type-checking and modern defaults, but no `module` or `moduleResolution` settings. Use this when `node.json` and `bundler.json` don't fit your environment:

```json
{
  "extends": "@foxglove/tsconfig/base.json",
  "compilerOptions": {
    "module": "...",
    "moduleResolution": "..."
  }
}
```

## License

[MIT License](/LICENSE.md)

## Releasing

```sh
tag=$(npm version minor) && echo "$tag"
git push && git push origin "$tag"
```

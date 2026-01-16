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

### Node.js applications and libraries

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

> **Note:** Uses `target: "ESNext"`. For older Node.js versions, set a lower target (e.g., `"ES2022"` for Node 18).

> **Cross-platform libraries:** Use `node.json` even if your library will be used in bundled apps. Bundlers consume Node-style packages natively—just avoid Node-specific APIs like `fs` or `process`.

### Bundled applications (Vite, Webpack, esbuild, etc)

For bundled apps that run in the browser (not published as packages):

```json
{
  "extends": "@foxglove/tsconfig/bundler.json",
  "include": ["./src/**/*"]
}
```

### Base config

Provides strict type-checking and modern defaults, but no `module` or `moduleResolution` settings. Use this when `node.json` and `bundler.json` don't fit your environment:

```json
{
  "extends": "@foxglove/tsconfig/base.json",
  "compilerOptions": {
    "target": "...",
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

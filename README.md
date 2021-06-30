# @foxglove/tsconfig

Base tsconfig for Foxglove projects.

To use, run `npm i --save-dev @foxglove/tsconfig`, then extend your `tsconfig.json` like so:

```json
{
  "extends": "@foxglove/tsconfig/base",
  "include": ["./src/**/*"],
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
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

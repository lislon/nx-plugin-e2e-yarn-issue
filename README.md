# NxPluginE2eFail

Demo for issue when I try to run e2e my own nx-plugin generated by `@nrwl/nx-plugin:plugin` under yarn 3

```
yarn set version berry
yarn install
yarn exec nx e2e my-plugin-e2e
```

Result output:

```typescript
> nx run my-plugin-e2e:e2e

Compiling TypeScript files for project "my-plugin"...
Done compiling TypeScript files for project "my-plugin".
  FAIL   my-plugin-e2e  apps/my-plugin-e2e/tests/my-plugin.spec.ts (14.007 s)
my-plugin e2e
    × should create my-plugin
--directory
      × should create src in the specified directory
--tags
      × should add tags to the project

  ● my-plugin e2e › should create my-plugin

Command failed: yarn

at runPackageManagerInstall (../../packages/nx-plugin/src/utils/testing-utils/nx-project.ts:54:27)
at newNxProject (../../packages/nx-plugin/src/utils/testing-utils/nx-project.ts:74:3)
at ensureNxProject (../../packages/nx-plugin/src/utils/testing-utils/nx-project.ts:86:3)
at Object.<anonymous> (tests/my-plugin.spec.ts:17:20)
```

When I try to run `yarn` inside `<project>/tmp` that was used for `e2e`:
```
Usage Error: The nearest package directory (C:\Users\ele\src\nx-plugin-e2e-fail\tmp\nx-e2e\proj) doesn't seem to be part of the project declared in C:\Users\ele\src\nx-plugin-e2e-fail.

- If C:\Users\ele\src\nx-plugin-e2e-fail isn't intended to be a project, remove any yarn.lock and/or package.json file there.
- If C:\Users\ele\src\nx-plugin-e2e-fail is intended to be a project, it might be that you forgot to list tmp/nx-e2e/proj in its workspace configuration.
- Finally, if C:\Users\ele\src\nx-plugin-e2e-fail is fine and you intend tmp/nx-e2e/proj to be treated as a completely separate project (not even a workspace), create an empty yarn.lock file in it.
```

Installation steps that was used to create repro:

```
npx create-nx-workspace@latest nx-plugin-e2e-fail --preset=empty --pm=yarn
yarn add -D @nrwl/nx-plugin @nrwl/react
nx generate @nrwl/react:app myapp
nx g @nrwl/nx-plugin:plugin my-plugin
```

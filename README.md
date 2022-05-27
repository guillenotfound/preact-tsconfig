# Steps to reproduce

```
npm run dev
```

As you can see, the output says:

```
6:30:53 PM [vite] Internal server error: parsing /private/tmp/preact-tsconfig/tsconfig.nodeA.json failed: Error: ENOENT: no such file or directory, open '/private/tmp/preact-tsconfig/tsconfig.nodeA.json'
  Plugin: vite:esbuild
  File: /private/tmp/preact-tsconfig/src/main.tsx
      at parseFile$1 (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:5689:11)
      at async Promise.all (index 0)
      at async parseReferences (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:5704:22)
      at async Promise.all (index 1)
      at async parse$l (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:5668:5)
      at async loadTsconfigJsonForFile (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:6057:24)
      at async transformWithEsbuild (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:5860:36)
      at async TransformContext.transform (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:5945:32)
      at async Object.transform (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:38900:30)
      at async doTransform (/private/tmp/preact-tsconfig/node_modules/vite/dist/node/chunks/dep-59dc6e00.js:55857:29)
```

The important part is `/private/tmp/preact-tsconfig/tsconfig.nodeA.json`

But `vite.config.ts` points to `/private/tmp/preact-tsconfig/tsconfig.custom.json` which should load `/private/tmp/preact-tsconfig/tsconfig.nodeB.json`.

Error goes away if I rename `tsconfig.json` to anything else, so it seems like when that file is present, for some reason the file passed to the plugin from `vite.config.ts` is ignored.
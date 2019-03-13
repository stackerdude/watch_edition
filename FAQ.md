**How do I run a subset of tests?**

When you run `./go test:dev`, this will start Jest in watch mode. It will present you with options on how to filter your tests.

You can also do the following:
```
  describe.only('group of tests', () => { ... })
  it.only('single test', () => { ... })
```

**Error: `libsass` bindings not found. Try reinstalling `node-sass`?**

You've probably switched node version. Try running `npm rebuild node-sass`

**I already have node installed, but it's a different version**

Use N to easily install and switch between different versions of Node https://github.com/tj/n


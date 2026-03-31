# Create vocabs return error ERR_UNKNOWN_FILE_EXTENSION

Run command `pnpm run setup:vocabs vocab.json` in Ubuntu oni-ui/, if get error:

```
 WARN  Unsupported engine: wanted: {"node":">=22.18.0"} (current: {"node":"v20.20.0","pnpm":"10.20.0"})

> oni-ui@2.1.5 setup:vocabs /home/RAPID/oni-ui
> scripts/fetch-vocabs.mts vocab.json

node:internal/modules/esm/get_format:189
  throw new ERR_UNKNOWN_FILE_EXTENSION(ext, filepath);
        ^

TypeError [ERR_UNKNOWN_FILE_EXTENSION]: Unknown file extension ".mts" for /home/RAPID/oni-ui/scripts/fetch-vocabs.mts
    at Object.getFileProtocolModuleFormat [as file:] (node:internal/modules/esm/get_format:189:9)
    at defaultGetFormat (node:internal/modules/esm/get_format:232:36)
    at defaultLoad (node:internal/modules/esm/load:145:22)
    at async ModuleLoader.loadAndTranslate (node:internal/modules/esm/loader:543:45)
    at async ModuleJob._link (node:internal/modules/esm/module_job:148:19) {
  code: 'ERR_UNKNOWN_FILE_EXTENSION'
}

Node.js v20.20.0
 ELIFECYCLE  Command failed with exit code 1
```

**SLN**: use nvm upgrade node and add node in package.json scripts `"setup:vocabs": "node scripts/fetch-vocabs.mts"`:

```
## check node version
node -v    # Output: v20.20.0

## check if nvm installed
command -v nvm   # If return nothing, means didn't install

## Install nvm
curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm --version

## upgrade node to latest version
nvm install --lts
nvm use --lts
nvm alias default lts/*
node -v  # Output: should be v24.x.x
```

Then run the command `pnpm run setup:vocabs vocab.json`, downloading dependencies, and show which url can access UI:

```
Done in 58.7s using pnpm v10.20.0
ubuntu@Ubuntu:~/RAPID/oni-ui/src$ pnpm run dev

> oni-ui@2.1.5 dev /home/RAPID/oni-ui
> vite


  VITE v7.2.6  ready in 776 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  Vue DevTools: Open http://localhost:5173/__devtools__/ as a separate window
  ➜  Vue DevTools: Press Alt(⌥)+Shift(⇧)+D in App to toggle the Vue DevTools
  ➜  press h + enter to show help
```
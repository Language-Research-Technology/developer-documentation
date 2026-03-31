# Missing node_module
If getting this error in arocapi when running `pnpm run build:ts`:
```
ubuntu@Ubuntu:~/RAPID/arocapi$ pnpm run build:ts

> arocapi@2.0.2 build:ts /home/daisyli/RAPID/arocapi
> tsc

sh: 1: tsc: not found
 ELIFECYCLE  Command failed.
 WARN   Local package.json exists, but node_modules missing, did you mean to install?
```

**SLN**: run `pnpm install` first.

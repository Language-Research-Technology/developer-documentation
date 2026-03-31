### @@unique error

If get `@@unique` error when running `npm run syncdb`:
```
ubuntu@Ubuntu:~/RAPID/ldacapi$ npm run syncdb

> ldacapi@1.0.0 syncdb
> ln -sfn ../node_modules/arocapi/prisma/models prisma/arocapi && npx prisma generate && npx prisma db push

Loaded Prisma config from prisma.config.ts.

Prisma config detected, skipping environment variable loading.
Prisma schema loaded from prisma
Error: Prisma schema validation - (get-dmmf wasm)
Error code: P1012
error: Error parsing attribute "@@unique": The length argument is not supported in an index definition with the current connector
  -->  node_modules/arocapi/prisma/models/file.prisma:19
   |
18 |
19 |   @@unique([fileId(length: 768)])
   |

Validation Error Count: 1
[Context: getDmmf]

Prisma CLI Version : 6.19.0
```

**SLN**: go to prisma/file.prisma: remove the index number at the last line:

```
## before
  @@unique([fileId(length: 768)])
## after 
  @@unique([fileId])

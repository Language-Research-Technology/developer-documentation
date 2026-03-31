# Backen and frontend development setup
This instruction help ldaca's development set up ldacapi, oni-ui, arocapi and database before development. All commands are based on Linux WSL2 environment. **Each repository has its own set up step in their own readme files. This instruction can work with those readme files.**

For RAPID project, we use:
- ldacapi: main branch
- oni-ui: new-api branch
- arocapi: ldacapi branch

## ldacapi
```
## Create a folder
mkdir RAPID
## Clone repo
git clone https://github.com/Language-Research-Technology/ldacapi.git
npm install 
npm audit
npm run syncdb
npm run dev
```

If running `syncdb` command get:
- `@@unique` error, go to [@@unique error](frequent-errors/syncdb-unique.md). 
- `Can't reach database server at 'localhost:5432'` error, go to [can't reach DB server at localhost error](fail-db-localhost.md).

Before running `npm run dev`, need to compose docker first.

```
cd ldacapi
docker compose up
```

If get error:
- docker cannot be found: need to close all Ubuntu terminals and cd to ldacapi again.
- ldacapi_db exited with code 1: delete the volumn `ldacapi_postgres_data`. To do this in Docker Desktop --> Volumnes --> check the name which is `ldacapi_postgres_data` --> click and see what is it containers --> go back to container to delete the container `ldacapi_db`.

If running ``npm run dev` command get:
- `.env` error, go to [create .env file](frequent-errors/create-env.md).

expect result:
```
ubuntu@Ubuntu:~/RAPID/ldacapi$ npm run dev

> ldacapi@1.0.0 dev
> node --env-file=.env --watch src/index.ts

{
  prefix: '/admin',
  repository: OcflStorageImpl { ocflVersion: '1.1' }
}
[14:47:29.833] INFO (88978): Connected to OpenSearch
[14:47:29.855] INFO (88978): Server listening at http://127.0.0.1:8080
[14:47:29.859] DEBUG (88978): Configure OpenSearch Cluster
```
And go to `http://127.0.0.1:8080`, it will be whole blank. Right click and go to `inspect` --> `console`, there is an [rocrate error](frequent-errors/rocrate-error.md). 



## Oni-UI

```
## Clone repo in local
cd RAPID
git clone https://github.com/Language-Research-Technology/oni-ui.git
## Create vocabs
pnpm run setup:vocabs vocab.json

cd src
pnpm i
pnpm run dev
```

If running create vocabs command and getting `ERR_UNKNOWN_FILE_EXTENSION` error, go to [ERR_UNKNOWN_FILE_EXTENSION error](frequent-errors/vocabs-unknown-file.md)

## arocapi

```
## Clone repo in local
cd RAPID    
git clone https://github.com/Language-Research-Technology/arocapi.git
cd arocapi
pnpm install
npx prisma generate
pnpm run build:ts
## Switch branch ldacapi in arocapi repo
git switch ldacapi  
pnpm run build:ts
## link ldacapi run it in VS code Ubuntu terminal or terminal 2
npm link

cd ..
cd ldacapi
npm link arocapi

## Every time change the arocapi code (if the code we need)
cd arocapi
git pull
pnpm run build:ts
```

If get `Missing node_modules` error when running, go to [missing node_modules in arocapi](frequent-errors/missing-node-module.md) 

### Run program
container: `docker compose up` 
ldacapi: `pnpm run dev`
oni-ui: `npm run dev`
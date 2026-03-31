# ldacapi and ONI-UI setup
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

I running ``npm run dev` command get:
- `.env` error, go to [create .env file](frequent-errors/create-env.md).

## Oni-UI

## arocapi
# Can't reach DB server at localhost error
If get error:
```
ubuntu@Ubuntu:~/RAPID/ldacapi$ npm run syncdb
> ldacapi@1.0.0 syncdb
> ln -sfn ../node_modules/arocapi/prisma/models prisma/arocapi && npx prisma generate && npx prisma db push
Loaded Prisma config from prisma.config.ts.
Prisma config detected, skipping environment variable loading.
Prisma schema loaded from prisma
✔ Generated Prisma Client (6.19.0) to ./src/generated/prisma in 84ms
✔ Generated Prisma Json Types Generator (3.6.2) to ./prisma in 85ms
Loaded Prisma config from prisma.config.ts.
Prisma config detected, skipping environment variable loading.
Prisma schema loaded from prisma
Datasource "db": PostgreSQL database "ldacapi", schema "public" at "localhost:5432"
Error: P1001: Can't reach database server at `localhost:5432`
Please make sure your database server is running at `localhost:5432`.
```

**SLN**: create a docker-compose.yml file and copy from `oni-ui`, do some changes (e.g., remove health check, networks name, POSTGRES_USER, PASSWORD, DB, etc). Then run `docker compose up -d`. If get error:

```
[+] Running 3/3
 ✔ Network ldacapi                   Created                                                     0.1s
 ✔ Volume "ldacapi_opensearch_data"  Created                                                     0.0s
 ✔ Volume "ldacapi_postgres_data"    Created                                                     0.0s
 ⠋ Container db                      Creating                                                    0.0s
 ⠋ Container opensearch              Creating                                                    0.0s
Error response from daemon: Conflict. The container name "/opensearch" is already in use by container "b61f275fa0e1774f0ebea00b02cbaf8d3c43b1bcb76922ba7ce9d930980bcaee". You have to remove (or rename) that container to be able to reuse that name.
Error response from daemon: Conflict. The container name "/db" is already in use by container "2b72130961099c9b263ca9ea2c3f60086cd01841a4c9b8db8bf978adeb069a52". You have to remove (or rename) that container to be able to reuse that name.
```

**SLN**: run stop docker command and change the container_name to `ldacapi_db` for db and opensearch in docker-compose,yml

```
## see all docker
docker ps
## stop dockers
docker stop $(docker ps -a -q)
## run docker and keep the terminal see logs
docker compose up  ## output will show ldacapi_opensearch and ldacapi_db logs

If get response is normal:

```
ubuntu@Ubuntu:~/RAPID/ldacapi$ docker compose up
WARN[0000] a network with name ldacapi exists but was not created for project "ldacapi".
Set `external: true` to use an existing network
[+] Running 2/2
 ✔ Container ldacapi_opensearch  Created                                                                                                                       0.1s
 ✔ Container ldacapi_db          Created                                                                                                                       0.1s
Attaching to ldacapi_db, ldacapi_opensearch

Here is the final docker-compose.yml version:
TBC
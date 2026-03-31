# Rocrate error

There might be error in the Ubuntu:
```
          Unknown argument `rocrate`. Did you mean `rocrateId`? Available options are marked with ?.
              at In (file:///home/RAPID/ldacapi/node_modules/@prisma/client/runtime/library.mjs:36:1363)
              at Wn.handleRequestError (file:///home/RAPID/ldacapi/node_modules/@prisma/client/runtime/library.mjs:128:6911)
              at Wn.handleAndLogRequestError (file:///home/RAPID/ldacapi/node_modules/@prisma/client/runtime/library.mjs:128:6593)
              at Wn.request (file:///home/RAPID/ldacapi/node_modules/@prisma/client/runtime/library.mjs:128:6300)
              at async a (file:///home/RAPID/ldacapi/node_modules/@prisma/client/runtime/library.mjs:137:9506)
              at async StructuralIndexer._index (file:///home/RAPID/ldacapi/src/indexer/structural.ts:36:11)
              at async StructuralIndexer.index (file:///home/RAPID/ldacapi/src/indexer/indexer.ts:52:7)
              at async indexObject (file:///home/RAPID/ldacapi/src/indexer/ocfl.ts:101:11)
              at async createIndex (file:///home/RAPID/ldacapi/src/indexer/ocfl.ts:125:11)
      "name": "PrismaClientValidationError",
      "clientVersion": "6.19.0"
    }
[14:56:31.336] DEBUG (88978): Indexing finished
```

Need to get authtorisation. So back to VS code ldacapi/, run below command:

```
curl -L -v -X POST -H "Authorization: Bearer abc"  http://localhost:8080/admin/index/arcp%3A%2F%2Fname%2Chansard
```

The `arcp%3A%2F%2Fname%2Chansard` is encoded. It is come from:

```
## In a new Ubuntu terminal
cd /opt/storage/oni/ocfl/arcp_name_hansard/__object__
## get the id
cat inventory.json
## Get the "id" string "arcp://name,hansard"
## need to go to the web `console` and run below:
encodeURIComponent("arcp://name,hansard")
```

Then run the command, the result will be:

```
ubuntu@Ubuntu:~/RAPID/ldacapi$ curl -L -v -X POST -H "Authorization: Bearer abc"  http://localhost:8080/admin/index/arcp%3A%2F%2Fname%2Chansard
* Host localhost:8080 was resolved.
* IPv6: ::1
* IPv4: 127.0.0.1
*   Trying [::1]:8080...
* connect to ::1 port 8080 from ::1 port 43686 failed: Connection refused
*   Trying 127.0.0.1:8080...
* Connected to localhost (127.0.0.1) port 8080
> POST /admin/index/arcp%3A%2F%2Fname%2Chansard HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/8.5.0
> Accept: */*
> Authorization: Bearer abc
> 
< HTTP/1.1 202 Accepted
< access-control-allow-origin: *
< content-type: application/json; charset=utf-8
< content-length: 57
< Date: Thu, 05 Feb 2026 04:56:31 GMT
< Connection: keep-alive
< Keep-Alive: timeout=72
< 
* Connection #0 to host localhost left intact
```

And the UI will be `{"total":0,"entities":[]}`. This is without index.

If the error `rocrate` still is there, means license issue.
To make the index work, need to change the contentLicenseId in src/indexer/structural.ts:

```
## before
contentLicenseId: entity.license[0]['@id'] || license,
## after
contentLicenseId: entity.license?.[0]['@id'] || license,
```

Then run `npm run syncdb` and `npm run dev`, there should be no [ERROR], and go to http://127.0.0.1:8080/entities it should be:

```
{"total":33,"entities":[{"id":"arcp://name,hansard","name":"Federal hansard","description":"Hansard data","entityType":"http://pcdm.org/models#Collection","memberOf":null,"rootCollection":{"id":"arcp://name,hansard","name":"Federal hansard"},"metadataLicenseId":"https://creativecommons.org/licenses/by/4.0/","contentLicenseId":"https://creativecommons.org/licenses/by/4.0/","access":{"metadata":true,"content":true},"accessControl":"Public","counts":{"collections":0,"objects":0,"files":0}},{"id":"arcp://name,hansard","name":"Federal hansard","description":"Hansard data","entityType":"http://pcdm.org/models#Collection","memberOf":null,"rootCollection":{"id":"arcp://name,hansard","name":"Federal hansard"},"metadataLicenseId":"https://creativecommons.org/licenses/by/4.0/","contentLicenseId":"https://creativecommons.org/licenses/by/4.0/","access":{"metadata":true,"content":true},"accessControl":"Public","counts":{"collections":0,"objects":0,"files":0}},
.....
.....
.....
```

Then start UI via `pnpm run dev` in Oni-UI WSL2, open the browser go to `http://localhost:5173/`, go to Collections, Items, there are something display. That's all done.
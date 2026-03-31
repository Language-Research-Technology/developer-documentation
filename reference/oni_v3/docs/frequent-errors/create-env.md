### create .env file
run ldacapi `npm run dev`. 
If get error:
```
> ldacapi@1.0.0 dev
> node --env-file=.env --watch src/index.ts

node: .env: not found
```
**SLN**: create a .env file and write below:

```
## Alvin sent:
DATABASE_URL="postgresql://ldacapi:ldacapi@host.containers.internal:5432/ldacapi?schema=public"
OPENSEARCH_URL="http://host.containers.internal:9200"
```

It might cause error:

```
ubuntu@Ubuntu:~/RAPID/ldacapi$ npm run dev

> ldacapi@1.0.0 dev
> node --env-file=.env --watch src/index.ts

file:///home/RAPID/ldacapi/node_modules/@prisma/client/runtime/library.mjs:119
You may have to run ${$e("prisma generate")} for your changes to take effect.`,this.config.clientVersion);return r}}parseEngineResponse(r){if(!r)throw new q("Response from the Engine was empty",{clientVersion:this.config.clientVersion});try{return JSON.parse(r)}catch{throw new q("Unable to JSON.parse response from engine",{clientVersion:this.config.clientVersion})}}async loadEngine(){if(!this.engine){this.QueryEngineConstructor||(this.library=await this.libraryLoader.loadLibrary(this.config),this.QueryEngineConstructor=this.library.QueryEngine);try{let r=new WeakRef(this);this.adapterPromise||(this.adapterPromise=this.config.adapter?.connect()?.then(Yt));let t=await this.adapterPromise;t&&Re("Using driver adapter: %O",t),this.engine=this.wrapEngine(new this.QueryEngineConstructor({datamodel:this.datamodel,env:process.env,logQueries:this.config.logQueries??!1,ignoreEnvVarErrors:!0,datasourceOverrides:this.datasourceOverrides??{},logLevel:this.logLevel,configDir:this.config.cwd,engineProtocol:"json",enableTracing:this.tracingHelper.isEnabled()},n=>{r.deref()?.logger(n)},t))}catch(r){let t=r,n=this.parseInitError(t.message);throw typeof n=="string"?t:new P(n.message,this.config.clientVersion,n.error_code)}}}logger(r){let t=this.parseEngineResponse(r);t&&(t.level=t?.level.toLowerCase()??"unknown",pf(t)?this.logEmitter.emit("query",{timestamp:new Date,query:t.query,params:t.params,duration:Number(t.duration_ms),target:t.module_path}):df(t)?this.loggerRustPanic=new de(go(this,`${t.message}: ${t.reason} in ${t.file}:${t.line}:${t.column}`),this.config.clientVersion):this.logEmitter.emit(t.level,{timestamp:new Date,message:t.message,target:t.module_path}))}parseInitError(r){try{return JSON.parse(r)}catch{}return r}parseRequestError(r){try{return JSON.parse(r)}catch{}return r}onBeforeExit(){throw new Error('"beforeExit" hook is not applicable to the library engine since Prisma 5.0.0, it is only relevant and implemented for the binary engine. Please add your event listener to the `process` object directly instead.')}async start(){if(this.libraryInstantiationPromise||(this.libraryInstantiationPromise=this.instantiateLibrary()),await this.libraryInstantiationPromise,await this.libraryStoppingPromise,this.libraryStartingPromise)return Re(`library already starting, this.libraryStarted: ${this.libraryStarted}`),this.libraryStartingPromise;if(this.libraryStarted)return;let r=async()=>{Re("library starting");try{let t={traceparent:this.tracingHelper.getTraceParent()};await this.engine?.connect(JSON.stringify(t)),this.libraryStarted=!0,this.adapterPromise||(this.adapterPromise=this.config.adapter?.connect()?.then(Yt)),await this.adapterPromise,Re("library started")}catch(t){let n=this.parseInitError(t.message);throw typeof n=="string"?t:new P(n.message,this.config.clientVersion,n.error_code)}finally{this.libraryStartingPromise=void 0}};return this.libraryStartingPromise=this.tracingHelper.runInChildSpan("connect",r),this.libraryStartingPromise}async stop(){if(await this.libraryInstantiationPromise,await this.libraryStartingPromise,await this.executingQueryPromise,this.libraryStoppingPromise)return Re("library is already stopping"),this.libraryStoppingPromise;if(!this.libraryStarted){await(await this.adapterPromise)?.dispose(),this.adapterPromise=void 0;return}let r=async()=>{await new Promise(n=>setImmediate(n)),Re("library stopping");let t={traceparent:this.tracingHelper.getTraceParent()};await this.engine?.disconnect(JSON.stringify(t)),this.engine?.free&&this.engine.free(),this.engine=void 0,this.libraryStarted=!1,this.libraryStoppingPromise=void 0,this.libraryInstantiationPromise=void 0,await(await this.adapterPromise)?.dispose(),this.adapterPromise=void 0,Re("library stopped")};return this.libraryStoppingPromise=this.tracingHelper.runInChildSpan("disconnect",r),this.libraryStoppingPromise}version(){return this.versionInfo=this.library?.version(),this.versionInfo?.version??"unknown"}debugPanic(r){return this.library?.debugPanic(r)}async request(r,{traceparent:t,interactiveTransaction:n}){Re(`sending request, this.libraryStarted: ${this.libraryStarted}`);let i=JSON.stringify({traceparent:t}),o=JSON.stringify(r);try{await this.start();let s=await this.adapterPromise;this.executingQueryPromise=this.engine?.query(o,i,n?.id),this.lastQuery=o;let a=this.parseEngineResponse(await this.executingQueryPromise);if(a.errors)throw a.errors.length===1?this.buildQueryError(a.errors[0],s?.errorRegistry):new q(JSON.stringify(a.errors),{clientVersion:this.config.clientVersion});if(this.loggerRustPanic)throw this.loggerRustPanic;return{data:a}}catch(s){if(s instanceof P)throw s;if(s.code==="GenericFailure"&&s.message?.startsWith("PANIC:"))throw new de(go(this,s.message),this.config.clientVersion);let a=this.parseRequestError(s.message);throw typeof a=="string"?s:new q(`${a.message}
                                                                                                                                                                                 
PrismaClientInitializationError: Can't reach database server at `host.containers.internal:5432`

Please make sure your database server is running at `host.containers.internal:5432`.
    at r (file:///home/RAPID/ldacapi/node_modules/@prisma/client/runtime/library.mjs:119:2770)
    at async setupDatabase (file:///home/RAPID/ldacapi/node_modules/arocapi/dist/app.js:28:5)
    at async app (file:///home/RAPID/ldacapi/node_modules/arocapi/dist/app.js:71:5) {
  clientVersion: '6.19.0',
  errorCode: 'P1001',
  retryable: undefined
}

Node.js v24.13.0
Failed running 'src/index.ts'. Waiting for file changes before restarting...
```

So the correct version of `.env`:

```
## Work in local WSL2
DATABASE_URL="postgresql://ldacapi:ldacapi@localhost:5432/ldacapi?schema=public"
OPENSEARCH_URL="http://localhost:9200"
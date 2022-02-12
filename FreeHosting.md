# Free Hosting of Web pages/services

Hosting of web static pages or dynamic services in HTTPS:
- feeding from source code (no need to build a container or to provide a binary package)
- having a always free tier (not only a trial) usable for testing or small audience/usage

Deployment of files/code by:
- push: ftp, ms-webdeploy, git, ad-hoc cli/api, online editor/ide, upload web ui
- pull from: github (gh), gitlab (gl), bitbucket (bb), ext git repo (egit)

## Static files

Note that dynamic hosting can usually also do static files (ex: replit, appengine)

https://bejamas.io/discovery/hosting/

| host | domain | deploy files | jamstack | remark |
|-|-|-|-|-|
|github pages|.github.io|git, ide|jekyll|
|gitlab pages|.gitlab.io|git, ide|
|bitbucket pages|.bitbucket.org|git, ide|
|glitch|.glitch.me|git||slow restart|
|render|.onrender.com|||CDN 2018 AWS GCP|
|surge|.surge.sh|npm||
|netlify|.netlify.app|cli/api|jamstack|2014 multi cloud|
|vercel|.vercel.app|gh gl bb cli/api|jamstack|2015 on AWS GCP|
|cloudflare pages|.pages.dev|||CDN, own infra|
|digitalocean app ptf|.ondigitalocean.app|gh gl egit dockhub|gatsby hugo next nuxt jekyll|above cloudflare, 3 free sites|
|google storage|.appspot.com|cli/api|
|google firebase|.web.app|cli/api||firestore 1GB free|
|azure static web apps|.azurestaticapps.net|?|gatsby hugo vue jekyll next nuxt|0.5GB|

- AWS has no always free service for static hosting with HTTPS, AWS Amplify is only 12mth free
- Azure CDN .azureedge.net has no free tier

## Dynamic backend

https://free-for.dev/#/?id=major-cloud-providers

ex: AppEngine Flex, Cloud Run, Replit gets your code, then the engine get dependencies, build it and put it in a container under the hood.

Quota for free tier:
- as disk space : MB, GB
- as requests per period : rq/day, rq/mth
- as network bandwidth per period : bw/day, bw/mth
- as duration of compute per period : hr/day, hr/mth
- as mem usage per period (vercel) : GB-hr/mth ; 1 GB-hr = 3600 req of 1 sec consuming 1GB each ; usual function duration is 100ms

Runtimes landscape:
- usually dynamic languages, no need for compilation : nodejs, python, ruby, php ; perl only on oldies
- sometimes bytecodes languages : java ; dotnet (C#) supported also by big ones : google, aws, ibm
- as native languages, golang is often present, less rust (iron.io), swift (ibm) or any c

| host | domain | runtimes | dbs | deploy files | free | remark |
|-|-|-|-|-|-|-|
|cloudflare workers|.workers.dev|v8 js/wasm|prop KV||100K rq/day|instant run|
|vercel edge|.vercel.app|v8 js/wasm|-|gh gl bb cli/api|3Grq/mth|on same servers as static pages|
|vercel serverless|.|go node py ruby|-|gh gl bb cli/api|100GB bw/mth, 100GB-hr/mth|
|stackpath||static, go node php perl py wasm|-|||
|render|.onrender.com|node py ruby rust go elixir php||
|heroku|.herokuapp.com|go java node php py ruby|pgsql redis|git|500h/mth free||2007 dyno, slow restart|
|fly app||go node deno python ruby elixir docker|pgsql|cli|2Kh/mth 3GBdisk, pgsql not free||
|google appengine std2|.appspot.com|node go java php py ruby|-||28h/day|2018 4/7 run (gVisor)|
|google appengine flex|.appspot.com|docker ; node go java php py ruby netcore|-||NO FREE TIER|2016 24/7 run (vm)|
|google cloudrun|.run.app|docker ; node py go java/kotlin/scala netcore||git|2M rq/mth|2019 run on-demand|
|google func||node py ruby php go java dotnet|||2M rq/mth|
|aws lambda|||||1M rq/mth|
|azure func|.azurewebsites.net||||1M rq/mth|
|ibm func|||||5M rq/mth|
|azure app service|.azurewebsites.net|node py ruby php dotnet java|cosmos db|azure repos gh bb git ftps webdeploy cli/api edit|10 apps, 1GB|lin and win|
|repl.it|.repl.co|static 30+|prop KV|ide gh||very slow restart|
|deta.sh micros||node python|||250MB files/code|linux vm|
|free.fr|.free.fr|php|mysql, pgsql|ftp||no https, shared websites|
|000webhosts||php|mysql|ftp|1GB|shared websites|
|freehostia||perl php py|mysql|ftp||shared websites|
|awardspace||php|mysql|ftp||shared websites|

- There are many other traditional php/mysql hosting, using simple shared hosting and FTP to push files
- begin.com (2015) is more a framework above raw AWS to use it easily, you have to allocate your AWS resources
- digitalocean.com (2012) : above CloudFlare CDN ; static has always free tier, not on apps : node py go ruby php on gvisor, or docker
- Oracle Functions (Fn based) has no always free tier
- AWS Elastic Beanstalk : Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker over Apache, Nginx, Passenger, and IIS ; pay only needed EC2 instances

## Database

Firestore 1GB
Azure CosmosDB 5GB
Azure Storage 5GB

## Details

### Functions

Very small units of code, pay per use : 
- Azure Functions : C#, F#, powershell, java/kotlin, node, python, custom (go, rust, ...)
  - built above Azure App Service :  _project_.azurewebsites.net/api/_function_
- AWS Lambda : nodejs, python, ruby, java, go, dotnet, custom docker
- Google Functions : go, node, python, php, ruby, java, dotnet
- IBM Apache OpenWhisk : js,swift,java,python,ruby,php,go,dotnet
- Iron.io functions: go,rust,java,node,php,python,ruby, support AWS lambda
- Oracle function : Fn based

Google Function Java : source code maven buildable or pre-built fat JAR
Google Function Dotnet (netcore3) : only C#, F#, VB with msbuild csproj/fsproj/vbproj files with nuget libs deps ; does not accept prebuilt binary
Azure Function Java/Kotlin : ad-hoc extensions in maven, gradle, intellij, vscode to build a zip sent to azure
Azure Function custom (Go, Rust) : build locally with vscode a linux/win binary being a http server, then deploy to azure

### Google layers

- Firebase : no server logic, just clients and database
- Functions : HTTP/Event small logic, deploy code, pay per use, autoscale, constrained runtime, warning on too much functions, no persistence
- AppEngine Std : HTTP only, always run, deploy code, autoscale, no pay per use?, local persistence, FEW LANGUAGES
- AppEngine Flex : ...
- Cloud Run : HTTP/Event with containers, deploy containers, pay per use, autoscale, no persistence, no clusters
- Kubernetes : multi purpose containers, deploy containers in clusters, autoscale, any protocol
- Compute : VMs

online cli/ide
- cloud shell : a VM with 5GB home, shutdown after 20mins unused ; free tier : 50h/week
- cloud shell editor : online ide, eclipse theia based (html ide based on vscode project)
  - Feb2022 langs : html css less ; node js ts coffeescript py ruby perl php lua ; cs fs ps vb bat ; java clj groovy ; shell r go rust c cpp objc swift
  - no kotlin or scala

### Google AppEngine

Always run : pay the sizing

Always free : 1GB code+static, 5GB blobstore

Quickly scale automatically

- Standard env : google specific isolation engine at process level
  - gen1 2008beta 2011 : python2, php5, java8, go ; isolation by modified runtimes, api constrained : can use only google services via google libs
  - gen2 2018 : python3, php7, java11, go, node, ruby ; gVisor process isolation, no constrains
- Flexible env : docker : python2/3, php5/7, java, go, node, ruby, netcore, custom

### Google CloudRun

As an always free tier
Run on-demand, but very fast
Replacement of AppEngine Flexible ?

Can directly deploy from source code without building a docker image : gcloud run deploy --source

Uses same buildpacks (heroku based) as AppEngine and Functions : nodejs10, python3, go, java8,11/kotlin, dotnet core 3+

based on Knative : a Kubernetes for serverless : pay per use

note : GKE requires effort to expose HTTPS

### Azure

**App Service** free tiers (F1) : 10 apps, 1GB disk

Requires credit card for registration

- Runtimes : node, python, ruby, php, dotnet, java
- Db : cosmosdb has a free tiers
- OSes : Linux or Windows, Windows is more feature rich
- Deploy :
  - from Azure repos ; from external Github, Bitbucket, Git
  - push git to a git server on the VM ; push FTP/S ; push Web Deploy (VStudio)
  - push to Kudu API, via az cli
  - Kudu UI File/Zip upload (Windows only)
  - Kudu UI File editor ; App Service Editor (Windows only)
- Shell via Kudu UI : Linux: SSH or run bash cmds ; Windows : CMD or PowerShell

### Vercel

- max 15000 files per deployment, build time <45min
- edge functions running on vercel Edge servers, as V8 with limited lib (no file io) ; similar to cloudflare workers
- serverless functions running as AWS Lambda
  - no websocket, http2/push, response streaming
  - functions zip must be < 50MB and <250MB unzipped
  - function timeout before first reply : 5 sec, proxied request 30 sec
  - response < 5MB
- https://vercel.com/docs/concepts/limits/overview

### Cloudflare

- Free x.pages.dev https://pages.cloudflare.com/
- Free tier Workers Sites ; https://developers.cloudflare.com/workers/platform/sites
  - was API Keys, now permanent Bearer Token - wrangler CLI needs a token- 
- serverless based on V8 = js,ts, wasm (from rust/c/c++ = no GC) ; js from kotlin/dart/python/scala/reason-ocaml/perl/php/f#
- Workers Site based on Workers KV db to store assets
  - https://site.project.workers.dev "wrangler generate --site X"
	- public/ : static files that will be pushed to Workers KV db by "wrangler publish"
	- worker-site/index.js : default script serving static assets from the KV db using "getAssetFromKV(evt)"
	- wrangler.toml config file : account_id,name, type:webpack/js/rust, site.bucket:'local/folder' site.entry_point='workers-site'
  
### Firebase

Allows SPA and mobile apps to directly consume data by HTTP calls to Firebase dbs : historical KV and new one.

Provides free tier for static hosting.

Also proposes to use Google functions (nodejs only) for small backend logic.

### Repl.it

for educational purposes : 35 languages, and also many libs/runtimes combinations

html py jv node deno cpp c# c php clj bash ruby lua qbasic go rust r haskell swift kotlin dart vb elixir scala erlang julia ts raku(p6) apl f#
nim crystal elisp tcl roy coffeescript forth

slow start after inactivity

### Free.fr

For clients of Free.fr ; php no https / mysql, pgsql / / FTP

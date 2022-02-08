# Free Hosting of static files/code

This hosts works from source code (no need to build a container) and have free tiers usable for dev or small audience/usage.

ex: AppEngine Flex, Cloud Run, Replit gets your code, then the engine get dependencies, build it and put it in a container under the hood.

Quick note on runtimes landscape:
- usually dynamic languages : nodejs, python, ruby, php ; perl only on oldies
- sometimes bytecodes languages : java ; dotnet (C#) supported also by big ones : google, aws, ibm
- as native languages, golang is often present, less rust (iron.io), swift (ibm) or any c

| host | domain | runtimes | dbs | push/pull files | remark |
|-|-|-|-|-|-|
|github pages|.github.io|static|-|git, ide|
|gitlab pages|.gitlab.io|static|-|git, ide|
|bitbucket pages|.bitbucket.org|static|-|git, ide|
|glitch|.glitch.me|static|-|run on-demand : slow start|
|render|.onrender.com|static|-||
|surge|.surge.sh|static|-||
|netlify|.netlify.app|static|-||dyn relies on AWS Lambda|
|vercel|.|static|-|github, gitlab, bitbucket|
|vercel|.|go node python ruby|-|github, gitlab, bitbucket|
|google storage|.appspot.com|static|-||
|google firebase|.web.app|static|firebase||not sure firebase db is free|
|google appengine std2|.appspot.com|nodejs go java php python ruby|-||24/7 run (gVisor)|
|google appengine flex|.appspot.com|nodejs go java php python ruby dotnetcore custom|-||24/7 run (docker)|
|google cloudrun|.run.app|Knative + builtin nodejs python go java/kotlin/scala dotnet||git|run on-demand|
|azure app service|.azurewebsites.net|nodejs python ruby php dotnet java|cosmos db|pull:azure repos,github,bitbucket ; push:git, ftps, vs webdeploy, kudu API, online editor|linux and windows, 10 apps, 1GB|
|repl.it|.repl.co|so many|prop KV|online ide|run on-demand : slow start|
|heroku|.herokuapp.com|go java node php python ruby|pgsql redis|git|uses dyno, not docker, run on-demand : slow start|
|cloudflare pages|.pages.dev|static|-|
|cloudflare workers|.workers.dev|V8: js,wasm|prop KV|
|stackpath||static, go node php perl python wasm|-||
|free.fr|.free.fr|php|mysql, pgsql|ftp|no https, shared websites|
|000webhosts||php|mysql|ftp|1GB, shared websites|
|freehostia||perl, php, python|mysql|ftp|shared websites|
|awardspace||php|mysql|ftp|shared websites|

Their are many other LAMP hosting : php/mysql style, using simple shared hosting and FTP to push files

## Details

### Functions

Very small units of code, pay per use : 
- Azure Functions : C#, F#, powershell, java, node, python, custom (go, rust, ...)
- AWS Lambda : nodejs, python, ruby, java, go, dotnet, custom docker
- Google Functions : go, node, python, php, ruby, java, dotnet
- IBM Apache OpenWhisk : js,swift,java,python,ruby,php,go,dotnet
- Iron.io functions: go,rust,java,node,php,python,ruby, support AWS lambda

### Google layers

- Firebase : no server logic, just clients and database
- Functions : HTTP/Event small logic, deploy code, pay per use, autoscale, constrained runtime, warning on too much functions, no persistence
- AppEngine Std : HTTP only, always run, deploy code, autoscale, no pay per use?, local persistence, FEW LANGUAGES
- AppEngine Flex : ...
- Cloud Run : HTTP/Event with containers, deploy containers, pay per use, autoscale, no persistence, no clusters
- Kubernetes : multi purpose containers, deploy containers in clusters, autoscale, any protocol
- Compute : VMs

### Google AppEngine

Always run
Quickly scale automatically

- Standard env : specific google isolation engine : process sandbox
  - gen2 : python3 ,php7, java11, node, ruby, go ; gVisor isolation, no constrains
  - gen1 2008 : python2, php5, java8 ; isolated runtimes, api constrained
- Flexible env : docker : python 2/3 ; php5/7 ; ruby, nodejs, java, go, dotnet core, custom

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

Also proposes to use Google functions (nodejs only) for small backend logic

### Repl.it

Many languages, but meant to be activated interactively

### Free.fr

For clients of Free.fr ; php no https / mysql, pgsql / / FTP

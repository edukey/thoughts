# Languages in Serverless platforms

How various languages are managed (dependencies, builds) in various Serverless platforms

Most serverless platforms allows to retrieve source code and then handle the dependencies and building.

Some platform also accept pre-built packages as docker images or zip files containing :
- on supported runtimes : complete script files (node/python/ruby/php) or bytecode files (java jar / dotnetcore exe/dll)
  - may also include some shared binary libs as linux
- linux arm64 or amd64 binary files and shared libs (from go,rust,c,...)
- self contained runtimes : you put the binary of the runtime alongs the script/bytecodes

| ptf | cmd | remarks | doc |
| - | - | - | - |
| google appengine flex | gcloud app deploy | local build
| google appengine std | gcloud app deploy | remote buildpacks
| google cloud run | gcloud run deploy | remote buildpacks to detect lang, get deps, build, gen docker, store in registry, deploy docker | [doc](https://cloud.google.com/run/docs/deploying-source-code) 
| google functions | gcloud functions deploy | 

https://github.com/googlecloudplatform/buildpacks

## Nodejs

package.json

require vs import

## Python

requirements.txt

## Ruby

## PHP

## Go

go.mod

## Java (JVM)

maven ; gradle ; fat jar

| ptf | langs | deps / build | provide prebuilt | remarks
| - | - | - | - | - |
| google appengine std2 | any | remote maven or gradle via buildpacks | graalvm binary | [doc](https://cloud.google.com/appengine/docs/standard/java-gen2/runtime)
| google appengine flex | any | local via maven/gradle/intellij/eclipse plugins | zip with war or jar | local build, flex gets a war/jar and a docker conf [doc](https://cloud.google.com/appengine/docs/flexible/java/how-to)
| google func | any | remote maven/gradle | fat jar | 
| google cloud run | any | remote maven/gradle buildpacks | docker |
| azure app service | 
| azure func | java, kotlin | adhoc ext in maven, gradle, intellij, vscode making a zip file sent to azure | NO?
| aws beanstalk |
| aws lambda |

## Dotnet


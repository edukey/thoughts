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
| google appengine flex | gcloud app deploy | local build | [doc](https://cloud.google.com/appengine/docs/flexible)
| google appengine std | gcloud app deploy | remote buildpacks | [doc](https://cloud.google.com/appengine/docs/standard)
| google cloud run | gcloud run deploy | remote buildpacks, store docker in registry, deploy docker | [doc](https://cloud.google.com/run/docs/deploying-source-code) 
| google functions | gcloud functions deploy | | [doc](https://cloud.google.com/functions/docs/concepts/exec)
| aws elastic beanstalk | eb deploy | local build or "aws codebuild" ; "bundle" zip with config and files | [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html)

buildpacks : used by heroku, pivotal and google to detect lang, retrieve dependencies, build and generate an OCI image (Docker)

https://github.com/googlecloudplatform/buildpacks ; https://buildpacks.io/

eb : nginx in front of web app on port 5000, static files and compression by nginx

Google func : 
 - HTTP
 - Background : google native event format from PubSub, Storage, Firebase, ... : Node Python Go Java
 - CloudEvents : using standard format : Ruby PHP C#

## Nodejs

package.json

require vs import

- Beanstalk
  - package.json in bundle zip, eb will retrieve deps when deploying [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_nodejs.container.html)

## Python

requirements.txt

- Beanstalk
  - uses WSGI, django
  - requirements.txt : eb use it to get dependencies [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/python-configuration-requirements.html)
- AppEngine std2 [doc](https://cloud.google.com/appengine/docs/standard/python3/runtime) : requirements.txt
  - app.yaml specifies the entry point function being web serv or else AppEngine starts gunicorn and there is a WSGI main.py with "app" object
- AppEngine Flex : [doc](https://cloud.google.com/appengine/docs/flexible/python/using-python-libraries) : requirements.txt
  - use any web fmk : flask, django, ... Need a proper WSGI server : gunicorn, uwsgi, ...
- Google Functions : [doc](https://cloud.google.com/functions/docs/writing/specifying-dependencies-python) : requirements.txt or self contained
  - some packages are always pre-installed, if needed shoudl ref them with proper version to avoid fetch at deployment
  - can use google artifact repo for private dependencies
  - HTTP function uses Flask and need "functions_framework"

## Ruby

- Beanstalk : [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_Ruby.html)
  - deps at deploy : Gemfile
- AppEngine flex : [doc](https://cloud.google.com/appengine/docs/flexible/ruby/using-ruby-libraries)
  - Gemfile, ok for linux compatible and natice libs
  - ex: `entrypoint: rails server`
- AppEngine std2 : [doc](https://cloud.google.com/appengine/docs/standard/ruby/runtime)
  - deps at deploy : Gemfile
  -  can use rack with puma, unicorn, Thin, ...
  -  generic : `entrypoint: bundle exec ruby app.rb`

## PHP

- Beanstalk
  - deps by eb via composer.json
  - or put all in your bundle file
- AppEngine flex [doc](https://cloud.google.com/appengine/docs/flexible/php/using-php-libraries)
  - composer.json, any linux/amd64 compatible
  - must use a php web framework
- AppEngine std2 [doc](https://cloud.google.com/appengine/docs/standard/php7/runtime)
  - need to have an index.php handling all requests (front controller)
  - or specify in config as `entrypoint: serve path/to/my/front/controller.php`
  - can use a long running process using `entrypoint: php long-process.php`
  - php.ini can be used to enable extra extensions (.so files)

## Go

go.mod

- Beanstalk [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/go-environment.html)
  - build by eb with go.mod
  - or provide a binary in root or bin/
- Appengine std2 : [doc](https://cloud.google.com/appengine/docs/standard/go/runtime)
  - go.mod recommended but not mandatory [doc](https://cloud.google.com/appengine/docs/standard/go/specifying-dependencies)
  - only linux/amd64 compatible libs

## Java (JVM)

maven ; gradle ; fat jar

| ptf | langs | deps / build | provide prebuilt | remarks
| - | - | - | - | - |
| google appengine std2 | any | remote maven or gradle via buildpacks | graalvm binary | [doc](https://cloud.google.com/appengine/docs/standard/java-gen2/runtime)
| google appengine flex | any | local via maven/gradle/intellij/eclipse plugins | zip with war or jar | local build, flex gets a war/jar and a docker conf [doc](https://cloud.google.com/appengine/docs/flexible/java/how-to)
| google func | any | remote maven/gradle | fat jar | 
| google cloud run | any | remote maven/gradle buildpacks | docker |
| azure app service | maven plugin | war/jar | [doc](https://docs.microsoft.com/en-us/azure/app-service/quickstart-java)
| azure func | java, kotlin | plugin in maven, gradle, intellij, vscode making a zip file sent to azure | ? | [doc](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-java)
| aws beanstalk | | | | [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_Java.html)
| aws lambda |

Beanstalk : 
- ngingx + tomcat ; deploy a WAR or multiple WAR in ZIP [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/java-tomcat-platform.html)
- nginx + jar [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/java-se-platform.html)
  - can build on EC2 usging javac/ant/maven/gradle
- the nginx proxy can directly serve the static files

## Dotnet

Beanstalk : build locally, package a bundle zip with config and dll and push to EB
- netcore on linux [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-dotnet-core-linux.html)
  - using aws provided runtime or self-contained
  - put config and dll in a zip and publish 
- dotnet on Windows with IIS
  - dotnet [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_NET.html)
    - visual studio plugin to publish to AWS
  - netcore [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/dotnet-core-tutorial.html)

## Docker

- Beanstalk [doc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/single-container-docker-configuration.html)
  - provide a zip with docker-compose.yml and app files 

# PaaS

* IaaS : (de)allocate VM with prebunbled OS, maybe augmented with some standard software (ex: db engine, web container, runtimes)
  * root access to VMs : disk, configs
  * pay per use : disk size, cpu used (cores), mem used, network bandwidth in/out ?
  * middleware/applications to be installed above the VMs by yourself
  * ex: Amazon EC2, S3 ; Google Cloud Compute Engine  ; Azure VMs ; many "cloud" hosting company
* IaaS++ : Container instead of VM
  * manage Containers (Docker) instead of VM directly
  * easier to setup
  * Load Balancer managed in front of the containers
  * faster scalability but not automatic : you must handle it by changing you cluster
  * ex: Google Cloud Container Engine (Kubernetes+Docker)
* PaaS : 
  * no access to underlying VM, no root access, no access to file system : deploy code package
  * constrained by supported runtimes (java, dotnet, ruby, python, php, ...), APIs, Db Engines
  * access to NoSql specific db or SQL db as usual (but without scalability then) and even BigData
  * provide object/blob/file storage
  * provide distributed memory cache
  * provide inter-workers communication systems : RPC, Messages Queues ?
  * integrated user authentication systems
  * capacity to send emails, to call urls
  * usually expect quick response to HTTP query (max duration)
  * specific management of background treatments (workers)
  * auto-scalability, monitoring and deployment system : devops
  * auto manage version upgrade rolling, multiple versions in parallel
  * pay per use : # "operations", volume of db, volume of mem cache, # connections, network bandwidth ?
  * ex: Heroku, Google AppEngine, Azure Workers 
* PaaS-- : mutualized hosting of simple web+sql db space : no scalability
  * FTP/WebDAV access to folder tree of website, usually with limited disk size, write access
  * access to a sql database space, also with limited size
  * usually prebundled with additional web software (ex: CMS like drupal, joomla ; wikis ; web commerce)
  * not possible to modify the global config of the web engine and db engine
  * usually no ensured capacity (cpu cores, mem)
  * ex: free.fr (php+mysql), Azure Web ?

## List of PaaS providers

* Public :
  * Zimki (2006) : js, nosql, mq ; closed 2007
  * Heroku (2007) : 
    * ruby then java, nodejs, scala, clojure, python,php
    * postgresql then redis, couchbase, cloudant, mongodb
    * dynos grid ; on debian ; bought by salesforce on 2010
  * EngineYard (2006) : ruby then php, nodejs (2011), java
    * postgresql, mysql, redis, memcached 
    * run on Gentoo/Ubuntu ; Nginx ; HAProxy ; AWS then AzureVm? (2013) ; Deis and Docker (2015)
  * Google AppEngine (2008 beta, 2011 rel) : pythonthen java, go ; nosql bigtable gql then mysql
  * Force.com : apex (prop lang) ; prop db
  * Azure Workers
  * Jelastic (2010)
    * Java then php (2013), ruby & nodejs (2014), python, dotnet (2015)
    * on OpenShift (2014), docker and parallels (for win) (2015) ; multiple hosting partners
  * Amazon Elastic Beanstalk
    * ruby,python,php on apache ; dotnet on iis ; java on tomcat ; nodejs ; go
    * dynamodb ; mysql, postgresql, oracle byol, sqlexpress ; elasticache
    * Simple NotificationService, QueueService, Workflow
    * docker
  * also: nodejitsu (closed) ; distelli
* On-Premise
  * Apprenda (2007) : dotnet ; java (2013)
  * RedHat OpenShift
    * oss github ; deploy with git ; on redhat linux only
    * java ; nodejs ; ruby rack rails/sinatra ; python wsgi django ; php ; perl psgi dancer
    * postgresql, mysql, mongodb
    * will support Windows dotnet and sqlserver using Uhuru
    * MCollective internal agents
  * CloudFoundry (VMWare then Pivotal JV), not a full PaaS but instanciate and bind "services"
    * fmk (buildpack) : java/spring,grails, ruby/rails,sinatra, nodejs, scala/play2,lift, python, php 
    * db : MySQL, PostgreSQL, MongoDB, Redis, Riak, DataStax (Cassandra), Neo4J, Pivotal HD (Hadoop)
    * mq : rabbitmq
    * dev: CloudBees
    * run on : vSphere, OpenStack/BOSH, VirtualBox/Vagrant, AWS
  * Azure Pack
  * AppScale : re-implem AppEngine API
  * IBM Bluemix (2014): CloudFoundry + SoftLayer


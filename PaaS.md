# PaaS

* IaaS : (de)allocate VM with prebunbled OS, maybe augmented with some standard software (ex: db engine, web container, runtimes)
  * root access to VMs : disk, configs
  * pay per use : disk size, cpu used (cores), mem used, network bandwidth in/out ?
  * middleware/app containers to be set up
  * ex: Amazon EC2, S3 ; Google ; Azure VMs ; many "cloud" hosting company
* PaaS : 
  * no access to underlying VM, no root access, no access to file system
  * constrained by supported runtimes (java, dotnet, ruby, python, php, ...), APIs, Db Engines
  * usually expect quick response to HTTP query (max duration)
  * specific management of background treatments
  * natively scalable
  * pay per use : # "operations", volume of db, volume of mem cache, # connections, network bandwidth ?
  * ex: Heroku, Google AppEngine, Azure Workers, 
* PaaS-- : mutualized hosting of simple web+sql db space
  * FTP/WebDAV access to folder tree of website, usually with limited disk size, write access
  * access to a sql database space
  * usually prebundled with additional web software (ex: CMS like drupal, joomla ; wikis ; web commerce)
  * not possible to modify the global config of the web engine and db engine
  * usually no ensured capacity (cpu cores, mem)
  * ex: free.fr (php+mysql), Azure Web ?

* Public :
  * Zimki (2006) : js, nosql, mq
  * Heroku
  * Google AppEngine (2008) : python, nosql gql ; then java, go, mysql
  * Azure
  * Amazon Elastic Beanstalk
  * Force.com
* On-Premise
  * Apprenda
  * RedHat OpenShift
  * Pivotal CloudFoundry
  * Azure Pack
  * AppScale


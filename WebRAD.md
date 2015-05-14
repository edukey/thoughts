# Web RAD

Find a RAD framework to quickly get CRUD web app and live improve it, without programming, with just data model definition

there is no difference between the data model definition and data input/query

* define data model 
  * core typed data : string with format, num/bool/date, mline with markdown, enum/(m)value list/ref to other entity
  * users from some referential
  * model definition may be a single xml/json/yaml file
  * (sub)grouped attributes
  * reused types group : ex: -/yes/no/n-a enum list + num + short label + markup info
  * sub (composite) entities
  * related entities
* allow specialization of types by code
* input/update data as :
  * unitary form
  * grid (horiz or verti)
* show online users, with chat
* trace all changes on model and data (what,who,when,why), allow revert
  * use db like datomic ?
* allow branch/merge model definition ?

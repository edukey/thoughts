# Web RAD

Find a RAD framework/solution to quickly get CRUD web app and live improve it, without coding, with just data model definition

there is no difference between the data model definition and data input/query : both are done live

* Often found form editor/builder within CMS or wikis (Drupal, Sharepoint, ...) as native or plugin
* commercial online web form/survey/app/database builders ; DIY online databases
  * wufoo, caspio.com, knackhq.com, quickbase, zoho.com, teamdesk.net, trackvia, zenginehq.com, outsystems, appery.io, ...
  * "free" ones : grubba/sodadb 
  * http://shayacrich.com/online-databases-and-business-apps , http://project-management.com/top-5-online-app-builders-for-creating-your-own-pm-tool/

* define data model 
  * core typed data : string with format, num/bool/date, mline with markdown, enum/(m)value list/ref to other entity
  * attribute has : codename, type, label, summary, description, link to some external doc
  * entity: users from some referential
  * model definition may be a single xml/json/yaml file
  * (sub)grouped attributes
  * reused types group : ex: -/yes/no/n-a enum list + num + short label + markup info
  * sub (composite) entities
  * related entities
  * manage user/group/role as first class entity
* allow specialization of types by code
* view data as :
  * unitary view : may be customized by logic free templating (ex:mustache) ; propose form display templates
  * grid/list with reorder/hide fields,sort,group,filter, transpose
* input/update data as :
  * unitary form
  * grid (horiz or verti)
* trace all changes on model and data (what,who,when,why), allow revert, allow to retrieve an as-of view of data
  * use db like datomic ?
* API to import/export data, anyway used by the HTML5 SPA ; support JSON and CSV and others ...
* allow comments threads, scoring/likes from users
* send notification on changes, on watched entity, from related entities, rules by user role ; live or end of day or period
* show online users, with chat
* allow branch/merge model definition ?
* data analytics, charts, graphs

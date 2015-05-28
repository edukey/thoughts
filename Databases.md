# Databases

Persist amount of (pre)structured data

* Relational : table of typed columns, some columns are used as references to other tables rows, SQL as query language, schema first
  * Sybase ASE c (Sybase Anywhere is another lightweight engine)
  * Microsoft SqlServer c (from Sysbase)
  * Oracle c
  * Sqlite c free : embedded mono user
  * MySql/MariaDB c free : lead in opensource
  * PostgreSql c free : more complete than mysql
  * H2 java free
  * Derby java free
* ColumnStore : good for analytics, OLAP style
  * Sybase IQ c
* NoSql : schema less (semi-structured) & scalable & rest api ; 2009
  * Column
    * Cassandra java
    * HBase java
  * Document : no joins between documents
    * MongoDB c++ rest
    * Couchbase erlang : memcache with persistence
    * CouchDB erlang
    * ElasticSearch java rest
    * RavenDB c#
  * kv
    * Redis c
    * Riak erlang rest
  * MultiModel : support joins/links
    * OrientDB java rest
    * ArangoDB c,v8 rest
    * FoundationDB on top of kv-db
  * Append : append only, get as-of views, fully audited
    * Datomic: append only get as-of ; on top of multiple backend db (kv model)
* Graph
  * Neo4j java
* Grid/Cache : massive distributed cache: Gigaspace, Hazelcast, infinispan, GemFire, Coherence
* XML
  * Documentum
  * eXists
* Object
  * Versant
  * VelocityDB c#

more: http://nosql-database.org/

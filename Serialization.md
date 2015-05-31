Data serialization format to host small blocks of structured data (not databases, not message/request protocol)

Also called data representation formats

Should defines data types, tree (and graph) structures, be auto descriptive or have schema specs

Not exaustive list, with a bit of history

Date and datetime are often not a normalized data type, also boolean 

# Textual

Normal human can read and understand it directly

* Positional : flat, no desc, no schema spec
* CSV : flat, only name desc not type, no schema spec, data types as supported by Excel
* EDIFACT : used in industry, separators for segments,components,fields ; components/fields content semantic is defined by the segment title as per some schema directory
* SGML : names/attributes content ; HTML is sort of SGML language
* XML - XSD : names/attributes content ; single element must be as <A/> , attributes must have a value
* JSON - WADL/SWAGGER/... ; list [a, b] , map {a:b, c:d}, null boolean string number ; no comment,tag,datetime
* YAML : indent, newline, custom types
* EDN : Clojure world ; list (a b c), vector [a b c], set #{b c d}, map {k1 v1 k2 v2} , :keywords , #tags, comments ; , discard #_, nil bool string char integer float , #inst "2014-12-13T23:45:34Z"
* GWT RPC : not readable but minified text

# Binary for the web

Meant for transport in web context

* Protobuf
* Avro
* Thrift
* MessagePack
* Flash AMF

# Binary by mdw framework

used for network or cross-techno interprocess communications

* Sun RPC : XDR - IDL schema ; first historical large one
* DCE/MS RPC/DCOM : NDR - IDL schema
* Corba IIOP : CDR - IDL schema
* Dotnet WCF : sort of binary xml
* ZeroC Ice
* DBus

# Binary generic

not especially meant for transport

* ASN.1
* ebxml (mkv)
* Bson (mongodb)
* Fressian (datomic), close to hessian ?

# Binary by Language

* Java binary (also in RMI)
* Hessian : for java
* Dotnet binary (also in .NetRemoting)
* Python pickle
* Ruby marshal
* Go ?


http://en.wikipedia.org/wiki/Remote_procedure_call

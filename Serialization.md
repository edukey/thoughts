Data serialization format to host small blocks of structured data (not databases, not message/request protocol)

Also called data representation formats

Should defines data types, tree (and graph) structures, be auto descriptive or have schema specs

Not exaustive list, with a bit of history

Date and datetime are often not a normalized data type, also boolean 

# Textual

Normal human can read and understand it directly

* Positional : flat, no desc, no schema spec
* CSV : flat, only name desc not type, no schema spec, data types as supported by Excel
* XML - XSD
* JSON - WADL/SWAGGER/...
* YAML
* GWT RPC

# Binary for the web

Meant for transport in web context

* Protobuf
* Avro
* Thrift
* MessagePack
* Flash AMF

# Binary generic

not especially meant for transport

* ASN.1
* ebxml (mkv)
* Bson (mongodb)

# Binary by Language

* Java binary (also in RMI)
* Dotnet binary (also in .NetRemoting)
* Python pickle
* Ruby marshal
* Go ?

# Binary by mdw framework

* Sun RPC : XDR - IDL schema ; first historical large one
* DCE/MS RPC/DCOM : NDR - IDL schema
* Corba IIOP : CDR - IDL schema
* Dotnet WCF
* ZeroC Ice
* DBus

http://en.wikipedia.org/wiki/Remote_procedure_call

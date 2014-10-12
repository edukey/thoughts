# Web API

## Format

* requested format for response :
  * within url as account.xml, account.json, accounts.csv
  * or as Accept header with mime type : Accept: text/xml ; Accept: application/vnd.acme.account+xml
* actual format of request or response body use Content-Type : Content-Type: text/xml ; Content-Type: application/vnd.acme.account+xml

* xml : good for tools and validation, low for human, data types defined by XSD, no clear list semantic, attributes (meta-data) ?, verbose
  * rdf : good for meta model
  * atom : good for links
  * html : good for humans only when behind a browser, like xml
* json : good for javascript clients &amp; servers, average for human, self expressed types (string, num, boolean, list) but no date-time type
* csv : good for human when small and comma used, good for Excel and SQL databases import/export, good for volumes
* yaml : good for human, has comments, supports datetime, indentation based, can do explicit typing
* markdown : good for humans behind a simple text editor, no data semantics

## Versionning

* Ensure client wont break on new fields, but just ignore them : non-breaking changes
* Allow client to explicitely declare the fields it wants to get (ODATA)

within url as /api/v1/account => breaks HATEOAS
within header as Accept : Accept: application/vnd.acme.account-v2+xml => HATEOAS compliant

* [Williams 2008](http://barelyenough.org/blog/2008/05/versioning-rest-web-services/)

## REST

* "REST" ([Fielding 2000](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)) : 
  * Client - Server
  * Stateless Server : the request must be self sufficient
  * Cache : client can cache responses to avoid redoing same requests
  * Layered : Client - Firewall - Gateway - LoadBalancer - Server
  * Code-On-Demand : client can execute "code" provided by server (my thought: not for WebAPIs)
  * Uniform interface
    * State Transfer : browse from page (state) to page (state) via links (transitions)
* Pragmatical
  * Allamaraju "RESTful Web Services Cookbook" 2010 O'Reilly
  * Masse "REST API Design" 2011 O'Reilly
  * http://restcookbook.com/
* "Truly RESTful" : 
  * Richardson "RESTful Web Services" 2007 O'Reilly, "RESTful Web API" 2013 O'Reilly
  * Fielding "[REST APIs must be hypertext-driven](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)"
  * [Apigee opinion on HATEOAS](http://fr.slideshare.net/apigee/hateoas-101-opinionated-introduction-to-a-rest-api-style)
  * Richardson Maturity Model : ([Fowler 2010](http://martinfowler.com/articles/richardsonMaturityModel.html))
    * 0: HTTP POST on fixed url with all API meaning within query/response body, ex: XML-RPC, SOAP
    * 1: URL as resource 
    * 2: Meaningful HTTP Verbs & Status Code : GET=safe, other=unsafe ; PUT=on URL resource ; POST=not on resource
    * 3: use Hypermedia ([HATEOAS](http://en.wikipedia.org/wiki/HATEOAS)) to avoid need for "out-of-band" information (doc)

## Hypermedia - HATEOAS 

Requires a way to represent "links" in API output data :
```
<link rel='meeting.confirm' href='/meeting/4515457/confirm' />
links: [ { 'rel':'meeting.confirm', 'href':'/meeting/4515457/confirm' }, ... ]
```

JSON hypermedia : Collection+JSON, HAL, JSON for Linking Data, Siren

my thought : hypermedia is not given to end-user at runtime but to client developer at design time, it can make sens to end-user only if the UI system dynamically follow the API hypermedia (as in HTML) AND needed data (payload)

* API is itself "browsable" from its start point
  * my thought : this reduce the need for documentation, but doc will never be avoided, so not extremely helpfull
* indirection : URLs are provided by links not doc, "rel" defines what the url is about
  * this allow server-side to change its urls, but not its keywords in "rel"
    * my thought : it much complexifies the client side for a "small" advantage on server side
    * my thought : anyway, the exact usage of the url must be known in advance by the client developer, based on what documentation says about the "rel" keyword
* related resources : the API directly says how to reach other resources which have relations to the current one
* authorized action (state transition) : the API say which action is possible on the current resource
  * my thought : this may have some value, other way will be the client to first try the operation on the resource (transition) and get an error from the server, like 403
*  my thought : interestingly, REST url are mainly understood as resource centric, but Hypermedia "sub-"urls are about action (transition)

* Hypermedia apis : 
  * https://api.github.com/ : you could have a UI client to browse this api without knowning it, only its link semantic of xxx_url fields and parameters

* Frameworks :
  * [Restfulie](http://restfulie.caelum.com.br/)
  * [Spring HATEOAS](http://spring.io/understanding/HATEOAS)

```
GET /account/12345 HTTP/1.1
  Host: somebank.org
  Accept: application/xml
```

Here is a response at T1:
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: ...

<?xml version="1.0"?>
<account>
   <account_number>12345</account_number>
   <balance currency="usd">100.00</balance>
   <link rel="to.agency" href="/agency/richmond" />
   <link rel="to.client" href="/client/john.doe" />
   <link rel="to.officer" href="/officer/michael.johnson" />
   <link rel="do.account.deposit" href="/account/12345/deposit" />
   <link rel="do.account.withdraw" href="/account/12345/withdraw" /> 
   <link rel="do.account.transfer" href="/account/12345/transfer" />
   <link rel="do.account.close" href="/account/12345/close" />
 </account>
```

Here is another response at T2:

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: ...

<?xml version="1.0"?>
<account>
    <account_number>12345</account_number>
    <balance currency="usd">-25.00</balance>
    <link rel="deposit" href="/account/12345/deposit" />
</account>
```

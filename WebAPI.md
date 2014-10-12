# Web API

## Formats

* requested format for response :
  * within url as account.xml, account.json, accounts.csv
  * or as Accept header with mime type : `Accept: text/xml` ; `Accept: application/vnd.acme.account+xml`
* actual format of request or response body use Content-Type : `Content-Type: text/xml` ; `Content-Type: application/vnd.acme.account+xml`

* xml : good for tools and validation, low for human, data types defined by XSD, no clear list semantic, attributes (meta-data) ?, verbose
  * rdf : good for meta model
  * atom : good for links
  * html : good for humans only when behind a browser, like xml
* json : good for javascript clients &amp; servers, average for human, self expressed types (string, num, boolean, list) but no date-time type
* csv : good for human when small and comma used, good for Excel and SQL databases import/export, good for volumes
* [yaml](http://www.yaml.org/) : good for human, has comments, supports datetime, indentation based, can do explicit typing ; [js-yaml](https://github.com/nodeca/js-yaml)
* markdown : good for humans, but no data structure semantics (fields, types), can be emulated with added semantics (using bullets)

## Versionning

Two strategies that can be combined :

* Ensure non breaking changes
  * Ensure client wont break on new fields, but just ignore them : non-breaking changes (avoid XSD validation)
  * Allow client to explicitely declare the fields it wants to get (ODATA)
* Support multiple parallel versions
  * within url as `/api/v1/account` => breaks Hypermedia
  * within header as : `Accept: application/vnd.acme.account-v2+xml` => Hypermedia compliant

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
  * Allamaraju "[RESTful Web Services Cookbook](http://shop.oreilly.com/product/9780596801694.do)" 2010 O'Reilly
  * http://restcookbook.com/, http://rest.elkstein.org/ (2008)
* "Truly RESTful" : 
  * Richardson "[RESTful Web Services](http://shop.oreilly.com/product/9780596529260.do)" 2007 O'Reilly
  * Fielding "[REST APIs must be hypertext-driven](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)" 2008
  * Webber "[REST in Practice](http://shop.oreilly.com/product/9780596805838.do)" 2010 O'Reilly
  * Amundsen "[Building Hypermedia APIs with HTML5 and Node](http://shop.oreilly.com/product/0636920020530.do)" 2011 O'Reilly
  * Masse "[REST API Design Rulebook](http://shop.oreilly.com/product/0636920021575.do)" 2011 O'Reilly
  * Richardson "[RESTful Web API](http://shop.oreilly.com/product/0636920028468.do)" 2013 O'Reilly
  * [Apigee opinion on HATEOAS](http://fr.slideshare.net/apigee/hateoas-101-opinionated-introduction-to-a-rest-api-style), [some guy bad opinion with interesting counter comments](http://www.jeffknupp.com/blog/2014/06/03/why-i-hate-hateoas/)
  * Richardson Maturity Model : ([Fowler 2010](http://martinfowler.com/articles/richardsonMaturityModel.html))
    * 0: HTTP POST on fixed url with all API meaning within query/response body, ex: XML-RPC, SOAP
    * 1: URL as resource 
    * 2: Meaningful HTTP Verbs & Status Code : GET=safe, other=unsafe ; PUT=on URL resource ; POST=not on resource
    * 3: use Hypermedia ([HATEOAS](http://en.wikipedia.org/wiki/HATEOAS)) to avoid need for "out-of-band" information (doc)

## Hypermedia - HATEOAS 

Requires a consistent conventional way to represent "links" in API output data :
```
<link rel='meeting.confirm' href='/meeting/4515457/confirm' />
links: [ { 'rel':'meeting.confirm', 'href':'/meeting/4515457/confirm' }, ... ]
```

JSON hypermedia : Collection+JSON, HAL, JSON for Linking Data, Siren

my thought : hypermedia is not given to end-user at runtime but to client developer at design time, it can make sens to end-user only if the UI system dynamically follow the API hypermedia (as in HTML) AND needed data (payload)

* API is itself "browsable" from its start point, so participates to documentation and discovery of the API at design time by client developer
  * my thought : this reduce the need for documentation, but doc will never be avoided, so not extremely helpfull
  * my thought : if the API also has a HTML format, it may allow the end-user to browse it directly without need for developer
* indirection : URLs are provided by links not hard-coded from doc, "rel" defines what the url is about
  * this allow server-side to change its urls roots, but not its keywords in "rel"
    * my thought : it much complexifies the client side for a "small" advantage on server side
    * my thought : anyway, the URL parameters/templates and in/out data must be documented to developer
    * my thought : anyway, the exact usage of the url must be known in advance by the client developer, based on what documentation says about the "rel" keyword
* related resources : the API directly says how to reach other resources which have relations to the current one, the developer does not need to reconstruct such urls as per documentation says
* authorized action (state transition) : the API say which action is possible on the current resource
  * the developer can write some logic as per the allowed transitions
  * my thought : this may have some value, other way will be the client to first try the operation on the resource (transition) and get an error from the server, like 403
*  my thought : interestingly, REST urls are mainly understood as resource centric, but Hypermedia "sub-"urls are about action (transitions)

* Hypermedia apis : 
  * https://api.github.com/ : you could have a UI client to browse this api without knowning it, only its link semantic of xxx_url fields and parameters
  * [Paypal](https://developer.paypal.com/docs/integration/direct/paypal-rest-payment-hateoas-links/)

* Frameworks :
  * [Restfulie](http://restfulie.caelum.com.br/)
  * [Spring HATEOAS](http://spring.io/understanding/HATEOAS)

```
GET /account/12345 HTTP/1.1

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

Here is another response at T2, with less possible actions:

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: ...

<?xml version="1.0"?>
<account>
    <account_number>12345</account_number>
    <balance currency="usd">-25.00</balance>
   <link rel="to.agency" href="/agency/richmond" />
   <link rel="to.client" href="/client/john.doe" />
   <link rel="to.officer" href="/officer/michael.johnson" />
    <link rel="deposit" href="/account/12345/deposit" />
</account>
```

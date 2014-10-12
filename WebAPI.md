# Web API

* "REST" ([Fielding 2000](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)) : 
* Pragmatical
  * Allamaraju "RESTful Web Services Cookbook" 2010 O'Reilly
  * Masse "REST API Design" 2011 O'Reilly
  * http://restcookbook.com/
* "Truly RESTful" : 
  * Richardson "RESTful Web Services" 2007 O'Reilly, "RESTful Web API" 2013 O'Reilly
  * Fielding "[REST APIs must be hypertext-driven](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)"
  * Richardson Maturity Model : ([Fowler 2010](http://martinfowler.com/articles/richardsonMaturityModel.html))
    * 0: HTTP POST on fixed url with all API meaning within query/response body, ex: XML-RPC, SOAP
    * 1: URL as resource 
    * 2: Meaningful HTTP Verbs : GET=safe, other=unsafe ; PUT=on URL resource ; POST=not on resource
    * 3: use Hypermedia ([HATEOAS](http://en.wikipedia.org/wiki/HATEOAS)) to avoid need for "out-of-band" information (doc)
  * Hypermedia (HATEOAS)
    * API is itself "browsable" from its start point
      * my thought : this reduce the need for documentation, but doc will never be avoided, so not extremely helpfull
    * indirection : URLs are provided by links not doc, "rel" defines what the url is about
      * this allow server-side to change its urls, but not its keywords in "rel"
        * my thought : it much complexifies the client side for a "small" advantage on server side
        * my thought : anyway, the exact usage of the url must be known in advance by the client developer, based on what documentation says about the "rel" keyword
    * authorized action (state transition) : the API say which action is possible on the current resource
      * my thought : this may have some value, other way will be the client to first try the operation on the resource (transition) and get an error from the server, like 403
    *  my thought : interestingly, REST url are mainly understood as resource centric, but Hypermedia "sub-"urls are about action (transition)
    * [Restfulie](http://restfulie.caelum.com.br/)
    * [Spring HATEOAS](http://spring.io/understanding/HATEOAS)

## HATEOAS sample

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
   <link rel="deposit" href="/account/12345/deposit" />
   <link rel="withdraw" href="/account/12345/withdraw" /> 
   <link rel="transfer" href="/account/12345/transfer" />
   <link rel="close" href="/account/12345/close" />
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

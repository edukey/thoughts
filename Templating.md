# Text templating

typically to generate xml or html, also to generate code in various languages

* xlst : to xml, in xml
* coldfusion cfml
* asp, aspx c#, jsp, ror erb : <% code %> <%= expr %> <%-- comment --%> <%@ pagedirective atr="val" %>
* php <?code?> <?=expr?> ; asp/jsp syntax also supported
* velocity java : $expr ; #set($foo=code) #if() #foreach(itm in list) #else #end ; ## com ; #* mlcom *# ; excl #[[...]]#
* thymeleaf java only for x/html using attributes to loop/fill tag content : th:text="${expr}" th:each="item : ${list}"
* t4 c# <#code#> <#=expr#>
* razor c# mvc3 @expr @code @{mlines code} @(expr) no close marker, nativelly understand c# semantic of }
* django python {{expr}} {{expr|filter}} {%code%} for itm in list endfor if expr else endif
* liquid ruby (jekyll) same as django {{expr}} {{expr|filter}} {%code%} for itm in list endfor if expr else endif
* mustache : {{expr}} ; no code logic, sections when checking boolean and lists  {{#list}} {{/list}} , invert {{^bool}}, comment {{!bla}}
* angular : only html : <tag ng-repeat="itm in list">{{itm}}</tag> ; {{expr|filter}}

http://en.wikipedia.org/wiki/Comparison_of_web_template_engines

engines from Play (java), RoR (ruby) ?

# Text templating

typically to generate xml or html, also to generate code in various languages

* using a generic code language for logic
  * asp vb/js, aspx c#, jsp java, ror erb ruby : <% code %> <%= expr %> <%-- comment --%> <%@ pagedirective atr="val" %>
  * php <?code?> <?=expr?> ; asp/jsp syntax also supported
  * mvc3 razor c# @expr @code @{mlines code} @(expr) no close marker, nativelly understand c# semantic of }
* specific xml/html based language (conditionals as attributes)
  * xlst : to xml,html,text, in xml : rule based, support also flow : <xsl:template match=""> <xsl:value-of select=""> <xsl:apply-templates select=""> <xsl:if> <xsl:for-each>
  * coldfusion cfml : to html, in xml : <cfoutput>#expr#</cfoutput> ; <cfset foo="expr"> ; 
  * thymeleaf java only for x/html using attributes to loop/fill tag content : <tag th:text="${expr}">sample</tag> <tag th:each="item : ${list}">
  * angular : only html : <tag ng-repeat="itm in list">{{itm}}</tag> ; {{expr|filter}}
* 
* velocity java : $expr ; #set($foo=code) #if() #foreach(itm in list) #else #end ; ## com ; #* mlcom *# ; excl #[[...]]#
* t4 c# <#code#> <#=expr#>
* django python {{expr}} {{expr|filter}} {%tags%} for itm in list endfor if expr else endif
* liquid ruby (jekyll) same as django {{expr}} {{expr|filter}} {%tags%} for itm in list endfor if expr else endif
* mustache : {{expr}} ; no code logic, sections when checking boolean and lists  {{#list}} {{/list}} , invert {{^bool}}, comment {{!bla}}

http://en.wikipedia.org/wiki/Comparison_of_web_template_engines

engines from Play (java), RoR (ruby) ?

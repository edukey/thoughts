# Text templating

typically to generate html, also to generate code and whatever text

* using an existing code language for logic
  * asp vb/js, aspx c#, jsp java, ror erb ruby : <% code %> <%= expr %> <%-- comment --%> <%@ pagedirective atr="val" %>
  * php <?code?> <?=expr?> ; asp/jsp syntax also supported
  * t4 c# <#code#> <#=expr#>
  * mvc3 razor c# @expr @code @{mlines code} @(expr) no close marker, nativelly understand c# semantic of }
* specific xml/html based language (control flow as attributes)
  * xlst : to xml,html,text, in xml : rule based, support also flow : <xsl:template match=""> <xsl:value-of select=""> <xsl:apply-templates select=""> <xsl:if> <xsl:for-each>
  * coldfusion cfml : to html, in xml : <cfoutput>#expr#</cfoutput> ; <cfset foo="expr"> ; 
  * thymeleaf java only for x/html using attributes to loop/fill tag content : <tag th:text="${expr}">sample</tag> <tag th:each="item : ${list}">
  * angular : only html : <tag ng-repeat="itm in list">{{itm}}</tag> ; {{expr|filter}}
* specific templating language
  * velocity java : $expr ; #set($foo=code) #if() #foreach(itm in list) #else #end ; ## com ; #* mlcom *# ; excl #[[...]]#
  * django python {{expr}} {{expr|filter}} ; {%tags%} : for itm in list endfor if expr else endif include block endblock
    * Jinja python
    * liquid ruby (jekyll)
    * swig js
  * mustache multi : {{expr}} ; no code logic, sections when checking boolean and lists  {{#list}} {{/list}} , invert {{^bool}}, comment {{!bla}}
    * handlebars : add control flow
    * hogan
  
http://en.wikipedia.org/wiki/Comparison_of_web_template_engines

engines from Play (java) ?

# Text templating

typically to generate html, also to generate code and whatever text

when following Model View pattern the View should be computed from a predefined complete Model only and not requiring any I/O or complex processing

* using an existing code language for logic
  * asp vb/js, aspx c#, jsp java, ror erb ruby : `<% code %>` `<%= expr %>` `<%-- comment --%>` `<%@ pagedirective atr="val" %>`
  * php `<?code?>` `<?=expr?>` ; asp/jsp syntax also supported
  * t4 c# `<#code#>` `<#=expr#>`
  * mvc3 razor c# `@expr` `@code` `@{mlines code}` `@(expr)` no close marker, nativelly understand c# semantic of `}`
* xml/html based language
  * xlst : to xml,html,text, in xml : rule based, support also flow  ; complex , hard to read : `<xsl:template match="">` `<xsl:value-of select="">` `<xsl:apply-templates select="">` `<xsl:if>` `<xsl:for-each>`
  * coldfusion cfml : to html, in xml ; dedicated to cf platform : `<cfoutput>#expr#</cfoutput>` ; `<cfset foo="expr">`
  * thymeleaf java only for x/html using attributes to loop/fill tag content : `<tag th:text="${expr}">sample</tag>` `<tag th:each="item : ${list}">`
  * angular : only html : `<div ng-repeat="itm in list">{{itm}}</div>` ; `{{expr|filter}}`
* specific templating language
  * velocity java : `$expr` ; `#set($foo=code)` `#if()` `#foreach(itm in list)` `#else` `#end` ; `## com` ; `#* mlcom *#` ; excl `#[[...]]#`
  * stringtemplate java : loop using subtemplates ; `<expr>` `<ope()>` `<expr:ope()>` `<list:templateX()>` `<it>` `<i>` `<if()>` `<elseif()>` `<else>` `<endif>` `<! comment !>` ; can use `<..>`or `$...$` 
  * freemarker java `${expr}` `<#-- -->` `<#if expr>` `<#else>` `</#if>` `<#list list as item>` `</#list>` `<#include "file">`
  * xpand java eclipse on emf model ; loop using subtemplate ; &laquo;expr&raquo; &laquo;EXPAND template FOREACH list&raquo; &laquo;DEFINE template FOR type&raquo; &laquo;ENDDEFINE&raquo;
  * macro processors : c preprocessor, m4
  * cheetah python : `$expr` `#for $itm in $list` `#end for` `#if` `#else if` `#else` `#end if` `## com` `#* mlcom *#`
  * django python `{{expr}}` `{{expr|filter}}` ; `{%ope%}` : `{%for itm in list%}` `{%endfor%}` `{%if expr%}` `{%else%}` `{%endif%}` `{%include ...%}` `{%block%}` `{%endblock%}`
    * Jinja python
    * liquid ruby (jekyll)
    * swig js
  * mustache multi : `{{expr}}` ; no code logic, sections when checking boolean and lists  `{{#list}}` `{{/list}}` , invert `{{^bool}}`, comment `{{!bla}}` `{{!--blabla--}}`
    * handlebars js 2010 : add control flow ope `{{#if}}` `{{#else}}` `{{/if}}` `{{#each list}}` `{{/each}}` ; can define its own opes
    * hogan js : fast mustache compiler, also command line node.js

http://en.wikipedia.org/wiki/Comparison_of_web_template_engines
http://en.wikipedia.org/wiki/Web_template_system

engines from Play (java)

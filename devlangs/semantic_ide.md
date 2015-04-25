# Semantic IDE

Let the IDE render the language in various ways to accommodate each ones personal flavours, 
with a single possible syntax behind, human readable and source control friendly.

Facts :
* All development languages have a human understandable and IDE supported textual syntax, behind which lied a semantic 
retrieved by both the compiler/interpreter and the IDE to do their respective jobs.
* Many peoples have different ways to quickly understand a program : may need space and keywords, or instead compacity and rich characters set
  * for each item within list do ... end for ; for(item : list){...}
  * ex: CoffeeScript has exact same semantic as Javascript but a completely different syntax to better fit some developers needs
* Differences in syntax usage may lead to changes in code history whereas the semantic is the same.
  * also reordered code blocks
* many language construct are syntax sugar, many languages evolutions are about syntax sugar (to reduce code size while keeping understandability)
* Some quality tools check syntax stuff to ensure maintainability (checkstyle, stylecop) : naming rules, positioning
  * some languages use naming conventions to host semantic (usually a prefix : $ @ _ get set uppercase)
* Quality tools implement checks to avoid known risks or discripencies authorized by the language
* Errors may be due to the syntax itself, most are catched by the IDE, then the compiler/interpreter.
* some languages use meta-programming to allow developers to implement their own syntax sugar and simplified way to do complex stuff
* Various syntax styles and keywords exists without semantic differences : 
  * curly brackets { } : c, perl, java, javascript, php, c#
  * begin end: pascal, vb, ruby
  * newline matters
  * indentation matters (off-side rule): python, coffeescript, yaml (anyway all languages allows indentation for readability)
  * parenthesis heaven (all is expression): lisp, clojure

Language syntax :
* Define a language with a rigid syntax : a unique way to represent a semantic tree
 * a semantic tree must lead to a single possible syntaxic representation
 * used stuff must appear after user stuff (higher level first), or other way, but choose a way
* This syntax must be human understandable, and allow easy history diff (by rows, inner row)
* use english for keywords
* Should use row by row and forced indentation
* Should be easily parseable (build the semantic tree in simple forward mode)
* Should finely represent both code logic and data structures
* comments and code disabling as first class feature
* semantic: contain state of the art features : object & functional, no null exception, integrated async/actor
* bonus : could generate to existing languages, and support completion for various ABI/IDL systems
  * at least java/c#/javascript (like the Fantom language), possibly ruby & python also, maybe go, should try "modern" ones like kotlin, ceylon, scala
  * although it is not realistic because of debug needs, but a good demonstration of capabilities

IDE :
* Provide an IDE capable to render/edit the semantic tree in various ways/styles as fit the developer
  * brackets or begin/end or lisp, indent size, multiple instructions on same line if simple
  * keywords in user's language
  * syntax sugar for specific concepts, or keep detailled syntax
  * visual programming : with boxes (shapes) and lines
* Web based IDE to be quickly usable on the web (cloud), but also local desktop tool
  * should be handleable with keyb only (on laptop/desktop with efficient keyboard)
  * may be also a finger version for tablets/smartphones ?

History :
* 2003 : first formalization of this idea in a ppt, after many coding experiences in various languages
* 200x : try to experiment such semantic ide by defining AST models in c# and related syntax format
* 200x : also experiment as html/js
* 2015 : formalize in github

# What to have, and to avoid

## To have

* static type checking, with generics : typescript (denojs), python type hints
* null safety to avoid null ref exception : kotlin, ceylon, rust, swift, fsharp, fantom, csharp8 opt-in, eiffel6.4, self, dart2
  * by default vars cannot be null, special type for nullables, compiler requires safe nav on nullables
* safe navigation in nullable types : elvis operator : `v=obj?.atr` `v=arr?.[10]` ; default value if null : `v = a ?? default`
* functional stuff like immutable, closures, unions
* constrained multi-inheritance like mixins, traits
* data expressiveness for arrays and dicts, ex: (javascript)
* concise yet readable code
* DSL ??
* multi-runtimes : Java, .Net, Javascript ?? (Fantom)
* native contracts ??
* meta-programming ??

## To avoid

* checked exceptions (Java)
* multiple methods with same name (Java, C#), prefere default/named params
* dynamic type, not good for IDE & Factories, prefere infered type, unions and default/named params
* bare multi-inheritance (C++), prefere interface, mixins, traits

## Be curious

* cross platform : same lang/std lib to multiple runtimes : JVM, CLR, Js, ...
  * https://haxe.org : to js, java, c#, cpp, php, python, lua, nodejs sources, also swf and neko bytecodes
    * std lib to all targets : files, xml, json, http client, hashes, unicode, zip, sqlite ; ext libs on various targets
  * https://fantom.org : to JVM and Js, no more CLR
  * https://ide.onelang.io/ online transpiler of few code lines
  * https://github.com/pseudo-lang/pseudo transpiler of lang and stdlib to python, ruby, js, c#, go

# Overview of global history

```mygraph
Viewport 1000 1000

T 100 0 - 1960 
T 200 0 - 1970 
T 300 0 - 1980 
T 400 0 - 1990 
T 500 0 - 2000 
T 600 0 - 2010

Class vline L w:0 h:1000
L 100 0 vline
L 200 0 vline
L 300 0 vline
L 400 0 vline
L 500 0 vline
L 600 0 vline

Class hline L w:900 h:0
L 0 300 hline
L 0 700 hline

Class devtype T o:90 av:m ah:m
T 10 100 devtype Imperative
T 10 500 devtype Object
T 10 700 devtype Functional

Class lsta T 
Class ldyn T d:italic

T 10 10 lsta Fortran
T 10 10 lsta Algol
T 10 10 lsta Basic
```

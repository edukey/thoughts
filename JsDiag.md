# Web Diagramming

To interactively build diagram with connecting lines (moving boxes moves lines), a positioning algorithm, inner boxes, a bit like Visio.

Should be copy/paste to Office docs keeping diagram objects.

To overlap with a modeling library (and textual format) giving semantics, styles and reusability to boxes and lines.

Should be eligible to both interactive diagramming on HTML5 viewers, and server side generation (command line) ; supporting SVG (and VML for IE9-) should do the stuff, but not the Canvas api

## Vector libs

Low level vector lib, without "lines connecting boxes" semantic

- [Raphael.js](http://raphaeljs.com) : based on SVG (and VML), most used
- [SnapSvg](http://snapsvg.io) (svg only)
- [Paper.js](http://paperjs.org) (canvas based)
- Processing.js (canvas based)

## Box & Lines libs

- [JsPlumb](http://www.jsplumb.org) github 
- [JoinJS](http://www.jointjs.com) github, and Rappid diagraming toolkit to build editors
- [WireIt](http://neyric.github.io/wireit/docs/) github
- [JGraph/MxGraph](https://www.jgraph.com/javascript-graph-visualization-library.html) $
- [GoJS](http://gojs.net) $
- [MindFusion JsDiagram](http://www.mindfusion.eu/jsdiagram.html) $
- [Draw2D](http://draw2d.org) $
- [yWorks](http://www.yworks.com) $
- Ajax.org (dead?)
- Dracula (Raphael based)

## Charts libs with Graph

Charting libs, to visualize numbers, usually does not allow to manipulate shapes, but some of them doing graphs may still be used

- D3

## Web modelers

- LucidChart
- Gliffy
- yEd (yWorks)
- Draw.io (MxGraph)
- Google Drive, Office 365

## Enterprise Web modelers

- Casewise
- MEGA HOPEX
- SAG Aris
- Troux ?

## Web Tools

- plantuml : from text dsl ; only generates bitmaps ?
- yuml : from text dsl ; only generates bitmaps ?
- webseqdiag : from text dsl ; only generates bitmaps ?
- graphviz : from text dsl ; only generates bitmaps ?

## References

http://www.erp5.com/officejs/javascript-10.Flow.Chart

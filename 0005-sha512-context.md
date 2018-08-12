---
tab: none
title: SHA Functions in ConTeXt
layout: page
permalink: /0005/
---

Imagine that you have the following list of documents---which are part of the _ConTeXt Suite_---in a CSV file:

``` tex
\unexpanded\def\sha#1%
   {\begingroup\tt
    \sethyphenationfeatures[sha]%
    \setuphyphenation[method=traditional]%
    #1%
    \endgroup}
```

```
"About \LuaTeX\ and \ConTeXt";"about.pdf"
"l2r, r2l: A Few Tips";"bidi.pdf"
"Flowcharts";"charts-mkiv.pdf"
"\ConTeXt\ Lua Documents";"cld-mkiv.pdf"
"Coloring \ConTeXt: Explaining \LuaTeX\ and MkIV";"colors-mkiv.pdf"
"Columns";"columnsets.pdf"
"It’s in the Details";"details.pdf"
;
;
"Exporting XML and ePub from \ConTeXt";"epub-mkiv.pdf"
"MkIV Hybrid Technology";"hybrid.pdf"
"Languages in \ConTeXt: Explaining \LuaTeX\ and MkIV";"languages-mkiv.pdf"
"Libraries in \ConTeXt";"libraries-mkiv.pdf"
"Lua: The \ConTeXt\ Libraries";"lua-mkiv.pdf"
"\LuaTeX\ Reference Manual";"luatex.pdf"
"\ConTeXt\ Mark IV: An Excursion";"ma-cb-en.pdf"
"Math";"math-mkiv.pdf"
"\MetaFun: \ConTeXt\ MkIV";"metafun-p.pdf"
;
"Bibliographies: The \ConTeXt\ Way";"mkiv-publications.pdf"
"\ConTeXt\ MKII – MKIV: The History of \LuaTeX";"mk.pdf"
;
"MathML";"mmlprime.pdf"
"Read Me First";"mreadme.pdf"
"Nodes";"nodes.pdf"
"Why Not Now";"notnow.pdf"
"On and On";"onandon.pdf"
"Pages";"pagecolumns.pdf"
"Rules: A \ConTeXt\ MkIV Manual";"rules-mkiv.pdf"
"Spacing in \ConTeXt";"spacing-mkiv.pdf"
"Simple Spreadsheets: \ConTeXt\ MkIV";"spreadsheets-mkiv."
"SQL in \ConTeXt";"sql-mkiv.pdf"
"Steps: \ConTeXt\ MkIV";"steps-mkiv.pdf"
"Still Going On";"still.pdf"
"SwigLib Basics";"swiglib-mkiv.pdf"
"LMX Templates";"templates-mkiv.pdf"
;
"Tools: luatools, mtxrun, context";"tools-mkiv.pdf"
"Units: \ConTeXt\ MkIV";"units-mkiv.pdf"
"Workflow Support in \ConTeXt";"workflows-mkiv.pdf"
"Dealing with XML in \ConTeXt\ MkIV";"xml-mkiv.pdf"
"Extreme Tables: \ConTeXt\ MkIV";"xtables-mkiv.pdf"
```
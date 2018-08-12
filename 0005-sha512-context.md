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

``` tex
\enabledirectives[backend.date=no]
\enabledirectives[backend.xmp=no]

\startluacode
function document.addfunnyhyphen(tfmdata)
    local underscore = utf.byte("_")
    local char       = tfmdata.characters[underscore]
    if not char then return end
    tfmdata.characters[0xFE000]   = {
        width    = 0,
        height   = 0,
        depth    = 0,
        commands = {
            { "right", -char.width },
            { "down", char.depth },
            { "slot", 1, underscore },
        }
    }
end


utilities.sequencers.appendaction("aftercopyingcharacters",
"after","document.addfunnyhyphen")

local shared = {
    start  = 1,
    length = 1,
    before = utf.char(0xFE000),
    after  = nil,
    left   = false,
    right  = false,
}

local all = table.setmetatableindex({ }, function(t,k)
    return shared
end)

languages.hyphenators.traditional.installmethod("sha",
    function(dictionary,word,n)
        return all
end
)

function document.capture(cmd, raw)
    local f = assert(io.popen(cmd, 'r'))
    local s = assert(f:read('*a'))
    f:close()
    if raw then return s end
    s = string.gsub(s, '^%s+', '')
    s = string.gsub(s, '%s+$', '')
    s = string.gsub(s, '[\n\r]+', ' ')
    return s
end

function document.sha256(file)
    command_output= document.capture("sha256sum -b " .. file)
    context(command_output:sub(0,64))
end

function document.sha512(file)
    command_output= document.capture("sha512sum -b " .. file)
    context(command_output:sub(0,128))
end
\stopluacode

\definehyphenationfeatures
   [sha]
   [characters=all,
    alternative=sha,
    righthyphenchar="FE000]

\unexpanded\def\sha#1%
   {\begingroup\tt
    \sethyphenationfeatures[sha]%
    \setuphyphenation[method=traditional]%
    #1%
    \endgroup}

\def\shatwo#1{\ctxlua{document.sha256("#1")}}
\def\shafive#1{{\tt\ctxlua{document.sha512("#1")}}}

\doif{\luaversion}{5.3}{\ctxlua{require("util-sha")}}

\def\hashtwofile#1{%
    \ctxlua{context(utilities.sha2.hash256(io.loaddata("#1")))}}

\def\hashfivefile#1{%
    \ctxlua{context(utilities.sha2.hash512(io.loaddata("#1")))}}

\setupinteraction[state=start, color=, style=, contrastcolor=]
\setupinteractionscreen[option={portrait, attachment}]

\usemodule[handlecsv]

\opencsvfile{context-documents.csv}
\removeemptylines

\setupbodyfont[times]

\starttext
\title{Some Special \ConTeXt\ Documents}
\startbuffer[item-file]
\doifelse{\luaversion}{5.3}
    {\item {\em\cA} \doiffile{\cB}{\attachment[title=\cA, name={\zeroedlineno-\cB}, file={\cB}, subtitle={SHA256: \hashtwofile{\cB}}]}\stopmode, con marca SHA512:}
    {\item {\em\cA} \doiffile{\cB}{\attachment[title=\cA, name={\zeroedlineno-\cB}, file={\cB}, subtitle={SHA256: \shatwo{\cB}}]}, with SHA512:}
\doifelse{\luaversion}{5.3}
    {\doiffileelse{\cB}{\sha{\hashfivefile{\cB}}}{{\ssbf\WORD{\color[red]{\\attachment\\is missing}}}}.}
    {\doiftextelse{\sha{\shafive{\cB}}}{\sha{\shafive{\cB}}}{{\ssbf\WORD{\color[red]{\\attachment\\is missing}}}}.}
\stopbuffer
\startitemize[n]
\doloopif{\cB}{~=}{}{\getbuffer[item-file]}
\stopitemize
\stoptext
```
BXdvidriver Package
===================

LaTeX: To specify a driver option effective only in DVI output

This single-function package enables authors to specify a global
driver option (dvips, dvipdfmx, etc) which is applied only when the
engine outputs a DVI file. It is useful to create special document-
templates that can be compiled in both PDF-mode and DVI-mode.

### System requirement

  * TeX format: LaTeX.
  * TeX engine: Anything.
  * Dependent packages:
      - ifpdf, ifluatex, ifxetex, ifvtex
      - pdftexcmds

### Installation

  - `*.sty` → $TEXMF/tex/latex/BXdvidriver

### License

This package is distributed under the MIT License.

The bxdvidriver Package
-----------------------

### Package Loading

    \usepackage[<option>,...]{bxdvidriver}

The available options are described hereafter.

#### Driver options

The following driver options are available:

    dvips,xdvi,dvipdf,dvipdfm,dvipdfmx,dvipsone
    dviwindo,oztex,textures,pctexps,pctex32

Suppose the document begins with:

    \documentclass[a4paper]{article}
    \usepackage[dvipdfmx]{bxdvidriver}
    \usepackage{graphicx,color}

If the document is compiled with pdflatex (or xelatex, lualatex), then
the package does nothing and the driver option `dvipdfmx` is simply
ignored.

However, if the document is compiled with latex (or any other engine
that outputs DVI files), then the package adds the given driver option
`dvipdfmx` to the global option list, and makes the settings effectively
the same as the following:

    \documentclass[a4paper,dvipdfmx]{article}
    \usepackage{graphicx,color}

The driver option is globally in effect, and thus the packages graphicx
and color will choose the driver for dvipdfmx.

*Note.* Some care must be taken when the document class itself has some
driver-dependent behavior. In that case, simply loading bxdvidriver
after `\documentclass` would leave its driver option unapplied to the
document class. Instead, you must load the bxdvidriver package *before*
`\documentclass` with `\RequirePackage` command.

    \RequirePackage[dvipdfmx]{bxdvidriver}
    \documentclass[a4paper]{some-fancy-class}
    \usepackage{graphicx,color}

#### Other options

This package is essentially single-function, but as side effect it also
checks some integrity on driver settings:

  * whether (at most) one driver option is given;
  * whether the driver matches the (PDF-output) engine;
  * whether (at most) one graphics driver is loaded.

By default, an error is issued when any check fails. But the behavior
can be changed by options.

  * `check` (default): Check failure issues an error.
  * `nocheck`: Check failure does not issue an error.

### Usage

This package offers no user commands or environments. All the settings
are done by package options.

Revision History
----------------

  * Version 0.2a ‹2017/02/13›
      - Bug fix.
  * Version 0.2  ‹2016/03/26›
      - The first public version.

--------------------
Takayuki YATO (aka. "ZR")  
https://github.com/zr-tex8r

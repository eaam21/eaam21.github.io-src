Title: Installing Texmaker under Debian
Slug: installing-texmaker
Date: 2018-03-21 17:14:36
Tags: Latex
Category: software
Authors: Elías Alejandro

![alt text](http://www.xm1math.net/texmaker/assets/portfolio/structure.png "Texmaker")

What is Texmaker? According to [Texmaker](http://www.xm1math.net/texmaker/){:target="_blank"} website:
>Texmaker is a free, modern and cross-platform LaTeX editor for linux, macosx and windows systems 
>that integrates many tools needed to develop documents with LaTeX, in just one application.

It makes sense since we need to create documents using [LaTex](https://en.wikipedia.org/wiki/LaTex){:target="_blank"} format.

So to install Texmaker in Debian/Ubuntu you can follow the next instructions:

###Steps and troubleshooting
First all install Texmaker :)
```console
$ sudo aptitude install texmaker
```
*Note: you can use apt-get to install your package like: sudo apt-get install texmaker*

Ok, now I have a LaTex document and I'd like to create a pdf file. You can open your LaTex document
(with TexMaker obviously :) and then clik on the Right Arrow (Run). If you get an error message like

```console
! Package babel Error: You haven't specified a language option.
```
You need to install another package, in my case my document will be in Spanish then:

```console
$ sudo aptitude install tex-live-lang-spanish
```
Then try again to create the pdf file as we describe above. If you get an error message like:

```console
! LaTeX Error: File `siunitx.sty' not found.
```
You need to install texlive-science package

```console
$ sudo aptitude install texlive-science
```
Then try to create the pdf file. If you get an error message like:

```console
! LaTeX Error: File `biblatex.sty' not found.
```
Install texlive-bibtex-extra package

```console
$ sudo aptitude install texlive-bibtex-extra
```
Once again try to create the pdf file. But if you still get an error about 

```console
undefined sequence control..
\entry ...ata@\the \c@refsection @\blx@dlist@name
...
```
You should delete temporary files .aux, .bbl, .bcf and try again.


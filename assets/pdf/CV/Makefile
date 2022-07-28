#
# Makefile for acmart package
#
# This file is in public domain
#
# $Id: Makefile,v 1.10 2016/04/14 21:55:57 boris Exp $
#

SAMPLES = main.tex
LATEX   = pdflatex

SRC = ${wildcard src/*.tex}

main.pdf:  main.tex $(SRC)
	$(LATEX) main
	- bibtex main
	$(LATEX) main
	$(LATEX) main

clean:
	$(RM)  $(PACKAGE).cls *.log *.aux *.pdf \
	*.cfg *.glo *.idx *.toc \
	*.ilg *.ind *.out *.lof \
	*.lot *.bbl *.blg *.gls *.cut *.hd \
	*.dvi *.ps *.thm *.tgz *.zip *.rpi
FONTNAME=Evolventa
FONTFACES=$(FONTNAME)-Regular $(FONTNAME)-Bold $(FONTNAME)-Oblique $(FONTNAME)-BoldOblique
TTFDIR=../../ttf

all: manual.pdf websample.png

%.pdf: %.tex preamble.tex frontmatter.tex $(FONTFACES:%=$(TTFDIR)/%.ttf)
	lualatex $<
	lualatex $<

%.png: %.pdf
	pdftoppm -r 800 -scale-to-y -1 -singlefile -png $< $*

cleanint:
	rm -f *.aux *.log *.gz *.toc *.out

clean: cleanint
	rm -f *.pdf *.png

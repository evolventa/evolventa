###########################
# Common definitions
###########################

FONTNAME=Evolventa
FONTFACES=$(FONTNAME)-Regular $(FONTNAME)-Bold $(FONTNAME)-Oblique $(FONTNAME)-BoldOblique

TMPDIR=tmp
OTFDIR=../otf
TTFDIR=../ttf
WOFFDIR=../woff
COVERAGEDIR=../doc/coverage
MANUALDIR=../doc/manual

###########################
# Main targets
###########################

all: otf ttf woff coverage manual

otf: $(FONTFACES:%=$(OTFDIR)/%.otf)

ttf: $(FONTFACES:%=$(TTFDIR)/%.ttf)

woff: $(FONTFACES:%=$(WOFFDIR)/%.woff)

coverage: $(FONTFACES:%=$(COVERAGEDIR)/%.pdf)

manual:
	cd $(MANUALDIR) && $(MAKE)

cleanint:
	rm -rf $(TMPDIR)
	cd $(MANUALDIR) && $(MAKE) cleanint

clean: cleanint
	rm -rf $(OTFDIR)/*.otf
	rm -rf $(TTFDIR)/*.ttf
	rm -rf $(WOFFDIR)/*.woff
	rm -f $(COVERAGEDIR)/*.pdf
	cd $(MANUALDIR) && $(MAKE) clean

###########################
# Specific recipes
###########################

$(OTFDIR)/%.otf: %.sfd
	fontforge -script makefonts.ff $^ otf $@

$(TTFDIR)/%.ttf: $(TMPDIR)/%-nohint.ttf
	ttfautohint $^ $@

$(TMPDIR)/%-nohint.ttf: %.sfd | $(TMPDIR)
	fontforge -script makefonts.ff $^ ttf $@

$(WOFFDIR)/%.woff: $(TTFDIR)/%.ttf
	sfnt2woff $^
	mv $(TTFDIR)/*.woff $(WOFFDIR)

$(COVERAGEDIR)/%.pdf: $(OTFDIR)/%.otf
	fntsample -f $^ -o $@

$(TMPDIR):
	mkdir -p $(TMPDIR)

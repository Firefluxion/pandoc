BUILDDIR=build
FILENAME=essay

pdf: pdf-print pdf-test-engine pdf-ereader

pdf-ereader:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars+raw_tex \
	--to=latex \
	--output=$(BUILDDIR)/$(FILENAME)-ereader.pdf \
	--pdf-engine=xelatex \
	--include-in-header="layout/ereader.tex"

pdf-print:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars+raw_tex \
	--to=latex \
	--output=$(BUILDDIR)/$(FILENAME)-print.pdf \
	--pdf-engine=xelatex \

pdf-test-engine:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars+raw_tex \
	--to=latex \
	--output=$(BUILDDIR)/$(FILENAME)-test-engine.pdf \
	--pdf-engine=xelatex \
	--toc \
	-N \
	--toc-depth=2 \

html:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars \
	--to=html5 \
	--output=$(BUILDDIR)/$(FILENAME).html \
	--mathjax \
	--standalone

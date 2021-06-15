BUILDDIR=output
FILENAME=linux-server-documentation.md

pdf: pdf-print pdf-test-engine pdf-ereader

pdf-ereader:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars+raw_tex \
	--to=latex \
	--output=$(BUILDDIR)/$(FILENAME)-ereader.pdf \
	--pdf-engine=xelatex \
	--include-in-header="layout/ereader.tex" \
	--resource-path=Images

pdf-print:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	-F pandoc-crossref \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars+raw_tex \
	--to=latex \
	--output=$(BUILDDIR)/$(FILENAME)-test-engine.pdf \
	--pdf-engine=xelatex \
	--toc \
	-N \
	--toc-depth=2 \
	--resource-path=Images


pdf-test-engine:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	--filter pandoc-crossref \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars+raw_tex \
	--output=$(BUILDDIR)/$(FILENAME)-test-engine.pdf \
	--number-sections \
	--pdf-engine=lualatex \
	-V papersize=a4paper \
	-V geometry:margin=2.5cm \
	-V lang=de-DE \
	-V fontsize=12pt \
	-V breakurl \
	-V hyphens=URL \
	-V colorlinks \
	--include-in-header="layout/disable_float.tex" \
	--include-in-header="layout/mainfont_arial.tex" \
	--resource-path=Images

html:
	mkdir $(BUILDDIR) -p
	pandoc $(FILENAME) \
	--citeproc \
	--from=markdown+tex_math_single_backslash+tex_math_dollars \
	--to=html5 \
	--output=$(BUILDDIR)/$(FILENAME).html \
	--mathjax \
	--standalone \
	--resource-path=Images

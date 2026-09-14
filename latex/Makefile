MAIN := Thesis.tex
PDF := Thesis.pdf
TINYTEX_BIN := $(HOME)/.TinyTeX/bin/x86_64-linux

ifneq ($(wildcard $(TINYTEX_BIN)/latexmk),)
export PATH := $(TINYTEX_BIN):$(PATH)
endif

LATEXMK ?= latexmk

.PHONY: all pdf check watch clean distclean doctor

all: pdf

pdf:
	$(LATEXMK) -pdf -interaction=nonstopmode -halt-on-error -file-line-error $(MAIN)

check: doctor pdf
	test -s $(PDF)
	@echo "OK: $(PDF) built successfully"

doctor:
	@command -v $(LATEXMK) >/dev/null || { echo "latexmk not found"; exit 1; }
	@command -v pdflatex >/dev/null || { echo "pdflatex not found"; exit 1; }
	@command -v biber >/dev/null || { echo "biber not found"; exit 1; }

watch:
	$(LATEXMK) -pdf -pvc -interaction=nonstopmode -file-line-error $(MAIN)

clean:
	$(LATEXMK) -c $(MAIN)

distclean:
	$(LATEXMK) -C $(MAIN)
	rm -f $(PDF)

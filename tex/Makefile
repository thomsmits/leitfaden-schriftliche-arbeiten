TEMP_DIR = ../temp
RESULT_DIR = ../result
LATEX = pdflatex
BIBTEX = biber
MAKEINDEX = makeindex


define latex-it
$(eval FILE = $(firstword $^))
@echo "Building $(FILE)"
@$(LATEX) -draftmode -output-directory=$(TEMP_DIR) $(FILE)
@cd $(TEMP_DIR) ; $(BIBTEX) $(basename $(FILE))
@cd $(TEMP_DIR) ; $(MAKEINDEX) $(basename $(FILE)).idx
@$(LATEX) -draftmode -output-directory=$(TEMP_DIR) $(FILE) > /dev/null
@$(LATEX) -draftmode -output-directory=$(TEMP_DIR) $(FILE) > /dev/null
@$(LATEX) -output-directory=$(TEMP_DIR) $(FILE)
endef


all: $(TEMP_DIR) $(RESULT_DIR) \
		$(RESULT_DIR)/Leitfaden_schriftliche_Arbeiten.pdf

clean:
	rm -rf $(TEMP_DIR)

$(TEMP_DIR)/Leitfaden_schriftliche_Arbeiten.pdf: Leitfaden_schriftliche_Arbeiten.tex
	cp sources.bib $(TEMP_DIR)
	$(latex-it)

$(RESULT_DIR)/Leitfaden_schriftliche_Arbeiten.pdf: $(TEMP_DIR)/Leitfaden_schriftliche_Arbeiten.pdf
	@cat $< > $@

$(TEMP_DIR):
	mkdir $(TEMP_DIR)

$(RESULT_DIR):
	mkdir $(RESULT_DIR)

.PHONY: clean all

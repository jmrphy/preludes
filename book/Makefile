##################################
# Some Makefile generator script #
##################################

# Directories
SOURCE := source
BUILD_DIR := build
TEMPLATES := templates
BIB := /Users/justin/Dropbox/global_files/mybib.bib

# doc settings
TITLE := "Preludes to a Science of Insurrection"
## Justin Murphy"
## Justin Murphy"
#DATE := $(date +%d.%m.%Y)
AUTHOR := "Justin Murphy"

## Markdown extension (e.g. md, markdown, mdown).
MEXT := md

MARKDOWN := $(wildcard $(SOURCE)/*.$(MEXT))
PDF := $(patsubst %.$(MEXT), %.pdf, $(subst $(SOURCE), $(BUILD_DIR), $(MARKDOWN))) 
TEX := $(patsubst %.$(MEXT), %.tex, $(subst $(SOURCE), $(BUILD_DIR), $(MARKDOWN)))

# second line is the link to your bib file.
CSL := chicago-fullnote-bibliography-no-ibid

all:	checkdirs pdf tex

checkdirs: $(BUILD_DIR)

# create build dir if not exists
$(BUILD_DIR):
	@mkdir -p $@

pdf: clean $(PDF)

tex: clean $(TEX)

$(BUILD_DIR)/%.pdf: $(SOURCE)/%.md
	cat $< | pandoc -r markdown+simple_tables+table_captions+yaml_metadata_block \
		-s -S --latex-engine=xelatex \
		--toc \
		--template=$(TEMPLATES)/xelatex.template \
		--filter pandoc-citeproc \
		--csl=./csl/$(CSL).csl \
		-Vtitle=$(TITLE) -Vauthor=$(AUTHOR) \
		--bibliography=$(BIB) -o $@
	open $@

$(BUILD_DIR)/%.tex: $(SOURCE)/%.md
	cat $< | pandoc -r markdown+simple_tables+table_captions+yaml_metadata_block \
		-s -S --latex-engine=xelatex \
		--toc \
		--template=$(TEMPLATES)/xelatex.template \
		--filter pandoc-citeproc \
		--csl=./csl/$(CSL).csl \
		-V title=$(TITLE) \
		--bibliography=$(BIB) -o $@

clean:
	rm -f ./$(BUILD_DIR)/*

.PHONY: all clean pdf tex checkdirs

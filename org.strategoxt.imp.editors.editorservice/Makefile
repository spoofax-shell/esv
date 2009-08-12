SYNTAX     = EditorService
SOURCE     = ../org.strategoxt.imp.generator/src/syntax/$(SYNTAX).def
PPAF       = ../org.strategoxt.imp.generator/src/syntax/$(SYNTAX)-pretty.pp.af

SDF2IMP    = ../org.strategoxt.imp.generator/sdf2imp
ESVS       = ${wildcard src/*.esv}

all : include/$(SYNTAX).packed.esv include/rtg.tbl include/EditorService-pretty.pp.af

clean :
	rm -f src/parser/$(SYNTAX)ParseController.java bin/$(SYNTAX).packed.esv
	rm -rf src/parser/ast
	# ...

include/$(SYNTAX).packed.esv : $(SYNTAX).def include/$(SYNTAX).tbl $(SDF2IMP) Makefile $(ESVS)
	$(SDF2IMP) -i $< -p $(SYNTAX).tbl -m $(SYNTAX) --verbose 2

$(SYNTAX).def : $(SOURCE)
	ln -s $< $@

include/$(SYNTAX).tbl : $(SYNTAX).def
	[ -e include ] || mkdir include
	sdf2table -i $< -o $@ -m $(SYNTAX)

# We need a better solution for this
include/EditorService-pretty.pp.af : $(PPAF)
	cp $< $@

include/rtg.tbl : ~/.nix-profile/share/sdf/stratego-regular/rtg.tbl
	baf2trm  -i $< -o $@ # cp $< $@

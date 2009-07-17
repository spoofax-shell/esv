SYNTAX     = EditorService
SOURCE     = ../org.strategoxt.imp.metatooling/src/syntax/$(SYNTAX).def
PPAF       = ../org.strategoxt.imp.metatooling/src/syntax/$(SYNTAX)-pretty.pp.af
CTREE      = ../org.strategoxt.imp.metatooling/src/include/sdf2imp.ctree

SDF2IMP    = ../org.strategoxt.imp.metatooling/sdf2imp
ESVS       = ${wildcard src/*.esv}

all : editor/include/$(SYNTAX).packed.esv $(CTREE) editor/include/rtg.tbl editor/include/EditorService-pretty.pp.af
	cp $(CTREE) editor/include

clean :
	rm -f src/parser/$(SYNTAX)ParseController.java bin/$(SYNTAX).packed.esv
	rm -rf src/parser/ast
	# ...

editor/include/$(SYNTAX).packed.esv : $(SYNTAX).def editor/include/$(SYNTAX).tbl $(SDF2IMP) Makefile $(ESVS)
	$(SDF2IMP) -i $< -p $(SYNTAX).tbl -m $(SYNTAX) --verbose 2

$(SYNTAX).def : $(SOURCE)
	ln -s $< $@

editor/include/$(SYNTAX).tbl : $(SYNTAX).def
	[ -e editor/include ] || mkdir editor/include
	sdf2table -i $< -o $@ -m $(SYNTAX)

# We need a better solution for this
editor/include/EditorService-pretty.pp.af : $(PPAF)
	cp $< $@

editor/include/rtg.tbl : ~/.nix-profile/share/sdf/stratego-regular/rtg.tbl
	baf2trm  -i $< -o $@ # cp $< $@

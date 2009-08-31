SYNTAX     = EditorService
SOURCE     = ../org.strategoxt.imp.generator/src/syntax/$(SYNTAX).def
PPAF       = ../org.strategoxt.imp.generator/src/syntax/$(SYNTAX)-pretty.pp.af

SDF2IMP    = ../org.strategoxt.imp.generator/sdf2imp
STRJAR     = `strj-jar -p || echo strategoxt.jar`
ESVS       = ${wildcard src/*.esv}

all : include/$(SYNTAX).packed.esv include/rtg.tbl include/EditorService-pretty.pp.af

clean :
	rm -f src/parser/$(SYNTAX)ParseController.java bin/$(SYNTAX).packed.esv
	rm -rf src/parser/ast
	# ...

include/$(SYNTAX).packed.esv : $(SYNTAX).def $(SDF2IMP) Makefile $(ESVS)
	$(SDF2IMP) -i $< -pn org.strategoxt.imp.editors.editorservice -m $(SYNTAX) --verbose 2
	rm build.xml ".externalToolBuilders/Ant Builder.launch"

# We need a better solution for this
include/EditorService-pretty.pp.af : $(PPAF)
	cp $< $@

include/rtg.tbl : ~/.nix-profile/share/sdf/stratego-regular/rtg.tbl
	baf2trm -i $< -o $@ # workaround for some BAFReader issue(?)

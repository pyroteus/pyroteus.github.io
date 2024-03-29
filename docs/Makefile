# Minimal makefile for Sphinx documentation

# You can set these variables from the command line.
SPHINXOPTS    =
SPHINXBUILD   = sphinx-build
SPHINXAPIDOC  = sphinx-apidoc
SPHINXPROJ    = Documentation
SOURCEDIR     = source
BUILDDIR      = build
PYTHON        = ${VIRTUAL_ENV}/bin/python3

ANIMATE       = ${VIRTUAL_ENV}/src/animate
MOVEMENT      = ${VIRTUAL_ENV}/src/movement
GOALIE        = ${VIRTUAL_ENV}/src/goalie


# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: help Makefile clean

GENERATED_FILES = source/demos

.PHONY: copy_demos

run_animate_demos:
	for file in ${ANIMATE}/demos/*.py; do \
		cd  ${ANIMATE}/demos/ && \
		${PYTHON} $$file ; \
	done; \
	cd . \

run_movement_demos:
	for file in ${MOVEMENT}/demos/*.py; do \
		cd  ${MOVEMENT}/demos/ && \
		${PYTHON} $$file ; \
	done; \
	cd . \

run_goalie_demos:
	for file in ${GOALIE}/demos/*.py; do \
		cd  ${GOALIE}/demos/ && \
		${PYTHON} $$file ; \
	done; \
	cd . \

source/demos: copy_demos

copy_demos:
	install -d source/demos
	cp ${ANIMATE}/demos/*.py source/demos
	cp ${ANIMATE}/demos/*.jpg source/demos
	cp ${MOVEMENT}/demos/*.py source/demos
	cp ${MOVEMENT}/demos/*.jpg source/demos
	cp ${MOVEMENT}/demos/demo_references.bib source/demos
	cp ${GOALIE}/demos/*.py source/demos
	cp ${GOALIE}/demos/*.jpg source/demos
	cat ${GOALIE}/demos/demo_references.bib >> source/demos/demo_references.bib
	for file in source/demos/*.py; do pylit -c $$file; mv $$file.txt $$file.rst; done
	install -d $(BUILDDIR)/html/demos
	cp source/demos/*.py $(BUILDDIR)/html/demos
	cp source/demos/*.jpg $(BUILDDIR)/html/demos
	cp source/demos/*.bib $(BUILDDIR)/html/demos
	install -d $(BUILDDIR)/html/animate
	install -d $(BUILDDIR)/html/movement
	install -d $(BUILDDIR)/html/goalie
	mkdir -p $(BUILDDIR)/html/_images
	cp source/animate/images/*.jpg $(BUILDDIR)/html/_images
	# cp source/movement/images/*.jpg $(BUILDDIR)/html/_images
	cp source/goalie/images/*.jpg $(BUILDDIR)/html/_images

SPHINX_TARGETS = dirhtml singlehtml pickle json htmlhelp qthelp devhelp epub \
	latex latexpdf latexpdfja text man texinfo info gettext changes \
	xml pseudoxml linkcheck doctest coverage

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
$(SPHINX_TARGETS): Makefile
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

html: apidoc $(GENERATED_FILES)
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
	cp -r $(BUILDDIR)/html/* ..

.PHONY: apidoc


clean:
	-git clean -fdx $(BUILDDIR)/html/
	-rm -rf $(BUILDDIR)/doctrees
	-rm -rf $(GENERATED_FILES)

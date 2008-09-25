%.html : %.txt ;
	asciidoc -b xhtml11 $^

%.gz : %.txt ;
	asciidoc -d manpage -b docbook $^
	xsltproc -nonet /usr/share/xml/docbook/stylesheet/nwalsh/manpages/docbook.xsl `echo $^ |sed -e 's/.txt/.xml/'` >/dev/null
	# ugly hack to avoid '.sp' at the end of a sentence or paragraph:
	sed -i 's/\.sp//' `echo $^ |sed -e 's/.txt//'`
	gzip -f --best `echo $^ |sed -e 's/.txt//'`

MANPAGES = git-last.1 git-publish-branch.1 git-rank-contributors.1 git-wtf.1


all: doc

doc: doc_man doc_html
doc_html: $(addsuffix .html, $(MANPAGES))
doc_man: $(addsuffix .gz, $(MANPAGES))

clean:
	@for i in $(MANPAGES); do \
		rm -f $$i.html $$i.xml $$i.gz; done



default:notes.pdf

notes.pdf:notes.md
	pandoc notes.md -o notes.pdf --template data/eisvogel-template.tex -N --include-in-header data/header.tex --filter pandoc-citeproc --top-level-division=chapter

clean :
	rm notes.aux notes.log notes.nav notes.out notes.snm notes.tex notes.toc

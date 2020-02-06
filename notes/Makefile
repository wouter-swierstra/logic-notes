
default:notes.pdf

verbose:notes.md
	pandoc notes.md -o notes.pdf --pdf-engine=xelatex --verbose --template eisvogel-template.tex --include-in-header=header.tex


notes.pdf:notes.md
	pandoc notes.md -o notes.pdf --pdf-engine=xelatex --template eisvogel-template.tex --include-in-header=header.tex -N --top-level-division=chapter


tex : notes.md
	pandoc notes.md -o notes.tex --pdf-engine=xelatex --verbose --template eisvogel-template.tex --include-in-header=header.tex

clean :
	rm notes.aux notes.log notes.nav notes.out notes.snm notes.tex notes.toc

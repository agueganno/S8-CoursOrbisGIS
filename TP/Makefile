all: pdf clean

pdf: slides.tex
	@echo "Génération du PDF"
	@pdflatex slides.tex
	@pdflatex slides.tex

handouttex: slides.tex
	@sed -i slides.tex -e 's/t,french/t,french,handout/'

handout: handouttex pdf

slides.tex: plan.rst
	@echo "Génération du fichier tex"
	@rst2beamer --title="S8SIG" \
		--language="fr" \
		--centerfigs="True" \
		plan.rst > slides.tex
	@echo "Conversion en utf8"
	@iconv -f ISO8859-1 -t UTF-8 -o slides-utf.tex slides.tex
	@mv slides-utf.tex slides.tex
	@sed -i slides.tex -e 's/latin1/utf8/'
	@echo "Tweaks d'affichage"
	@sed -i slides.tex -e '/\usetheme/ a\
	\\usecolortheme{seahorse}'
	@sed -i slides.tex -e 's/| alert@\++//g'
	@sed -i slides.tex -e '/\end{itemize}\
	\includegraphics/ a\
	\\pause{}'
	@sed -i slides.tex -e '/\includegraphics/ i\
	\\begin{center}'
	@sed -i slides.tex -e '/\includegraphics/ a\
	\\end{center}'
	@echo "Ajout de blocs"
	@sed -i slides.tex -e '/\\frametitle/ a\
	\\begin{block}{}'
	@sed -i slides.tex -e '/\end{frame}/ i\
	\\end{block}'
	@echo "Ajout d'informations"
	@sed -i slides.tex -e 's/^Initiation à la progr - dummy title//'
	@sed -i slides.tex -e '/\date/ a\
	\\title{Initiation à la programmation spatiale sous OrbisGIS}'
	@sed -i slides.tex -e 's/author{}/author{Alexis \\textsc{Guéganno} \\and Jean-Yves \\textsc{Martin}}/'
	@sed -i slides.tex -e 's/date{}/date{9 février 2012}/'


clean:
	@echo "Nettoyage des fichiers temporaires"
	@rm slides.tex
	@rm slides.aux
	@rm slides.log
	@rm slides.nav
	@rm slides.out
	@rm slides.snm
	@rm slides.toc
	@rm slides.vrb

mrproper: clean
	@echo "Suppression du fichier PDF"
	@rm slides.pdf



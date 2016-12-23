# Requirements
 - [pandoc](https://github.com/jgm/pandoc/releases/tag/1.19.1) 
 - any latex engine. For windows I recommend [miktex](https://miktex.org/download). You can build this for other OS but I haven't tried that.
# Latex packages
Im not sure about this but I think you need to install these packages to your latex engine. 
If youre using miktex you can use the *MiktexPackage Installer* which is installed once you install miktex (for different engines there is also a package installer ussualy)
 - *ragged2e* for hyphenated left align
 - *sourceserifpro*, *sourcesanspro*, *sourcecodepro* for adobe x pro fonts
# Usage
Just replace the markdown files on input/ with your own. 
If you put all parts of the proposal in one markdown its okay just replace the filename. 
And then run this on a terminal:
```
pandoc -f markdown -t latex plaintexts/introduction.md plaintexts/"related work.md" plaintexts/"research questions.md" plaintexts/methodology.md plaintexts/conclusion.md plaintexts/references.md -o proposal.pdf --template=styles/template.tex --bibliography=plaintexts/references.bib --csl=styles/apa.csl -V documentclass=report -V mainfont=SourceSerifPro -V sansfont=SourceSansPro -V fontfamily=SourceSerifPro --toc
```
#Notes
 - Make sure you put hard linebreaks on your markdown for every new paragraph. 
 - Pandoc doesn't work if your md is ANSI just set it to UTF-8.
 - I will update this once i integrate the abstract.
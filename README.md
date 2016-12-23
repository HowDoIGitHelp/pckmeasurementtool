# Requirements
 - [pandoc](https://github.com/jgm/pandoc/releases/tag/1.19.1) 
 - any latex engine. For windows I recommend [miktex](https://miktex.org/download). You can build this for other OS but I haven't tried that.
 
# Latex packages
Im not sure about this but I think you need to install these packages to your latex engine. 
If youre using miktex you can use the *MiktexPackage Installer* which is installed once you install miktex (for different engines there is also a package installer usualy)
 - *ragged2e* for hyphenated left align
 - *sourceserifpro*, *sourcesanspro*, and *sourcecodepro* for adobe x pro fonts
If you cant find the packages they might be preinstalled already so just leave it be.
 
# Usage
Just replace the markdown files on plaintexts/ with your own. 
If you put all parts of the proposal in one markdown its okay just replace the filename. 
And then run this on a terminal:
```
pandoc -f markdown -t latex plaintexts/abstract.md plaintexts/introduction.md 
plaintexts/"related work.md" plaintexts/"research questions.md" 
plaintexts/methodology.md plaintexts/conclusion.md plaintexts/references.md 
-o proposal.pdf --template=styles/template.tex 
--bibliography=plaintexts/references.bib --csl=styles/apa.csl 
-V documentclass=report -V mainfont=SourceSerifPro -V sansfont=SourceSansPro -V fontfamily=SourceSerifPro --toc
```
 
#Notes
 - Make sure you put hard linebreaks on your markdown for every new paragraph. 
 - Pandoc doesn't work if your md is ANSI just set it to UTF-8.
 - references.md is just there to create the section heading
 - if you are just using one file for all just add an new heading "#References"
 - in your '#Abstract' section header, change it to '#Abstract {.unnumbered} so that walay chapter number
 - The template.tex was adapted form [tompollard's phd_thesis_markdown](https://github.com/tompollard/phd_thesis_markdown)

# Related Work
## Theoretical Perspectives
### Genes, Proteins and Function Expressions
The central dogma of molecular biology explains the how genetic information flows within a biological system [@Crick1958].
This idea was first stated by one of the co-discoverers the structure of a the DNA, Francis Crick.
The most simplistic description of the central dogma states that "DNA makes RNA and RNA makes protein" [@Leavitt2010].
The dogma is a framework that describes three general processes of biological sequential information transfers.

#### Replication
DNA replication is simply the processes that facilitate the reproduction of DNA sequences.
This process is essential since DNA information must be reproduced when the cell itself reproduces.

#### Transcription
This is the process in which DNA information in a particular section is replicated into another type of biological sequence information, the RNA.
There many biological process that facilitate the transcription of DNA to RNA but RNA is basically a copy of the information found in the DNA.
RNA serves as a middle man/messenger sequence between DNA and protein sequences.
This extra middle step is essential in the whole process as it protects the information located in the DNA.
Instead of subjecting DNA to the dangers of the process of translation, the RNA copy is used instead.

#### Translation
This process takes place after an RNA is transcripted from DNA.
An RNA makes its way to a ribosome, a cellular organelle that facilitates translation.
Using multiple enzymatic processes within the ribosome, RNA sequences of nucleoases (A,U,G,C) are translated into protein sequences of amino acids.
Every three nucleobases in the RNA has a corresponding translation to one of the 20 amino acids.
Starting from RNA, the translation process yields a protein sequence of amino acids.
These proteins are responsible for various biological functions that are expressed in organisms

The central dogma describes how genes (DNA) dictate an organism functions.
These processes show how any organism can be defined as a set of functions, a set of proteins and consequentially a sequence of genes.

### Essential and Non-essential Genes
Genes range from as few as 480 base pairs ,as shown by the bacterium *Mycoplasma genitalium*, to 100,000 to 150,000, as shown by multi-cellular eukaryotes like humans [@Koonin2000].
Not all of these genes are completely essential for the survival of an organism. Some of these genes are functionally redundant. Functionally redundant genes are two or more genes that share the same function when expressed. This means that only one of these genes is  needed for surviva. [@Koonin2000;@Nowak1997].
The concept of essential genes refer to the smallest set of genes which produces a fully functioning organism under the best conditions of living, that is, nutrients are abundant and stress is absent [@Koonin2000].
Researchers have considered the upper bound of the minimum set of genes to be 480 genes. This number is chosen as it is the number of genes of the bacterium *Mycoplasma genitalium*. *M. genitalium* is the organism with the smallest known genome [@Fraser1995 ].

### Core genome
One of the approaches for the determination of the minimal set of genes uses the concept of the core genome.
The core genome of a group of organisms refer to the set of genes shared by all organisms under said group of organisms.
This set of genes doesn't include genes that vary for other organisms in the same group  (genes that only contribute to the diversity of  said group of organisms) [@Tettelin2005; @Tettelin2008 ].
Since the core genome of a group of organisms consists of genes shared by multiple genomes, said core genome could be a good candidate for the minimal gene set.

## State of the Art
### Using the *Mycoplasma genitalium* bacteria
*Mycoplasma genitalium's* genome has been researchers' primary candidate for the core bacterial gene set.
It is widely accepted that the length of this bacterium's gene set is the upper bound for the bacterial genome [@Fraser1995].
Global transposon mutagenesis on *M. genitalium* is a well studied approach on the study of the minimal gene set. Trasposon mutagenesis is a process that allows gene segments to be transferred to another organism.
Because of the insertion of the introduced gene during transposon, the host organism (the owner of the interupted gene) experiences a mutation. By deliberately interrupting the host's chromosomes, researchers can infer information on the function of the hosts genes [@Hamer2001].
Hutchison III  et. al. (1996) used transposon mutagenesis on *M. genitalium's* genome along with its closest relative *M. pneumoniae* to identify which gene locations are essential and which are nonessential [@HutchisonIII1999].
The researchers did this by deliberately inserting extant genes to introduce mutations to *M. genitalium* and *M. pneumoniae* and studying the effects of these mutations to their survivability [-@HutchisonIII1999].
Their analysis suggests that 265 to 350 of the 480 protein-coding genes of *M. genitalium* are considered essential.

*M. genitalium's* gene sequence has also been used in the comparative genomics approach of the search for the minimal bacterial gene set.
Using protein sequence analysis, a bioinformatics approach of comparing sequences described by Koonin (1996), Musheigian and Koonin (1996) compared *M. genitalium* with *Haemophilus influenzae* and found 240 orthologs (genes with the same functions but not necessarily same sequences) [-@Mushegian1996 ].
This means that the two bacteria share a set of 256 gene functions.
Genes outside of the 256 orthologs can be considered non-essential genes since either bacterium can survive without them.

### Experimentally determined essential genes
DEG 10 (Database of Essential Genes) is a database of genes where their essentiality to survival is experimentally determined [@Zhang2009 ].
This database is an improved version of DEG 1.0, created 10 years ago.
It contains information about the essential genes, the experimental method used to determine their essentiality, and their associated references.
The most common experimental methods of confirming gene essentiality are direct gene deletions or random mutagenesis [@Zhang2009 ].

Direct deletions
Mori et. al. (2015) identified 328 essential gene candidates for the bacterium *Escherichia coli* using direct gene deletions [-@Mori2015].
Their method involves experimentally "knocking out" gene segments and studying the effect of the gene's abscence to the survivability of *E. coli*.
Kobayashi et. al. (2003) and de Berardinis et. al. (2008) also used single gene deletions to determine essential genes for *Bacillus subtilis* and *Acinetobacter baylyi* respectively [-@Kobayashi2003; -@DeBerardinis2008].

Transposon mutagenesis
Transposon mutagenesis, just as discussed previously, is an approach using transposons which insert in extant genes in random positions in the genome. At publication of Zhang's (2009) paper, 7 prokaryote genomes' essential genes were studied.
The number of essential genes for each specific prokaryote ranges between 300-650 [@Zhang2009].
A similar database called the CEG (Clusters of Essential Genes) database is also available.
It was built using data from the DEG but their difference is that this database annotates genes according to an improved protein family groups,  COG's (discussed in the following section) [@Qi2004].

### Use of machine learning and statistical methods
The current trend of research in this study is starting to shift from experimental methods to qualitative analyses due to the emergence of statistical and machine learning tools.
Van Tonder et. al. (2014) used this approach to determine bacterial core genomes to specific populations [@VanTonder2014 ].
The researchers developed Bayesian decision models to estimate the number of core genes for each population.
The researchers built the Bayesian prior of the model using the probabilities of gene occurrences as posterior.
Said Bayesian prior rule is then used to determine if a gene is present in the core genes.

### Clusters of Orthologous Genes (COGs)
Koonin started his work on the minimum set of genes in 1996 with Musheigan in a time when completely sequenced genomes were scarce.
In fact it was only 1995 when the first bacteral genome (*H. influenzae*) was completely sequnced.
During this time he was able to suggest the first iterations of the minimum gene set concept by comparing two relatively distant bacteria (*M. genitalium* and *H. influenzae*) [@Mushegian1996 ].
A year later Koonin, along with Tatusova and Lipman (1997) proposed a new perspective in protein classification [-@Tatusov1997].
This was the first conceptions of Cluster's of Orthologous Genes (COG).
The study created families of gene encoded proteins according to their orthology (having same functions).  
At the time of the study's publishing, 720 COG's were identified, each with individual orthologous proteins or orthologous set of proteins.
The COG classification was used as a framework to predict gene functions of poorly sequenced genome.
Using this new COG tool in hand, in the year 2000, Koonin revisited the minimal gene set concept [@Koonin2000 ].
The COG approach along with more sequenced genomes, allowed Koonin to compare more genes.
Koonin found a smaller set of conserved gene functions (about 30% of the 1996 minimum gene set size) across 25 sequenced genomes which oppose his previous finding in 1996.

## Gaps in knowledge
### Comparative methods fail on highly diverse group of organisms
The most common methods of comparative genomics usually involve studying the intersection of gene sets. Examples of this approach are Koonin and Musheigian's (1996) comparison between *M. genitalium* and *H. influenzae* and Tettelin et. al's (2005) *Streptococcus agalactiae* pangenome [-@Mushegian1996; -@Tettelin2005 ].
This approach worked very well on these papers because these studies involve comparing two closely related genes or comparing a group of genes belonging in a population of organisms.
A problem arises when the collection of genes compared is in a diverse group. The intersection of gene sets on a collection of diverse group will yield a very small set [@VanTonder2014].
The reason for this limitation is because the conservativeness of this comparative approach fails to take into account the complex relationships of genes and metabolic functions like synthetic lethality (e.g. genes A and B are only lethal if both are present in the same genome) [@Pal2006; @Mori2015] and conditionally essential genes (e.g. gene A is essential given C) [@Gerdes2006].

### Bacteria's resilience to transposon mutagenesis' disruption and single gene deletions
Hutchison (1999) discussed some of the limitations of transposon mutagenesis in his paper.
Hutchison's paper reported surprising results of 12 essential genes out of 1354 (less than 1%).
According to his discussion this may be because his experiment failed to disrupt some of the genes providing incorrect results.
Hutchison also suggests that erroneous results may be due to some cells keeping a functional duplicate copy of the otherwise disrupted gene.

### Previous methodologies don't make use of current state of the art gene annotations
As disccussed in the previous sections, knowledge about the minimum set of genes evolve as new bioinformatics and genomic tools evolve.
As an example, Koonin's body of work in the concept of minimum set of gene's has undergone multiple revisions as new tools emerge [@Mushegian1996; @Koonin2000 ].
Koonin's 2000 meta study on the concept of the minimum gene set make use of the early version of the COG database tool [@Tatusov1997].
At the time of the paper's publishing, Koonin worked with 25 completely sequenced genomes and the COG the database contained 2112 unique COGs.
On the other hand, at the time of this paper writing the most recent version (2014 update) of the COG database contains 5665 unique COG's [@Galperin2015].
The emergence of more completely sequenced genomes and better annotation tools prompt a revisit of the minimum gene set concept.
This time around we have in our hands robust machine learning techniques to study this abundant gene data.

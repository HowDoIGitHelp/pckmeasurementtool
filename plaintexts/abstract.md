# Abstract {.unnumbered}
The minimum set of genes of an organism refers to the smallest set of genes that can support a free living organism.
In this study the minimum set of genes was described using three machine learning models are used (Naive Bayes Classifier, Random Forest Classifier, and Artificial Neural Network), each trained with data annotated using the COG (Clusters of Orthologous Groups) framework.
The models show promising predictive power (Naive Bayes Classifier=0.80, Random Forest Classifier=0.78, and Artificial Neural Network=0.87).
Each model is then subjected to feature extraction to describe a its own interpretation of the minimum set of genes.
Each of the models' set of genes are compared the CEG databases set of essential genes.
The results show that even though the Naive Bayes Classifier does not have the most predictive power, it is able to perform best in the set comparisons between the CEG database. In particular it was the best model in classifying which genes are non-essential (Jaccard index of 0.0058 when compared to CEG set of nonessential genes).
These findings show that machine learning algorithms can provide good modelling tools for the minimum set of genes. The methods discussed in this paper can be applied to improve our understanding of the concepts behind gene essentiality and the requirements of creating life.

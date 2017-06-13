# Discussions
Each of the models were able to model the relationships with relatively high performance (Naive Bayes f1_score=0.80; Random Forest Classifier f1_score=0.78; Artificial Neural Network f1_score=0.87) but the main focus of the study was each of the model's representation of the minimum set of genes. In the representation aspect, each of the model's show its own respective advantages and disadvantages. The Random Forest Classifier was able to show complex conditional relationships of genes with each other but this models feature's cannot be represented as a set of genes. It was the Naive Bayes Classifier which was able to represent its features as coefficient of likelihoods that correspond to each gene's likelihood of being an element of the minimum set of genes.

##Comparing findings to an existing database
By obtaining the important features on each model, this study was able to propose its own findings on the concept of minimum gene set. Using the CEG database as a point of comparison, the following results were obtained:

|                               | CEG essential genes | non essential genes |
|-------------------------------|--------------------:|--------------------:|
| bayesian findings t=0.9       |          0.00149775 |                   0 |
| bayesian findings t=0.8       |           0.0549176 |                   0 |
| bayesian findings t=0.7       |            0.191447 |          0.00245776 |
| bayesian findings t=0.6       |            0.269896 |           0.0058548 |
| nn findings t=0.9             |           0.0684466 |           0.0189306 |
| nn findings t=0.8             |            0.130047 |           0.0403559 |
| nn findings t=0.7             |            0.189569 |           0.0614355 |
| nn findings t=0.6             |             0.23507 |            0.104526 |
Table: Jaccard index values of each model and their corresponding feature importance threshold (t)

Note that only the non-tree based models are in this table since the random forest model's representation of the minimum set of genes cannot be perfectly represented by feature importances. Random Forest classifier represents feature importances as if-else conditional relationships instead of individual weighted coefficients for each gene. Table 6.1 shows the Jaccard index of each model's obtained gene set and the CEG databases gene set. Jaccard index $\mathrm{J(A,B)}$ is a measure used to compare similarity over two sets. Jaccard index is defined by:

\begin{equation} \mathrm{J(A,B)}=\frac{|\mathrm{A} \cap \mathrm{B}|}{|\mathrm{A} \cup \mathrm{B}|}  \end{equation}

Table 5.2 shows that the gene sets obtained by this study are smaller than the gene set in the CEG database. There could be two reasons behind this disparity in gene sets.

(1) CEG database contain functionally redundant genes. The gene set obtained from the CEG database doesn't necessarily represent the minimum gene set itself, this gene set is merely the set of genes that have been defined as essential. There may be redundant functions in the CEG database itself which means that constructing a valid bacterium doesn't require exactly one of each gene defined in the database.

(2) The model is unable to represent the minimum set of genes. Although the models yield high scores in classifying between valid and invalid bacteria, this doesn't mean that models are able to perfectly represent the minimum set of genes. This could be the consequence if the data used in training isn't enough to represent the whole population of valid and invalid bacteria. There may be samples of bacteria that are not represented in any of the samples in the data. If this is truly the case the model would be unaware of relationships of genes and validity of these underrepresented bacteria.  Although all of the models genes sets are similar in the sense that all are smaller than the CEG database, the two models differ in their ability to determine nonessential genes. The Bayesian classifier's Jaccard index when compared to the non-essential gene set is smaller than the neural network classifiers Jaccard Index. This means that the neural network classifier has more genes misidentified as essential. This is a surprising result given that the neural network slightly outperforms the Bayesian classifier. The neural network's classifier's poor performance in identifying non-essential genes could be attributed to its own model representation of the minimum set of genes. It was discussed earlier how neural network classifiers are black box models. Even though these type of models perform well in classification, they are not widely used in feature analyses of data because of their complex  and black boxed structure.

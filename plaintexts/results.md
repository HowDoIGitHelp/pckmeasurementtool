# Results
## Binarization of data
One of the observations this study makes is how the models perform better when data is binarized. Instead of using each frequency value for each gene (Cluster of Orthologous Genes), the model yielded higher cross validation values when data was transformed through a binarization function:
\begin{equation}
b(x) = \left\{\begin{matrix}
1 &{x>0} \\
0 & {x\leq 0}
\end{matrix}\right.
\end{equation}
This approach may work better because same COG's serve similar functions (as discussed in a previous section in Chapter 2: Clusters of Orthologous Genes). Using frequency distribution as data values may obscure the relationships from the models due to the extra complexity. It may also introduce more noise for the data making it highly prone to overfitting.

## Minimum Set of Genes
### Coefficient of likelihood for each gene
Using the Naive Bayes Classifier each a coefficient of likelihood for each gene was obtained. The higher the coefficient of likelihood, the higher the probability that this gene is part of the minimum set of genes. The following graph in Figure 5.1 shows the frequency distribution of gene likelihoods:

![Frequncy Distribution of coef Values vs F1 Score](images/frequncy distribution of coef values.PNG)
\begin{center} Figure 5.1:Frequncy Distribution of coef Values vs F1 Score \end{center}

Figure 5.1 shows that the frequency of genes decreases as the coefficient of likelihood increases. In fact there are only 3 genes with coefficient of likelihood greater than or equal to 0.9. As we decrease our coefficient of likelihood threshold, we can include more genes, as seen in Table 5.1.

|                         | Number of genes in the set |
|-------------------------|---------------------------:|
| bayesian findings t=0.9 |                          3 |
| bayesian findings t=0.8 |                        110 |
| bayesian findings t=0.7 |                        393 |
| bayesian findings t=0.6 |                        566 |
Table: Threshold of coefficient of likelihood and the corresponding number of genes included in the set

### Decision trees of important genes
Using the Random forest classifier, 5 decision trees were obtained. These trees model the relationship of genes to bacterial validity.

![One of the 5 trees in the forest](images/tree3.PNG)
\begin{center} Figure 5.2: One of the 5 trees in the forest \end{center}

Genes which are closer to the root nodes are genes which are more likely part of the minimum set of genes since these genes are the primary splitters between valid and invalid bacteria. This means that the presence or absence of these genes describe the difference between each valid and invalid bacteria. Genes located farther from the root node are genes that may exhibit conditional essentiality from its parent genes.

### Matrix of network weights
Using the artificial neural network 2 matrices of interconnection weights were obtained. Since the architecture of the neural network is 4346-75-1 (4356 features/input neurons, 75 hidden layer neurons, 1 output class) the two matrices are o sizes $W_1:4346 \times 75$ and $W_2:75 \times 1$. We can infer which neurons in the hidden layers classify for valid bacteria by looking at matrix $W_2$. Highly positive values in $W_2$ indicate neurons that are strong determinants of bacterial validity. Each of these hidden layer neurons have a corresponding column in matrix $W_1$.

Therefore the gene weights (weights of interconnections between input and hidden layer) of highly positive hidden neurons with higher values will correspond genes which are more likely part of the minimum set of genes.

# Results and Discussions
## Binarization of data
One of the things this study observed is how the models perform better when data is binarized.
Instead of using each frequency value for each gene (Cluster of Orthologous Genes), the model yielded higher cross validation values when data was transformed through a binarization function:
\begin{equation}
b(x) = \left\{\begin{matrix}
1 &{x>0} \\
0 & {x\leq 0}
\end{matrix}\right.
\end{equation}
This approach may work better because same COG's serve similar functions (as discussed previously).
Using frequency distribution as data values may obscure the relationships from the models due to the extra complexity.
It may also introduce more noise for the data making it highly prone to overfitting.

## Algorithm Parameter Tuning

### Random Forest Classifier

#### Forest Size
The number of trees in a forest can affect the model's behaviour.
Having too little trees in the forest will make the model prone to overfitting while having too many trees will make the subsets of data assigned for each tree too small to represent the whole data.
Therefore the amount of trees in the forest should be chosen carefully.
This study did this by fitting the data into models with different forest sizes, from size=1 to size=20.
When the  forest is of size 1 (one decision tree) the sole tree is assigned with 195 samples.
While a forest with size 20 assigns about 10 samples for each tree.

![Forest Size vs F1 Score](images/forestsize.png)

The model performs the best at about forest sizes greater than 5.
Beyond this value, the graph shows that there is no meaningful increase in the model's performance as the forest size increases.

#### Minimum Impurity Split
The model's minimum impurity parameter was also tuned.
Minimum impurity refers to the value in which the algorithm decides to split the tree into subtrees.
A conservative approach in building each tree in the forest is making a tree split only when both subtrees are purely valid bacteria and purely invalid bacteria.
This approach is prone to overfitting since it doesn't forgive impurities from outlier samples.
By setting the minimum impurity to a higher value, the algorithm becomes more lenient in its tree splits, forgiving noise and outliers.
Although, if minimum impurity is set too high, the algorithm may be too lenient that it may forgive even incorrect tree splits that do not actually represent relationships in the data.
Finding the best amount of impurity is similar to finding the best forest size.
The model is fit with varying minimum impurities from impurity=0 to impurity=1.

![Minimum Impurity Threshold vs F1 Score](images/impurity.png)

The best performing minimum values of impurity are found between 0 to 0.1.
The model's performance experiences higher variance beyond this value.
As soon as impurity exceeds 0.3, the performance drops to zero because splits become too forgiving that the tree becomes meaningless.

### Artificial Neural Network

#### Number of Nodes in 1 Hidden Layer
The number of nodes in the hidden layer of a neural network also affects the model's performance.
Just like hidden layer sizes, having too few neurons may affect the ability of the network to model the relationships of the data while having too much neurons may slow down training and promote overfitting.
There are also architectural rules of thumb for choosing the number of neurons per layer.
According to Hagan et. al, (2014) one should begin with more than enough neurons from the start (somwhere between $N_i$ and $N_o$.
In this study different neuron sizes were tested, between n=10 until n=300

![Number of Neurons vs F1 Score](images/neuronssize.png)

The performance of the model is fluctuates between 0.75 to 0.85 between n=10 and n=60.
At about n>60 the performance of the model stabilizes to a narrower range, between 0.75 and 0.85.
Increasing the number of neurons where $60<n<300$ does not contribute a meaningful increase in model performance.

#### Number of Hidden Layers
The neural network model as also tested using different sizes.
Although an approximation of the relationships in the data can be represented by neural network with one hidden layer, additional layers improve this approximation.
Most neural networks work with 1 or 2 hidden layers.
Although increasing the neural network size will help the apporximation, having too much additional hidden layers is not advisable.
It will slow down the fitting and prediction of the data and it may also contribute to overfitting [@Hagan1996].
Although in this situation, where feature size greatly outnumber the sample size, it is advisable to have a small hidden layer size as possible.
This is because, most neural network architectural guidelines state the rule of thumb
$$N_h = \frac{N_s}{a(N_i+N_o)}$$
where $N_h$ is the upper bound of hidden layers that will not result in overfitting; $N_s=261$ is the sample size; $N_i=4345$ is the feature size; $N_o=2$ is the the number of classes; and $a$ is a scaling factor
This leaves $N_h$ with a value less than one for any $a>1$.
Despite knowing this, the model was still fit into different sizes of hidden layers from n=1 to n=20 just for the purposes of testing.

![Hidden Layer Size vs F1 Score](images/layersize.png)

The results show that neural networks with hidden layer sizes fluctuate between 0.8 and 0.85.
 The size of the hidden layer doesn't meaningfully affect this model's performance.
After testing all this, it was decided that the number of layers be set as small as possible (n=1) to follow the architectural rule of thumb.

## Cross Validation
### F1 score as Performance Measure
The amount of positive (valid bacteria; n=195) and negative (invalid bacteria;n=66) samples are unequal in this dataset.
This means that using the measure of accuracy:
\begin{equation} \mathrm{accuracy}=\frac{tP + tN}{N}  \end{equation}
where $tP$ is the number of true positives (predicted positive and actually positive); $tN$ is the number of true negatives (predicted negative and actually positive); and $N$ is the total size of the test partition.
will not be a good measure of model performance.
This is because having more positive data will reward higher accuracy to models that have high frequencies of positive predictions.
Using accuracy as a measure of performance will favor models that "cheat" by simply predicting positive for any sample.
To avoid models cheating, the measure f-1 score is used instead of accuracy.
$F_1$ score is defined as:
\begin{equation} F_1 =2 \frac{\mathrm{precision}\cdot \mathrm{recall}}{\mathrm{precision} + \mathrm{recall}}  \end{equation}
where precision is defined as  
\begin{equation} \mathrm{precision} =\frac{tN}{tP+fP}  \end{equation}
and recall is defined as
\begin{equation} \mathrm{recall} =\frac{tN}{tP+fN}  \end{equation}
$fN$ stands for false negatives (predicted negative but actually positive) and $fP$ stands for false positives (predicted positive but actually negative)
$F_1$ score is a more robust performance measure since it takes into account both precision and recall.
Despite having unequal amounts of positive and negative data, $F_1$ score can accurately measure model performance.

### Measuring overfitting
It was discussed in the previous sections how unreliable it is to measure a models performance using the same data it was trained on.
Having high performance on the training partition does not necessarily mean that the model has successfully described the relationships of data.
High performance on the training partition could also mean that the model is highly overfit to the training data.
This is why in this section, training performance and testing performance for each model is compared.
The following graphs show the effect of changing the proportion of the two partitions to each model's performance.
Each model performance is tested from training proportion of 0.1 (train_samples=26) to training proportion 0.75 (train_samples=196).
Whatever is left in the whole dataset is used as the test proportion.
Naive Bayes

![Naive Bayes Train Size Proportion vs F1 Score](images/bayesCV.png)

Random Forest Classifier

![Random Forest Classifier Train Size Proportion vs F1 Score](images/treeCV.png)

Artificial Neural Network

![Neural Network Train Size Proportion vs F1 Score](images/nnCV.png)

All of the models show typical model behaviors.
While the training partition increases in size, training score decreases.
This is because more samples mean that noise and outliers are outscaled by the number of samples, therefore, overfitting becomes less likely, decreasing the performance on its own training data.
On the other hand, while the training partition increases in size, test score increases.
This is because the increase of training samples means that the model is able to generalize the relationships easier.
Good generalization is manifested by a higher score in its test partition since this partition does not share the noise and outlier samples of the training partition.

## Minimum Set of Genes
### Coefficient of likelihood for each gene
Using the Naive Bayes Classifier each a coefficient of likelihood for each gene was obtained.
The higher the coefficient of likelihood, the higher the probability that this gene is part of the minimum set of genes.
The following graph shows the frequency distribution of gene likelihoods:

![Frequncy Distribution of coef Values vs F1 Score](images/frequncy distribution of coef values.PNG)

This shoes that the frequency of genes decreases as the coefficient of likelihood increases.
In fact there are only 3 genes with coefficient of likelihood greater than or equal to 0.9.
As we decrease our coefficient of likelihood threshold, we can include more genes.

|                         | Number of genes in the set |
|-------------------------|---------------------------:|
| bayesian findings t=0.9 |                          3 |
| bayesian findings t=0.8 |                        110 |
| bayesian findings t=0.7 |                        393 |
| bayesian findings t=0.6 |                        566 |

Table: Threshold of coefficient of likelihood and the corresponding number of genes included in the set

### Decision trees of important genes
Using the Random forest classifier, 5 decision trees were obtained.
These trees model the relationship of genes to bacterial validity.

![One of the 5 trees in the forest](images/tree1.PNG)

Genes which are closer to the root nodes are genes which are more likely part of the minimum set of genes since these genes are the primary splitters between valid and invalid bacteria.
This means that the presence or absence of these genes describe the difference between each valid and invalid bacteria.
Genes located farther from the root node are genes that may exhibit conditional essentiality from its parent genes.

### Matrix of network weights
Using the artificial neural network 2 matrices of interconnection weights were obtained.
Since the architecture of the neural network is 4346-75-1 (4356 features/input neurons, 75 hidden layer neurons, 1 output class) the two matrices are of sizes $W_1:4346 \times 75$ and $W_2:75 \times 1$.
There are multiple methods to calculate feature importance on neural networks.
Although most of these methods (e.g. recursive feature extraction, partial derivative) cannot be applied to this study because they lack the ability to calculate the direction of influence (feature is importance in classifying a specific output class) [@DeOna2014].
These feature extraction methods calculate a feature's contribution to the network's performance.
The value derived from these methods are not based on the model's structure.
This is the reason why in this study, Garson's feature extraction method is used [@Garson1991].
Garson's method derive it's feature importance value by interpreting the neural networks weight.
Using Garson's method we can infer which neurons in the hidden layers contribute the most in classifying valid bacteria by looking at matrix $W_2$.
Highly positive values in $W_2$ indicate that neurons that are strong determinants of bacterial validity.
Each of these hidden layer neurons have a corresponding column in matrix $W_1$.
Therefore the gene weights (weights of interconnections between input and hidden layer) of highly positive hidden neurons with higher values will correspond genes which are more likely part of the minimum set of genes.

### Comparing findings to existing databases
By obtaining the important features on each model, this study was able to propose its own findings on the concept of minimum gene set.
Using the CEG database as a point of comparison, the following results were obtained:
Note that only the non-tree based models are in this table since the random forest model's representation of the minimum set of genes cannot be perfectly represented by feature importances.
Random Forest classifier represents feature importances as if-else conditional relationships instead of individual weighted coefficients for each gene.


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


This table is the Jaccard index of each model's obtained gene set and the CEG databases gene set.
Jaccard index $\mathrm{J(A,B)}$ is a measure used to compare similarity over two sets.
Jaccard index is defined by:
\begin{equation} \mathrm{J(A,B)}=\frac{|\mathrm{A} \cap \mathrm{B}|}{|\mathrm{A} \cup \mathrm{B}|}  \end{equation}
This table shows that the gene sets obtained by this study are smaller than the gene set in the CEG database.
There could be two reasons behind this disparity in gene sets.

(1) CEG database contain functionally redundant genes.
 The gene set obtained from the CEG database doesn't necessarily represent the minimum gene set itself, this gene set is merely the set of genes that have been defined as essential.
There may be redundant functions in the CEG database itself which means that constructing a valid bacterium doesn't require exactly one of each gene defined in the database.

(2) The model is unable to represent the minimum set of genes.
Although the models yield high scores in classifying between valid and invalid bacteria, this doesn't mean that models are able to perfectly represent the minimum set of genes.
This could be the consequence if the data used in training isn't enough to represent the whole population of valid and invalid bacteria.
There may be samples of bacteria that are not represented in any of the samples in the data.
If this is truly the case the, model would be unaware of relationships of genes and validity on these underrepresented bacteria.

Although all of the models genes sets are similar in the sense that all are smaller than the CEG database, the two models differ in their ability to determine nonessential genes.
The Bayesian classifier's Jaccard index when compared to the non-essential gene set is smaller than the neural network classifiers Jaccard Index.
This means that the neural network classifier has more genes misidentified as essential.
This is a surprising result given that the neural network slightly outperforms the Bayesian classifier.
The neural network's classifier's poor performance in identifying non-essential genes could be attributed to its own model representation of the minimum set of genes.
It was discussed earlier how neural network classifiers are black box models.
Even though these type of models perform well in classification, they are not widely used in feature analyses of data because of their complex  and black boxed structure.

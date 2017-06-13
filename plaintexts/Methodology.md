# Methodology
## Data Collection
### Genes as features
To find the minimum set of bacteria genes to sustain a valid bacteria, a machine learning classification model was to be created built on features based on the genomic data. By building a model that can recognize valid and free living bacteria, this study can also propose on what features characterize a valid bacteria. These features used to build the model should represent genes of said bacteria. By studying on how the machine learning algorithms built the model we can infer which genes are the best determinants for characterizing a valid and free living bacteria and by consequence which genes are required to create a bacteria. But instead of focusing on the predictive and classification abilities of the model, the focus of this study was to analyse which features (genes) are strongest determinants. Of course the classification model built must also be a competent classifier, but this is only to ensure that the model built is correct and unbiased.

### Positive and Negative data
The data used in this study are genes with functions annotated according to COG's (cluster of orthologous genes). The data is divided into 2 groups, positive group (valid free living bacteria) and negative group (unculturable and non free living bacteria). Both sets are comprised of multiple samples of fully sequenced bacterium preprocessed by the Philippine Genome Center. Each column in the data (feature) represents a COG profile. For each instance of bacteria, the values for each cell represents the frequency of the COG's found in said bacterium’s genome. The model requires a negative set of data so that the models have a way to differentiate valid bacteria to non valid bacteria. Without the opposite groups the model built would be unable to make unbiased generalizations of the the characteristics of the bacterial core genome.

## Training and Testing
The process for model creation for the three models are identical. The data is split into two partitions, training and testing. The training partition is used to fit the model to the data and the testing partition is used to calculate the model's validation score. It is important that data is not shared by the two partitions. This rule is kept so that the model's tests can detect if the classifier is able to generalize on the data or it merely overfits on the data.

Overfitting occurs when the model describes the data's noise instead of the underlying relationship of genes and genome validity of bacteria. A model's overfitting is manifested by having exceptional scores on its training while having poor scores on its testing. This will happen if the model is too biased on the training partition and its noise and specificities instead of generalizing the relationships [@Smith2014]. The precautions to avoid overfitting is different for each model and these precautions will be discussed in their own sections later. The ratio of splitting into partitions should also be an informed choice. Leaving too little data instances for the training partition will negatively affect the model's accuracy. While leaving too little data instances for the testing partition will create unreliable tests. The two partitions of data must be large enough to be equivalent representations of each other [@Steinberg2014].

## Model Choices
### Naive Bayes
Naive Bayes is suitable for classifiers with features that represent frequency or set elements. This applies to the data set used in this study where frequency is the frequency of a particular COG in a bacterium's genome. Each data instance can also be represented as a set of COG's that fully comprises the bacterium's genome [@Zhang2004].

#### Model Fitting
The Naive Bayes family of classifiers are created based on Bayesian theorem. This algorithm is naive in the sense that it makes a naive assumption that all of the features in the model are mutually independent of each other. Applying Bayes theorem in bacterium data gives this relationship:
\begin{equation} P(y|x_{1},...,x_{n}) = \frac{P(y)P(x_{1},...,x_{n}|y)}{P(x_{1},...,x_{n})}  \end{equation}
Where $P(y|x_{1},...,x_{n})$ is the posterior probability of a bacterium being valid or invalid ($y$) given that the probabilities of gene occurences ($x_i$) are $x_{1},...,x_{n}|y$ [@Zhang2004].

$P(y)$ refers to the prior probability, or the general probability of the occurences of valid and invalid bacteria. There are no papers that describe the actual probability distribution of valid and invalid bacterium in the wild therefore the value used for the prior probability is the probability distribution of the data provided. $P(x_{1},...,x_{n}|y)$ refers to the likelihood probability or the likelihood of gene occurences to be $x_{1},...,x_{n}$ for each type of data ($y$, valid or invalid bacteria). The values $x_{1},...,x_{n}$ are frequency distributions of each gene (n=4347) in a given bacterium over the total number of gene occurrences in the whole dataset.

Naive Bayes family of classifiers are relatively immune to overfitting. This is because the rules that the algorithm builds are simple probability rules that erase noise and outliers. As long as the data is an accurate representation of the actual relationships, these models will not overfit [@Zhang2004].

#### Model representation of minimum set of genes
The model’s representation of the minimum set of genes will be derived from a set of each feature's coefficient of likelihood. This set will be a set of probabilities, where each probability represents a corresponding gene. Each feature's coefficient represents the likelihood that its corresponding gene is describes a valid bacterium. If that value is close to one, then it is likely that this gene is part of the minimum set.

### Random Forest Classifier
This model is also suitable for classifiers that can be represented as frequency values or set elements. The advantage of this model over Naive Bayes is that it is able to build more complex conditional relationships between features. This is suitable for this study since bacteria metabolism is governed by complex relationships (as previously discussed) [@Dietterich2000].

#### Model Fitting
Random forest classifier  is an ensemble classifier of decision trees. This means that this classifier is a model that classifies according to a frequency distribution of opinions from a set of independently trained decision trees. Each decision tree is trained in its own independent subset of the data. Decision trees are models which are also built from frequency distributions of data. Instead of making posterior probability rules like the Naive Bayes family of algorithms, decision tree algorithms build a tree of if-then-else decision rules [@Dietterich2000].

![image of dtree](images/treeexample.png)
\begin{center} Figure 4.1:Decision Tree Example \end{center}

Each node of a tree is a feature in the dataset and each leaf is an output class. Therefore, the model in this case is a tree where each node is a gene and each leaf represent either a valid bacterium or an invalid bacterium. Given a set of genes S that represent a bacteria, the classifier follows the decision tree, checking on each tree node if the gene is present in S and follows the described tree path until it ends up on the leaves as either valid or invalid. The model does this for each tree in the Forest and yields a frequency distribution of opinions. The predicted class will be whichever output class that has a higher frequency of opinions.

Decision trees are prone to overfitting that is why this study uses a random forest classifier.Instead of using only one decision tree to describe relationships in the data, a forest of decision trees is used, each tree with independent models of relationships built from disjoint partitions of the data. This isolates noise and outliers to a specific tree in the forest. Erroneous opinions will be hidden in the set of opinions, preventing it from affecting the model's predictions [@DiazUriarte2006].

#### Model Representation of the minimum set of genes
Random Forest Classifier creates a tree for each decision tree specified. Each of these trees describes the relationships within the data. Decision tree algorithms only create nodes for features that are good determinants of data. Because of this behaviour, trees created from the genome data will only contain genes which are good determinants of bacteria validity. The trees created from the data will also describe complex conditional relationships of genes like, synthetic lethality and conditional essentiality.

### Artificial Neural Network
Artificial Neural Networks are a powerful classification tool and are suitable for data with highly complex relationships. Models created using a multi-layer perceptron can generalize into high order mappings that represent high order relationships which may be the case for this data. Although the problem with multi-layer perceptron is that it produces a "black box" model which is difficult to analyse.

#### Model Fitting
An artificial neural network is defined by (1) the interconnection of neurons according to their layers, (2) the weights of the interconnections (3) an activation function that converts a neuron’s input into a meaningful output [@Hagan1996].

![neural network image](images/nnexample.png)
\begin{center} Figure 4.2:Neural Network Example \end{center}

The leftmost layer of a network is a set of input neurons representing the set of features. In this case it is a set of genes and their frequency distributions. The value passed into each neuron is a the weighted sum $g(w_1x_1+w_2x_2+...+w_nx_n)$ where $w_i$ is the interconnection weight, x is the node value and $g$ is an activation function. The activation function in this case is the sigmoid function

\begin{equation} g(x) = \frac{1}{1+e^{-x}} \end{equation}

Neural networks model's intuition is based on the universal approximation theorem. According to this theorem, any continuous function can be approximated by a single hidden layer containing a finite amount of neurons given mild assumptions under an activation function [@Hagan1996]. This just means that if the relationship of gene sets to bacterial validity can be represented as a continuous function, then there exists a neural network model that represents this relationship.

Neural Networks can easily overfit to the training data. But there are regularization precautions that are embedded into the training of neural networks that can avoid overfitting. Before training the model an alpha parameter can be set, along with other parameters like, number of layers and number of neurons per layer. This alpha parameter represents the regularization term, also known as a penalty term. It penalizes extremely large weights ($w$) therefore promoting smaller weight values. Thus, the resulting function representation of a highly regularized neural network has softer curves. Softer curves means that the model is more forgiving to the effects of data noise thus mitigating overfitting [@Hagan1996].

#### Model representation of minimum set of genes
The model representation of a neural network model is less intuitive than the Bayesian model and the Random Forest model. Instead of a set of probabilities or trees, the  neural network model yields a matrix of weights with size $m \times n$ where m is the number of neurons per layer and n is the number of layers. Since this study's interest is finding the minimum set of genes, this study will examine which weight values are consistently high for each node. Weights with higher values means that its corresponding feature (gene) contribute more in the classification decision of valid vs invalid bacteria.

## Algorithm Parameter Tuning
### Random Forest Classifier
#### Forest Size
The number of trees in a forest can affect the model's behaviour. Having too little trees in the forest will make the model prone to overfitting while having too many trees will make the subsets of data assigned for each tree too small to represent the whole data. Therefore the amount of trees in the forest should be chosen carefully. This study did this by fitting the data into models with different forest sizes, from size=1 to size=20. When the forest is of size 1 (one decision tree) the sole tree is assigned with 195 samples. While a forest with size 20 assigns about 10 samples for each tree.

![Forest Size vs F1 Score](images/forestsize.png)
\begin{center} Figure 4.3:Forest Size vs F1 Score \end{center}

According to the graph in Figure 4.3, the model performs the best at about forest sizes greater than 5. Beyond this value, the graph shows that there is no meaningful increase in the model's performance as the forest size increases.

#### Minimum Impurity Split
The model's minimum impurity parameter was also tuned. Minimum impurity refers to the value in which the algorithm decides to split the tree into subtrees. A conservative approach in building each tree in the forest is making a tree split only when both subtrees are purely valid bacteria and purely invalid bacteria. This approach is prone to overfitting since it doesn't forgive impurities from outlier samples. By setting the minimum impurity to a higher value, the algorithm becomes more lenient in its tree splits, forgiving noise and outliers. Although, if minimum impurity is set too high, the algorithm may be too lenient that it may forgive even incorrect tree splits that do not actually represent relationships in the data. Finding the best amount of impurity is similar to finding the best forest size. The model is fit with varying minimum impurities from impurity=0 to impurity=1.

![Minimum Impurity Threshold vs F1 Score](images/impurity.png)
\begin{center} Figure 4.4:Minimum Impurity Threshold vs F1 Score \end{center}

The best performing minimum values of impurity are found between 0 to 0.1.
According to the graph in Figure 4.4, the best performing minimum values of impurity were found between 0 to 0.1. The model's performance experiences higher variance beyond this value. As soon as impurity exceeds 0.3, the performance drops to zero because splits become too forgiving that the tree becomes meaningless.

### Artificial Neural Network

#### Number of Nodes in 1 Hidden Layer
The number of nodes in the hidden layer of a neural network also affects the model's performance. Just like hidden layer sizes, having too few neurons may affect the ability of the network to model the relationships of the data while having too much neurons may slow down training and promote overfitting [@Hagan1996]. There are also architectural rules of thumb for choosing the number of neurons per layer. According to Hagan et. al, (2014) one should begin with more than enough neurons from the start (somwhere between $N_i$ and $N_o$. In this study different neuron sizes were tested, between n=10 until n=300.


![Number of Neurons vs F1 Score](images/neuronssize.png)
\begin{center} Figure 4.5:Number of Neurons vs F1 Score \end{center}

According to the graph in figure 4.5, the performance of the model is fluctuates between 0.75 to 0.85 between n=10 and n=60. At about n>60 the performance of the model stabilizes to a narrower range, between 0.75 and 0.85. Increasing the number of neurons where 60<n<300 does not contribute a meaningful increase in model performance.

#### Number of Hidden Layers
The neural network model was also tested using different sizes. Although an approximation of the relationships in the data can be represented by neural network with one hidden layer, additional layers improve this approximation. It is common practice to employ neural networks with 1 or 2 hidden layers. However, while increasing the neural network size will help the approximation, having too much additional hidden layers is not advisable. It will slow down the training and prediction of the data and it may also contribute to overfitting [@Hagan2014]. Although in this situation, where feature size greatly outnumber the sample size, it is advisable to have a small hidden layer size as possible. This is because, most neural network architectural guidelines state the rule of thumb
\begin{equation} N_h = \frac{N_s}{a(N_i+N_o)}$ \end{equation}
where $N_h$ is the upper bound of hidden layers that will not result in overfitting; $\N_s=261$ is the sample size; $N_i=4345$ is the feature size; $N_o=2$ is the the number of classes; and $\alpha$ is a scaling factor

This leaves $N_h$ with a value less than one for any $\alpha > 1$. Despite knowing this, the model was still fit into different sizes of hidden layers from n=1 to n=20 just for the purposes of testing.

![Hidden Layer Size vs F1 Score](images/layersize.png)
\begin{center} Figure 4.6:Hidden Layer Size vs F1 Score \end{center}

According to the graph in Figure 4.6, neural networks’ performaces fluctuate between 0.8 and 0.85. The size of the hidden layer does not meaningfully affect this model's performance. After testing all this, it was decided that the number of layers be set as small as possible (n=1) to follow the architectural rule of thumb.

## Cross Validation
### F1 score as Performance Measure
The amount of positive (valid bacteria; n=195) and negative (invalid bacteria;n=66) samples are unequal in this dataset. This means that using the measure of accuracy:
\begin{equation} \mathrm{accuracy}=\frac{tP + tN}{N}  \end{equation}
where $tP$ is the number of true positives (predicted positive and actually positive); $tN$ is the number of true negatives (predicted negative and actually positive); and $N$ is the total size of the test partition.

Accuracy will not be a good measure of model performance. This is because having more positive data will reward higher accuracy to models that have high frequencies of positive predictions. Using accuracy as a measure of performance will favor models that "cheat" by simply predicting positive for any sample. To avoid models cheating, the measure f-1 score is used instead of accuracy. $F_1$ score is defined as:
\begin{equation} F_1 =2 \frac{\mathrm{precision}\cdot \mathrm{recall}}{\mathrm{precision} + \mathrm{recall}}  \end{equation}
where precision is defined as  
\begin{equation} \mathrm{precision} =\frac{tN}{tP+fP}  \end{equation}
and recall is defined as
\begin{equation} \mathrm{recall} =\frac{tN}{tP+fN}  \end{equation}
$fN$ stands for false negatives (predicted negative but actually positive) and $fP$ stands for false positives (predicted positive but actually negative)
$F_1$ score is a more robust performance measure since it takes into account both precision and recall. Despite having unequal amounts of positive and negative data, $F_1$ score can accurately measure model performance.

### Measuring overfitting
It was discussed in the previous sections how unreliable it is to measure a model’s performance using the same data it was trained on. Having high performance on the training partition does not necessarily mean that the model has successfully described the relationships of data. High performance on the training partition could also mean that the model is highly overfit to the training data. This is why in this section, training performance and testing performance for each model is compared. The following graphs show the effect of changing the proportion of the two partitions to each model's performance. Each model performance is tested from training proportion of 0.1 (train_samples=26) to training proportion 0.75 (train_samples=196). Whatever is left in the whole dataset is used as the test proportion.

![Naive Bayes Train Size Proportion vs F1 Score](images/bayesCV.png)
\begin{center} Figure 4.7:Naive Bayes Train Size Proportion vs F1 Score \end{center}

![Random Forest Classifier Train Size Proportion vs F1 Score](images/treeCV.png)
\begin{center} Figure 4.8:Random Forest Classifier Train Size Proportion vs F1 Score \end{center}

![Neural Network Train Size Proportion vs F1 Score](images/nnCV.png)
\begin{center} Figure 4.9:Neural Network Train Size Proportion vs F1 Score \end{center}

All of the models show typical model behaviors. While the training partition increases in size, training score decreases. This is because more samples mean that noise and outliers are outscaled by the number of samples, therefore, overfitting becomes less likely, decreasing the performance on its own training data. On the other hand, while the training partition increases in size, test score increases. This is because the increase of training samples means that the model is able to generalize the relationships easier. Good generalization is manifested by a higher score in its test partition since this partition does not share the noise and outlier samples of the training partition.

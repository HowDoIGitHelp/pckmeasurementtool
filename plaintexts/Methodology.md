# Methodology
## Data Collection
### Genes as features
To find the minimum set of bacteria genes to sustain a valid bacteria, a machine learning classification model was to be created built on features based on the genomic data.
By building a model that can recognize valid and free living bacteria, this study can also propose on what features characterize a valid bacteria.
These features used to build the model should represent genes of said bacteria.
By studying on how the machine learning algorithms built the model we can infer which genes are the best determinants for characterizing a valid and free living bacteria and by consequence which genes are required to create a bacteria.
But instead of focusing on the predictive and classification abilities of the model, the focus of this study was to analyse which features (genes) are strongest determinants.
Of course the classification model built must also be a competent classifier, but this is only to ensure that the model built is correct and unbiased.

### Positive and Negative data
The data used in this study are genes with functions annotated according to COG's (cluster of orthologous genes).
The data is divided into 2 groups, positive group (valid free living bacteria) and negative group (unculturable and non free living bacteria).
Both sets are comprised of multiple samples of fully sequenced bacterium preprocessed by the Philippine Genome Center.
Each column in the data (feature) represents a COG profile.
For each instance of bacteria, the values for each cell represents the frequency of the COG's found in said bacteriums genome.
The model requires a negative set of data so that the models have a way to differentiate valid bacteria to non valid bacteria.
Without the opposite groups the model built would be unable to make unbiased generalizations of the the characteristics of the bacterial core genome.

## Training and Testing
The process for model creation for the three models are the same.
The data is split into two partitions, training and testing.
The training partition is used to fit the model to the data and the testing partition is used to calculate the model's validation score.
It is important that data is not shared by the two partitions.
This rule is kept so that the model's tests can detect if the classifier is able to generalize on the data or it merely overfits on the data.

Overfitting occurs when the model describes the data's noise instead of the underlying relationship of genes and genome validity of bacteria.
A model's overfitting is manifested by having exceptional scores on its training while having poor scores on its testing.
This will happen if the model is too biased on the training partition and its noise and specificities instead of generalizing the relationships.
The precautions to avoid overfitting is different for each model and these precautions will be discussed in their own sections later.
The ratio if splitting into partitions should also be an informed choice.
Leaving too little data instances for the training partition will negatively affect the model's accuracy.
While leaving too little data instances for the testing partition will create unreliable tests.
The two partitions of data must be large enough to be equivalent representations of each other.

## Model Choices
### Naive Bayes
This model is suitable for classifiers with features that represent frequency or set elements.
This applies to the data set used in this study where frequency is the frequency of a particular COG in a bacterium's genome.
Each data instance can also be represented as a set of COG's that fully comprises the bacterium's genome.

#### Model Fitting
The Naive Bayes family of classifiers are created based on Bayesian theorem.
This algorithm is naive in the sense that it makes a naive assumption that all of the features in the model are mutually independent of each other [@Zhang2004].
Applying Bayes theorem in bacterium data gives this relationship:
\begin{equation} P(y|x_{1},...,x_{n}) = \frac{P(y)P(x_{1},...,x_{n}|y)}{P(x_{1},...,x_{n})}  \end{equation}
Where $P(y|x_{1},...,x_{n})$ is the posterior probability of a bacterium being valid or invalid ($y$) given that the probabilities of gene occurences ($ x_{i}$) are $x_{1},...,x_{n}|y$.
$ P(y)$ refers to the prior probability, or the general probability of the occurences of valid and invalid bacteria.
There are no papers that describe the actual probability distribution of valid and invalid bacterium in the wild therefore the value used for the prior probability is the probability distribution of the data provided.
$P(x_{1},...,x_{n}|y)$ refers to the likelihood probability or the likelihood of gene occurences to be $x_{1},...,x_{n}$ for each type of data ($y$, valid or invalid bacteria)
The values $x_{1},...,x_{n}$ are frequency distributions of each gene (n=4347) in a given bacterium over the total number of gene occurrences in the whole dataset.
Naive Bayes family of classifiers are relatively immune to overfitting.
This is because the rules that the algorithm builds are simple probability rules that erase noise and outliers.
As long as the data is an accurate representation of the actual relationships, these models will not overfit.

#### Model representation of minimum set of genes
The models representation of the minimum set of genes will be derived from a set of each feature's coefficient of likelihood.
This set will be a set of probabilities, where each probability represents a corresponding gene.
Each feature's coefficient represents the likelihood that its corresponding gene is describes a valid bacterium.
If that value is close to one, then it is likely that this gene is part of the minimum set.

### Random Forest Classifier
This model is also suitable for classifiers that can be represented as frequency values or set elements.
The advantage of this model over Naive Bayes is that it is able to build more complex conditional relationships between features.
This is suitable for this study since bacteria metabolism is governed by complex relationships (as previously discussed).

#### Model Fitting
Random forest classifier  is an ensemble classifier of decision trees.
This means that this classifier is a model that classifies according to a frequency distribution of opinions from a set of independently trained decision trees.
Each decision tree is trained in its own independent subset of the data.
Decision trees are models which are also built from frequency distributions of data.
Instead of making posterior probability rules like the Naive Bayes family of algorithms, decision tree algorithms build a tree of if-then-else decision rules [@Dietterich2000].
[image of dtree]
Each node of a tree is a feature in the dataset and each leaf is an output class.
Therefore, the model in this case is a tree where each node is a gene and each leaf represent either a valid bacterium or an invalid bacterium.
Given a set of genes S that represent a bacteria, the classifier follows the decision tree, checking on each tree node if the gene is present in S and follows the described tree path until it ends up on the leaves as either valid or invalid.
The model does this for each tree in the Forest and yields a frequency distribution of opinions.
The predicted class will be whichever output class that has a higher frequency of opinions.
Decision trees are prone to overfitting that is why this study uses a random forest classifier.
Instead of using only one decision tree to describe relationships in the data, a forest of decision trees is used, each tree with independent models of relationships built from disjoint partitions of the data.
This isolates noise and outliers to a specific tree in the forest.
Erroneous opinions will be hidden in the set of opinions, preventing it from affecting the model's predictions [@DiazUriarte2006].

#### Model Representation of the minimum set of genes
Random Forest Classifier creates a tree for each decision tree specified.
Each of these trees describes the relationships within the data.
Decision tree algorithms only create nodes for features that are good determinants of data.
Because of this behaviour, trees created from the genome data will only contain genes which are good determinants of bacteria validity.
The trees created from the data will also describe complex conditional relationships of genes like, synthetic lethality and conditional essentiality.

### Artificial Neural Network
This is a neural network model that is a powerful classification tool and is suitable for data with highly complex relationships.
Models created using a a multi-layer perceptron can generalize into high order mappings that represent high order relationships which may be the case for this data.
Although the problem with multi-layer perceptron is that it produces a "black box" model which is difficult to analyse.

#### Model Fitting
An artificial neural network is defined by (1) the interconnection of neurons according to their layers, (2) the weights of the interconnections (3) an activation function that converts a neurons input into a meaningful output.
[neural network image]
The leftmost layer of a network is a set of input neurons representing the set of features.
In this case it is a set of genes and their frequency distributions.
The value passed into each neuron is a the weighted sum $g(w_1x_1+w_2x_2+...+w_nx_n)$ where $w_i$ is the interconnection weight, x is the node value and $g$ is an activation function.
The activation function in this case is the sigmoid function \begin{equation} g(x) = \frac{1}{1+e^{-x}} \end{equation}

Neural networks model's intuition is based on the universal approximation theorem.
According to this theorem, any continuous function can be approximated by a single hidden layer containing a finite amount of neurons given mild assumptions under an activation function [@Hagan1996].
This just means that if the relationship of gene sets to bacterial validity can be represented as a continuous function, then there exists a neural network model that represents this relationship.

Neural Networks can easily overfit to the training data.
But there are regularization precautions that are embedded into the training of neural networks that can avoid overfitting.
Before training the model an alpha parameter can be set, along with other parameters like, number of layers and number of neurons per layer.
This alpha parameter represents the regularization term, also known as a penalty term.
It penalizes extremely large weights ($w$) therefore promoting smaller weight values.
Thus, the resulting function representation of a highly regularized neural network has softer curves.
Softer curves means that the model is more forgiving to the effects of data noise thus mitigating overfitting.

#### Model representation of minimum set of genes
The model representation of a neural network model is less intuitive than the Bayesian model and the Random Forest model.
Instead of a set of probabilities or trees, the  neural network model yields a matrix of weights with size  $m \times n$ \end{equation} where m is the number of neurons per layer and n is the number of layers.
Since this study's interest is finding the minimum set of genes, this study will examine which weight values are consistently high for each node.
Weights with higher values means that its corresponding feature (gene) contribute more in the classification decision of valid vs invalid bacteria.

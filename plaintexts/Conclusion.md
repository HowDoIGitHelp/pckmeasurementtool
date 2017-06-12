# Conclusion
The advent of big data and machine learning has contributed to the growth of many fields.
In the case of this study, machine learning was used in the field of genomics and bioinformatics, particularly on the concept of the minimum set of genes.
In this study multiple machine learning algorithms (Naive Bayes, Random Forest, Artifical Neural Network) were used to model the relationship between bacterial validity and genes.
Training using data from COG annotated gene sequences, the models were able to classify the validity of a given bacterium based only on its genes.
Each of the models were able to model the relationships with relatively high performance (Naive Bayes f1_score=0.80; Random Forest Classifier f1_score=0.78; Artificial Neural Network f1_score=0.87) but the main focus of the study was each of the model's representation of the minimum set of genes.
In the representation aspect, each of the model's show show its own respective advantages and disadvantages.
The Random Forest Classifier was able to show complex conditional relationships of genes with each other but this models feature's cannot be represented as a set of genes.
It was the Naive Bayes Classifier which was able to represent its features as coefficient of likelihoods that correspond to each gene's likelihood of being an element of the minimum set of genes.
The Neural Network Classifier, despite showing the best results in terms of performance score, showed poor results in its representation on the minimum set of genes, when compared to the CEG database.
The Naive Bayes Classifier was able to show that the minimum set of genes may be a small subset of the total set of essential genes.
This study also considers the possibility that the minimum set of genes cannot be modeled using the data used in this study.
But this possibility is unlikely since the naive bayes classifier was able to show good performance in identifying non-essential genes.

As a recommendation, future studies could focus on selecting more robust methods in extracting feature importance.
This especially applies to the extraction of feature importance in a neural network model.
At the time of writing this paper, there is still no widespread consensus as to which feature extraction method is best in neural network models.
In the future when there is one, the study of minimum set of genes will surely benefit from it.
It is also advisable for future studies to include other families of classifiers like SVM, KNN or maybe unsupervised algorithms like K means clustering.

In conclusion, the study shows that there is good promise in the application of machine learning in the study of the minimum set of genes.
The study on the minimum set of genes has been an open problem ever since the dawn of the field genomics.
This study is the first of kind in the sense that this was the first attempt in applying machine learning algorithms to model the minimum set of genes.
Research on the field of bio-informatics and machine learning are still emerging, in the future when data is more abundant and tools are more advanced, this study would be a good framework for more large-scale and in depth studies.

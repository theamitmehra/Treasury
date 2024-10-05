# Basic Practice
### Feature Engineering
The process of transforming row data into dataset is called **feature engineering**.  It is a labor-intensive process that demands from the data analyst a lot of creativity and preferably domain knowledge.
#### One-Hot Encoding
The process of transforming categorical feature into several binary ones is called One-Hot Encoding.
If you example has a categorical feature "color" and this feature has three possible values; "red", "yellow", and "green", you can transform this feature into a vector of three values
$$
\begin{align}
\text{red} = [1, 0, 0] \\ 
\text{yellow} = [0, 1, 0] \\
\text{green} = [0, 0, 1]  \\
\end{align}
$$
#### Binning
An opposite situation, occurring less frequently in practice, is when you convert numerical feature into categorical one . This process is called **Binning** (or **Bucketing**).
For example, instead of representing age as a single real-valued feature, the analyst could chop ranges of age into discrete bins: all ages between 0 and 5 years-old could be put into one bin, 6 to 10 years-old could be in the second bin, 11 to 15 years-old could be in the third bin, and so on.
#### Normalization
Normalization is the process of converting an actual range of values which a numerical feature can take, into a standard range of values, typically in the interval $[-1, 1]$ or $[0, 1]$. For example, suppose the natural range of a particular feature is 350 to 1450. By subtracting 350 from every value of the feature, and dividing the result by 1100, one can normalize those values into the range $[0, 1]$. More generally, the normalization formula looks like this: 
$$
\bar{x}_{(j)} = \frac{x_{(j)} - min_{(j)}} {max_{(j)} - min_{(j)}}
$$

where $min^{(j)}$ and $max^{(j)}$ are, respectively, the minimum and the maximum value of the feature j in the dataset.
#### Standardization
Standardization (or z-score normalization) is the procedure during which the feature values are rescaled so that they have the properties of a standard normal distribution with µ = 0 and ‡ = 1, where µ is the mean (the average value of the feature, averaged over all examples in the dataset) and ‡ is the standard deviation from the mean. Standard scores (or z-scores) of features are calculated as follows: 
$$
\bar{x}^{(j)} = \frac {x^{(j)} - \mu^{(j)}} {\sigma (j) }.
$$
#### Dealing with Missing Features
We often face data that comes with some or many missing values. And missing values are not useful to model, so we need to deal with them
Here are some approaches of dealing with missing values for a feature include.
- Removal of example with missing feature
- Using a learning algorithm that can deal with missing feature values
- Using data imputation techniques.
#### Data imputation Techniques
1. One technique is to replace missing value with the average value of feature in the dataset.
2. Another technique is to replace the missing value by the same value outside the normal range of values. For example, if the normal range is $[0, 1]$, then you can set the missing value equal to $2$ or $-1$.
3. A more advanced technique is to use the missing value as the target variable for a regression problem. You can use all remaining features $[x_{i}^{(1)}, x_{i}^{2}, \dots, x_{i}^{(j-1)}, x_{i}^{(j+1)}, \dots, x_{i}^{D}]$ to form a feature vector $\hat{x}_{i}$, set $y_{i} = x^{(j)}$, where $j$ is the feature with a missing value. Now we can build a regression model to predict $\hat{y}$ from the feature vectors $\text{\^{x}}$
### Learning Algorithm Selection
Choosing a algorithm can be a difficult task. Here are some steps to follow.
- Explainability
- In-memory vs out-of-memory
- Number of Feature and examples
- Categorical vs numerical features
- Nonlinearity of the data
- Training speed
- Prediction Speed
### Three Sets
Data analyst work with three sets of labeled examples
1. Training set
2. Testing set
3. Validation set
### Underfitting vs overfitting

### Regularization
**Regularization** is an umbrella-term that encompasses methods that force the learning algorithm to build a less complex model. In practice, that often leads to slightly higher bias but significantly reduces the variance. This problem is known in the literature as the bias-variance tradeoff.

Linear regression objective we want to minimize :
$$
min _{w, b} \frac{1}{N} \sum_{i=1}^N (f_{w, b} ((\text{x}_{i}) - y_{i}))^2
$$

An L1- regularized objective looks like this
$$
min_{w, b} C|\text{w}| + \frac{1}{n} \sum_{1} ^ N (f_{w, b} (\text{x}_{i} - y_{i}))^2
$$
where $|\text{w}|\stackrel{def}{=} \sum_{j=1}^D |w^{(j)}|$ and $C$ is a hyperparameter that controls the importance of regularization. if we set $C$ to zero, the model becomes a standard non-regularized linear.

An L2 - regularized objective will look like this :
$$
min_{w, b} C||\text{w}||^2 + \frac{1}{n} \sum_{1} ^ N (f_{w, b} (\text{x}_{i} - y_{i}))^2
$$
Where $||\text{w}||^2 \stackrel{def}{=} \sum_{j=1}^D( w^{(j)})^2$
### Model Performance Assessment
#### Confusion Matrix
The **confusion matrix** is a table that summarizes how successful the classification model is at predicting examples belonging to various classes. One axis of the confusion matrix is the label that the model predicted, and the other axis is the actual label.
#### Precision/Recall
**Precision** is the ratio of correct positive predictions to the overall number of positive predictions: 
$$
Precision = \frac{TP} {TP + FP} 
$$

**Recall** is the ratio of correct positive predictions to the overall number of positive examples in the test set: 
$$
Recall = \frac {TP} {TP + F}
$$
The precision is the proportion of relevant documents in the list of all returned documents. The recall is the ratio of the relevant documents returned by the search engine to the total number of the relevant documents that could have been returned.
#### Accuracy
**Accuracy** is given by the number of correctly classified examples divided by the total number of classified examples. In terms of the confusion matrix, it is given by: 
$$
Accuracy = \frac {TP + TN} {TP + TN + FP + FN}
$$

Accuracy is a useful metric when errors in predicting all classes are equally important
#### Cost-Sensitive Accuracy
For dealing with the situation in which different classes have different importance, a useful metric is **cost-sensitive accuracy**.
To compute a cost-sensitive accuracy, you first assign a cost (a positive number) to both types of mistakes: FP and FN. You then compute the counts TP, TN, FP, FN as usual and multiply the counts for FP and FN by the corresponding cost before calculating the accuracy
#### Area under the ROC curve (AUC)
The ROC curve (ROC stands for “receiver operating characteristic,” the term comes from radar engineering) is a commonly used method to assess the performance of classification models. ROC curves use a combination the true positive rate (the proportion of positive examples predicted correctly, defined exactly as recall) and false positive rate (the proportion of negative examples predicted incorrectly) to build up a summary picture of the classification performance. 
The true positive rate and the false positive rate are respectively defined as
$$
\begin{matrix}
TPR = \frac{{TP}}{(TP + FN)} & \text{and} & FPR = \frac{FP}{FP+TN}
\end{matrix}
$$
ROC curves can only be used to assess classifiers that return some confidence score (or a probability) of prediction.
### Hyperparameter Tuning
hyperparameters aren’t optimized by the learning algorithm itself. The data analyst has to “tune” hyperparameters by experimentally finding the best combination of values, one per hyperparameter.
#### Cross Validation
When you don’t have a decent validation set to tune your hyperparameters on, the common technique that can help you is called cross-validation. When you have few training examples, it could be prohibitive to have both validation and test set. You would prefer to use more data to train the model. In such a case, you only split your data into a training and a test set. Then you use cross-validation to on the training set to simulate a validation set

___
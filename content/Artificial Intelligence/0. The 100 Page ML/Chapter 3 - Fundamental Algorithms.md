# Fundamental Algorithms

### Linear Regression
Linear regression is a popular regression learning algorithm that learns a model which is a linear combination of features of the input example.
#### Problem Statement
We have a collection of labeled examples ${(xi, yi)}N i=1$, where $N$ is the size of the collection, $x_i$ is the D-dimensional feature vector of example $i = 1,...,N,$ $y_i$ is a real-valued target and every feature $x(j) i , j = 1,...,D$, is also a real number. We want to build a model $f_{w,b(x)}$ as a linear combination of features of example x: 
$$
fw,b(x) = wx + b, \qquad \qquad(1)  
$$
where w is a D-dimensional vector of parameters and b is a real number. The notation $f_{w,b}$ means that the model $f$ is parametrized by two values: $w$ and $b$
We will use the model to predict the unknown y for a given x like this: $y \leftarrow f_{w,b} (X)$. Two models parametrized by two different pair $(w,b)$ will likely to produce two different predictions which applied to the same example. We want to find the optimal value $(w*, b*)$.
#### Solution
The optimization procedure which we use to find the optimal values for $w*$ and $b*$ tries to minimize the following expression:
$$
\frac {1} {N} \sum_{i=1 ... N} (f_{w,b} (x_i) - y_i)^2. \qquad \qquad (2)
$$
In mathematics, the expression we minimize  or maximize is called an **objective function** or simply and **objective**. The expression $(f(x_i) - y_i)^2$ in the above objective is called **the loss function**. It's a measure of penalty for misclassification of example $i$. This particular choice of the loss function is called **squared error loss**. All model-Based learning algorithms have a loss function and what we do to find a best model is we try to minimize the objective known as the cost function.
In linear regression, the cost function is given by the average loss, also called the empirical risk. The average loss, or empirical risk, for a model, is the average of all penalties obtained by applying the model to the training data.
**Overfitting** is the property of a model such that model predicts very well labels of the examples used during training but frequently make errors when applied to examples that weren't seen by the learning algorithm during training.
Linear models rarely overfit.
In 1705, the French mathematician `Adrien-Marie Legendre`, who first published the sum of squares method for gauging the quality of the model stated that squaring the error before summing is convenient. Why did he say that? The absolute value is not convenient, because it doesn’t have a continuous derivative, which makes the function not smooth. Functions that are not smooth create unnecessary difficulties when employing linear algebra to find closed form solutions to optimization problems. Closed form solutions to finding an optimum of a function are simple algebraic expression and often preferable to using numerical optimization methods such as **Gradient Descent**.
___
### Logistic Regression
The first thing to say is that logistic regression is not a regression, but a classification learning algorithm. The name comes from statistics and is due to the fact that the mathematical formulation of logistic regression is similar to that of linear regression.
#### Problem statement
In logistic regression, we still want to model $y_i$ as a linear function of $\text x_i$ however, with a binary $y_i$ is not straightforward. The linear combination of features such as $\text wx_i + b$ is a function that spans from minus infinity to plus infinity, while $y_i$ has only two possible values.
If we define negative label as 0 and positive label as 1, then we would just need to find a simple continuous function whose codomain is (0,1). If the value returned by model is close to 0, then assign a negative label to x; otherwise positive.
One function that is simple continuous is **Standard logistic function** (also known as **sigmoid function**) :
$$
f(x) = \frac {1} {1+ e^{-x}}
$$
where $e$ is the base of the natural logarithm (also called Euler's numbers).
![[Pasted image 20240814114419.png]]

#### Solution
In logistic regression instead of using squared loss and trying to minimize the empirical risk, we maximise the $likelihood$ of out training set according to model.
The optimization criterion in logistic regression is called **maximum likelihood**.
$$
L_{w,b} \space {\buildrel def \over =} \space  \prod_{i=1, ..., N} f_{w,b} {\text x_i}^{y_{i}} \space (1- f_{w,b} (\text x_i)) ^{(1-y_i)}
$$

$log-likelihood$ 
$$
LogL_{w,b} {\buildrel def \over =} \space ln(L(w,b(x)) = \sum _{i=1}^N y_i \space ln f_{w,b}(\text x) + (1 - y_i) ln (1 - f_w{w,b} (x)).
$$
___
### Decision Tree Learning
A decision tree is an acyclic graph that can be used to make decisions. In each branching node of the graph, a specific feature j of the feature vector is examined. If the value of the feature is below a specific threshold, then the left branch is followed; otherwise, the right branch is followed. As the leaf node is reached, the decision is made about the class to which the example belongs.
#### Problem Statement
make a simple decision tree classifier.
#### Solution
There are various formulation of the decision tree learning algorithm. One of them is **ID3**.
The optimization criterion, in this case, is the average log-likelihood:
$$
\frac 1 N \sum_{i=1} ^N {\text {ln}} \space f_{ID3} (\text{x}_i) + (1-y_i) {\text ln} (1- f_{ID3} (\text{x}_i)). 
$$


### Support Vector Machine

### K-Nearest Neighbors
K-Nearest Neighbors (KNN) is a non-parametric learning algorithm. Contrary to other learning algorithms that allow discarding the training data after the model is built, KNN keeps all training examples in memory. Once a new, previously unseen example x comes in, the KNN algorithm finds k training examples closest to x and returns the majority label (in case of classification) or the average label (in case of regression). The closeness of two points is given by a distance function. For example, Euclidean distance seen above is frequently used in practice. Another popular choice of the distance function is the negative cosine similarity. 
**Cosine similarity** defined as,
$$
s(\mathbf{x}_i, \mathbf{x}_k) \stackrel{\text{def}}{=} \cos(L(\mathbf{x}_i, \mathbf{x}_k)) = \frac{\sum_{j=1}^D x_i^{(j)} x_k^{(j)}}{\sqrt{\sum_{j=1}^D \left(x_i^{(j)}\right)^2} \sqrt{\sum_{j=1}^D \left(x_k^{(j)}\right)^2}}
$$
is a measure of similarity of the directions of two vectors. If the angle between two vectors is 0 degrees, then two vectors points to the same direction and cosine similarity is equal to 1. If the vectors are orthogonal, the cosine similarity is 0.  For vectors pointing in opposite direction, the cosine similarity is -1. If we want to use cosine similarity as distance metric we need to multiply it by -1.
Other popular distance metrics include `Chebychev distance`,` Mahanobis distance`,` Hamming Distance`. 
The choice of distance metric as well the value for k are the choices the analyst makes before running the algorithm. So these are hyperparameters.
___

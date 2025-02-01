# Notation and Definitions

### Notation
#### Scalars
A scalars is a simple numerical value like 19, or -3,45. Variable or constant that takes scalar values are denoted by an italic letter like $x$ or $a$.
#### Vectors
A vector is an ordered list of scalar values, called **attributes**. We denote a vector as a bold character, for example, $x$ or $w$. Vectors can be visualized as arrows that point to some directions as well as points in a multi-dimensional space.
#### Set
A set is an **unordered collection** of **unique elements**. We denote a set as a calligraphic capital character, for example, $S$.
A set of numbers can be finite (include a fixed amount of values). In this case, it is denoted using accolades, for example, $\{1, 3, 18, 23, 235\}$ or $\{x1, x2, x3, x4,...,xn\}$. A set can be infinite and include all values in some interval. If a set includes all values between a and b, including a and b, it is denoted using brackets as $[a, b]$. If the set doesn’t include the values a and b, such a set is denoted using parentheses like this: (a, b). For example, the set $[0, 1]$ includes such values as 0, 0.0001, 0.25, 0.784, 0.9995, and 1.0. A special set denoted R includes all numbers from minus infinity to plus infinity. 

When an element x belongs to a set $S$, we write $x \in S$. We can obtain a new set $S3$ as an intersection of two sets $S1$ and $S2$. In this case, we write $S3 \leftarrow S1 \cap S2$. For example $\{1, 3, 5, 8\}$ $\cap$ $\{1, 8, 4\}$ gives the new set {1, 8}.

We can obtain a new set $S_3$ as a union of two sets $S_1$ and $S_2$. In this case, we write $S_3 \leftarrow S_1 \cup S_2$. For example $\{1, 3, 5, 8\} \cup \{1, 8, 4\}$ gives the new set $\{1, 3, 4, 5, 8\}$.

#### Capital Sigma Notation
The summation over a collection $X = \{x_1, x_2, ... , x_{n-1}, x_n\}$ or over the attributes of a vector $x = [x^{(1)}, x^{(2)}, ..., x^{(m-1)}, x^{(m)}]$ is denoted like this:
$$
\sum_{i=1}^n x_i {\buildrel \rm def \over =}  x_1 + x_2 + ... + x_{n-1} + x_n,
\text {or else}:
$$
$$
\sum_{j=1}^m x^{(j)} {\buildrel \rm def \over =} x^(1) + x^(2) + ... + x^(m-1) + x^(m).
$$
The notation ${\buildrel \rm def \over =}$ means "is defined as".

#### Capital Pi Notation 
 notation analogous to capital sigma is the capital pi notation. It denotes a product of elements in a collection or attributes of a vector: 
$$
 \prod_{i=1} ^ n {x_i} {\buildrel \rm def \over =} x_1. x_2 ., ... . x_{n-1}. x_n
$$
 where $a · b$ means $a$ multiplied by $b$. Where possible, we omit $·$ to simplify the notation, so ab also means a multiplied by b.
#### Operation of Sets
A **derived set creation operator** looks like this: $S' \rightarrow \{x^2 | x \in S, x > 3\}$. This notation means that we create a new set $S'$ by putting into it x squared such that that x is in S, and x is greater than 3. 
The **cardinality operator** $|S|$ returns the number of elements in set $S$.
#### Operations of Vectors
Sum of two vectors $x + z$ is defined as the vector 
$$[x(1) + z(1), x(2) + z(2),...,x(m) + z(m) ]$$

Difference of two vectors $x-z$ is defined as 
$$r [x(1) ≠ z(1), x(2) ≠ z(2),...,x(m) ≠ z(m) ]$$

Scalar Multiplication  
$${wc\buildrel \rm def \over =} [cx(1), cx(2), . . . , cx(m) ]$$
Dot product of vectors is a scalar 
$${wx \buildrel def \over =} \sum_{i=1} ^{m} w(i) x(i)$$
#### Functions
A function is a relation that associates each element x of a set $X$ , the domain of the function, to a single element y of another set Y, the codomain of the function. A function usually has a name. If the function is called f, this relation is denoted $y = f(x)$ (read f of x), the element x is the argument or input of the function, and y is the value of the function or the output. The symbol that is used for representing the input is the variable of the function (we often say that f is a function of the variable x).

#### Max and Arg Max
Given a set of values $A = {a1, a2,...,an}$, the operator, 
$$
{\buildrel \rm max \over {a \in A} } f(a)
$$
returns the highest value f(a) for all elements in the set A. On the other hand, the operator,
$$
{\buildrel \rm {argmax} \over {a \in A} } f(a)
$$
returns the element of the set A that maximizes f(a). 
Sometimes, when the set is implicit or infinite, we can write $max_a f(a)$ or ${\buildrel \rm max \over {a} } f(a)$ 
Operators `min` and `arg min` operate in a similar manner.
#### Assignment Operator
The expression $a \leftarrow f(x$) means that the variable a gets the new value: the result of $f(x)$. We say that the variable a gets assigned a new value. Similarly, $a \leftarrow [a1, a2]$ means that the two-dimensional vector a gets the value $[a1, a2]$.
#### Derivative and Gradient 
A derivative $f'$ of a function $f$ is a function or a value that describes how fast $f$ grows (or decreases).
___
### Random Variable
A $\text {random variable}$ is a variable whose possible values are numerical outcomes of a random phenomenon.
Types : 
1. Discreate Random Variable
2. Continuous Random Variable
#### Unbiased Estimators
#### Bayes' Rule
The conditional probability $Pr(X = x|Y = y)$ is the probability of the random variable X to have a specific value x given that another random variable Y has a specific value of y. The **Bayes’ Rule** (also known as the Bayes’ Theorem) stipulates that:
$$
Pr(X = x | Y = y) = \frac {Pr(Y = y | X = x) Pr(X = x)} {Pr(Y = y)}
$$
#### Parameter Estimation
#### Classification vs. Regression 
**Classification** is a problem of automatically assigning a label to an unlabeled example. Spam detection is a famous example of classification.

In machine learning, the classification problem is solved by a classification learning algorithm that takes a collection of **labeled examples** as inputs and produces a model that can take an unlabeled example as input and either directly output a label.
In a classification problem, a label is a member of finite set of **classes**. 
- Binary classification : When the size of the set of classes is two. 
- Multiclass classification : When the size of the set of classes is three or more.

**Regression** is a problem of predicting a continuous real-valued label (target) given an unlabeled example. Estimating house price valuation based on house features is a famous example of regression.
The regression problem is solved by a regression learning algorithm that takes a collection of labeled examples as inputs and produces a model that can take an unlabeled example as input and output a target
#### Model-Based vs. Instance-Based Learning

Most supervised learning algorithms are model-based. **Model-Based learning algorithms** use the training data to create a model that has parameters learned from the training data. In SVM the two parameters were `w*` and `b*`. After model is built, the training data can be discarded.

**Instance-based learning** algorithms use the whole dataset as the model. One instance-based algorithm frequently used in practice is K-Nearest Neighbors (KNN). In classification, to predict a label for an input example the `KNN algorithm`looks at the close neighborhood of the input example in the space of feature vectors and outputs the label that it saw the most often in this close neighborhood

#### Shallow vs. Deep Learning
A **shallow learning algorithm** learns the parameters of the model directly from the features of the training examples. Most supervised learning algorithms are shallow. The notorious exceptions are **neural network** learning algorithms, specifically those that build neural networks with more than one **layer** between input and output. Such neural networks are called **deep neural networks**. In deep neural network learning (or, simply, deep learning), contrary to shallow learning, most model parameters are learned not directly from the features of the training examples, but from the outputs of the preceding layers.
___

# Introduction 
Machine Learning is a subfield of **computer science** that is concerned with building algorithms which to be useful, rely on a collection of examples of some phenomenon.

Machine Learning can also be defined as the process of solving a practical problem by 
1) gathering a dataset and 
2) algorithmically building a statistical model based on that dataset.
___
### Type of Learning
#### Supervised Learning : 
In supervised learning that dataset is the collection of labeled examples $\{(x_i, y_i)\}_{i=1} ^{N}$. Each element $x_i$ among N is called a feature vector. A **feature vector** is a vector in which each dimension j = 1,...,D contains a value that describes the example somehow. That value is called a feature and is denoted as $x(j)$ .

#### Unsupervised Learning : 
In Unsupervised Learning the dataset is a collection of unlabeled examples $\{x_i\}_{i=1}^N$ Again, x is a feature vector and the goal of a unsupervised learning algorithm is to create a model that takes feature vector x as input and either transforms it into another vector or into a value that can be used to solve a practical problem. For example, in **Clustering**, the model returns the id of the cluster for each feature vector in the dataset. 
In **Dimensionality Reduction**, the output of the model is a feature vector that has a fewer feature than the input x; in **Outlier Detection**, the output is a real number that indicates how x is different from a typical example in the dataset. 

#### Semi-Supervised Learning 
In Semi-Supervised learning the dataset contains both labeled and unlabeled examples. The goal of a semi-supervised learning algorithm is the same as the goal of supervised learning algorithm.
The hope here is that using many unlabeled examples can help the learning algorithm to find a better model.

#### Reinforcement Learning
Reinforcement learning is a subfield of machine learning where the machine “lives” in an environment and is capable of perceiving the state of that environment as a vector of features. The machine can execute actions in every state. Different actions bring different rewards and could also move the machine to another state of environment. The goal of RL is to Learn Policy. 
A policy is a function $f$ (similar to the model in supervised learning) that takes the feature vector of a state as input and outputs an optimal action to execute in that state. 
___
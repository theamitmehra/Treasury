# Neural Networks and Deep learning

### Neural networks
A neural network just like regression or an SVM model, is a mathematical function:
$$
y = f_{NN}(\text{x})
$$
The function $f_{NN}$ has a particular form: it’s a nested function.
$$
y = f_{N N} (\text{x}) = f_{3}(f_{2}(f_{1}(x)))
$$
where $f_{2}$ and $f_{3}$ are vector functions of the following form:
$$
f_{l}(\text{z}) \stackrel {\text{def}}{=} g_{l}( \text{W}_{l} z+ b_{l})
$$
where $l$ is called the layer index and can span from 1 to any number of layers. The function $g_{l}$ is called activation function. The parameters $\text{W}_{l}$ (a matrix) and $b_{l}$ (a vector) for each layer are learned using the familiar gradient descent by optimizing. The output of $f_{l}(z)$ is a vector $[g_{l}(a_{l, 1}), g_{1}(a_{l, 2}), \dots, g_{l}(a_{l, size_{1}})]$
where $g_l$ is some scalar function and $size_{l}$ is the number of units in layer $l$.
#### Multilayer Perceptron

![[A Multilayer Perceptron.png]]

$$
\begin{align}
& Fig : \text{ A multilayer perceptron with two-dimensional input, } \\
& \text{ two layers with four units and one output layer with one unit}
\end{align}
$$


#### Feed-forward Neural Network Architecture
Feed-forward neural network architecture is a widely popular architecture used in ANN that process data in a feed forward manner. 
Two very popular activation functions are logistic function, **tanh** and **ReLU** . 

$$
\begin{align}
\tanh(z) = \frac{e^z - e^{-z}} {e^z + e^{-z}},  \\
 \\
relu(z) = \begin{cases}
0 & \text{if } z <0  \\
z & \text{otherwise}
\end{cases}
\end{align}
$$

### Deep Learning
Deep learning refers to training neural networks with more than two non-output layers. The two biggest challenges were referred to as the problems of **exploding gradient** and **vanishing gradient** as gradient descent was used to train the network parameters.

To update the values of parameters in neural networks the algorithm called **backpropagation** is typically used. Backpropagation is an efficient algorithm for computing gradients on a neural networks using the chain rule. Chain rule is used to calculate partial derivatives of a function. 
During gradient descent, the neural network’s parameters receive an update proportional to the partial derivative of the cost function with respect to the current parameter in each iteration of training.
#### Convolutional Neural network
A convolutional neural network (CNN) is a special kind of FFNN that significantly reduces the number of parameters in a deep neural network with many units without losing too much in the quality of the model. CNNs have found applications in image and text processing where they beat many previously established benchmarks.
Because CNNs were invented with image processing in mind.

![[Filter convolving across an image..png]]

In CNNs, a small regression model looks like the one in the multilayer perception image. To detect some pattern, a small regression model has to learn the parameters of a matrix $F$ (for "filter") of size $p \times p$ where $p$ is the size of a patch. 
One layer of a CNN consists of multiple convolution filters just like one layer in vanilla FFNN consists of multiple units. Each filter of the first (leftmost) layer slides $-$ or convolves $-$ across the input image, left to right, top to bottom, and convolution is computed at each iteration.
The numbers in the filter matrix, for each filter $F$ in each layer, as well as the value of the bias term $b$, are found by the gradient descent with backpropagation, based on data by minimizing the cost function.
A nonlinearity is applied to the sum of convolution and the bias term. Typically ReLU activation function is used in all hidden layers.
Since we can have $size_l$ filters in each layer $l$, the output of the convolution layer $l$ would consist of $size_l$ matrices, one for each filter. 

If the CNN has one convolution layer following another convolution layer, then the subsequent layer $l + 1$ treats the output of the preceding layer $l$ as a collection of $size_l$ image matrices. Such a collection is called a volume. Each filter of layer $l + 1$ convolves the whole volume. The convolution of a patch of a volume is simply the sum of convolutions of the corresponding patches of individual matrices the volume consists of.

In computer vision, CNNs often get volumes as input, since an image is usually represented by three channels: R, G, and B, each channel being a monochrome picture
___
#### Recurrent neural network
Recurrent neural networks (RNNs) are used to label, classify, or generate sequences. A sequence is a matrix, each row of which is a feature vector and the order of rows matters. Labeling a sequence means predicting a class to each feature vector in a sequence. Classifying a sequence means predicting a class for the entire sequence. Generating a sequence means to output another sequence (of a possibly different length) somehow relevant to the input sequence.

The idea behind RNN is that each unit u of recurrent layer $l$ has a real-valued **state** $h_{i, u}$. The state can be seen as a memory of input. in RNN each unit $u$ in each recurrent layer $l$ receives two inputs : 
1. A vector of outputs from the previous layer $l-1$ 
2. A vector of state from this same layer $l$ from the previous time step.
![[RNN.png]]
In an RNN, the input example is "read" by the neural network one feature vector at a timestep. The index $t$ denotes a timestep. To update the state $h_{l,u}^{t}$ at each timestep $t$ in each unit u of each layer $l$ we first calculate a linear combination of the input feature vector with the state vector $h_{l, u}^{t-1}$ of this same layer from the previous timestep, $t-1$. The linear combination of two vectors is calculated using two parameter vectors $w_{l, u}, u_{l, u}$ and a parameter $b_{l, u}$. The value of $h_{l, u}^{t}$ is then obtained by applying an activation function g1 to the result of the linear combination. A typical choice for function $g_1$ is $tanh$. The output $y_l^t$ is typically a vector calculated for the whole layer $l$ at once. To obtain $y_{l}^{t}$, we use an activation function $g_2$ that takes a vector as input and returns a different vector values $v_{l, u}^{t}$ calculated using a parameter matrix $V_{l}$ and the parameter vector $c_{l,u}$. A typical choice for $g_{2}$ is the `softmax` function.
$$
\sigma (z) \stackrel {def} {=} [\sigma^{(1)}, \dots, \sigma^{(D)}], where \, \sigma^{(j)} \stackrel {def} {=} \frac{\exp(z^{(j)}) }{\sum_{k=1}^{D}\exp(z^{k})}
$$
The `softmax` function is a generalization of the sigmoid function to multidimensional data. It has the property that $\sum_{j=1}^{D} \sigma^{(j)}$ and $\sigma^{(j) > 0}$ for all $j$.

The values of $w_{l,u}, u_{l,u}, b_{l,u} , V_{l,u}$ , and $c_{l,u}$ are computed from the training data using gradient descent with backpropagation. To train RNN models, a special version of backpropagation is used called **backpropagation through time**.

Both $\tanh$ and $softmax$ suffer from the vanishing gradient problem. 

Another problem RNNs have is that of handling long-term dependencies. As the length of the input sequence grows, the feature vectors from the beginning of the sequence tend to be “forgotten,” because the state of each unit, which serves as network’s memory, becomes significantly affected by the feature vectors read more recently. Therefor in text or speech processing, the cause-effect link between distant words in a long sentence can be lost.

The most effective RNNs used in practice are gated RNNs. These include LSTM and GRUs.

Let’s look at the math of a GRU unit on an example of the first layer of the RNN (the one that takes the sequence of feature vectors as input). A minimal gated GRU unit u in layer l takes two inputs: the vector of the memory cell values from all units in the same layer from the previous timestep, ht≠1 l , and a feature vector xt . It then uses these two vectors like follows (all operations in the below sequence are executed in the unit one after another):

$$
\begin{align}
{\stackrel {\sim}{h}}_{l, u}^{t} & \leftarrow g_{1} (w_{l, u}x^{t} + u_{l, u}h_{l}^{t-1} + b_{l,u}), \\
\Gamma_{l,u}^{t} &\leftarrow g_{2}(m_{l,u}x^{t} + o_{l,u}h^{t-1} + a_{l, u}), \\
h_{l, u}^{t} & \leftarrow \Gamma_{l,u}^{t} {\stackrel {\sim}{h}}_{l}^{t} + (1- \Gamma _{l,u}^{t}) h_{l}^{t-1}  \\
h_{l}^{t} & \leftarrow [h_{l, 1}^{t}, \dots, h_{l, size_{l}}^{t}]  \\
y_{l}^t & \leftarrow g_{3}(V_{l}h_{l} ^{t} + c_{l, u}),
\end{align}
$$
where $g_{1}$ is the $\tanh$ activation function , $g_{2}$ is called the gate function is implemented as the sigmoid function. The sigmoid function takes values in the range of (0, 1). If the gate $\Gamma _{l,u}$ is close to 0, then the memory cells keeps its value from the memory cell is overwritten by a new value $\stackrel {\sim} {h}_{l,u}^{t}$ . Just like in standard RNNs, $g_{3}$ is usually softmax.

A gated unit takes an input and stores it for some time. This is equivalent to applying the identity function (f(x) = x) to the input. Because the derivative of the identity function is constant, when a network with gated units is trained with backpropagation through time, the gradient does not vanish.
___
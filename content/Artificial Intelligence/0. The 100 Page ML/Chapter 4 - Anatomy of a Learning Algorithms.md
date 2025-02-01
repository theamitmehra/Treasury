# Anatomy of a Learning Algorithm
### Building Blocks of a Learning Algorithm
Every learning algorithm consists of three parts
1. A loss function
2. An optimization criterion
3. An optimization routine 
### Gradient Descent
Gradient descent is an iterative optimization algorithm for finding the minimum of a function. To find a local minimum of a function using gradient descent, one starts at some random point and takes steps proportional to the negative of the gradient (or approximate gradient) of the function at the current point.
Gradient descent can be used to find optimal parameters for linear and logistic regression, SVM and also neural networks which we consider later. For many models, such as logistic regression or SVM, the optimization criterion is convex. Convex functions have only one minimum, which is global. Optimization criteria for neural networks are not convex, but in practice even finding a local minimum suffices.

##### Working of Gradient Descent 
Linear regression model looks like : $f(x) = wx + b$. where $w$ is called weights and $b$ is called bias. in order to get the optimal model we have to find the optimal values for both $w$ and $b$.
we look for such values $w$ and $b$ that minimize the mean square error:
$$
l = \frac{1}{N} \sum _{i=1}^{N}{{(y_{i} -( wx_{i} + b))^{2}}}.
$$
Gradient Descent starts with calculating the partial derivate for every parameter.

$$
 \begin{align}
\frac{\partial l}{\partial w} & = \frac{1}{N} \sum_{i=1}^{N} -2x_{i} (y_{i} - (w_{x_{i}} + b)); \\
\frac{\partial l}{\partial b} & = \frac{1}{N} \sum_{i=1}^{N} - 2(y_{i} - (wx_{i} + b))
\end{align}
$$
To find the partial derivate of the term $(y_{i} - (wx + b))^{2}$ with respect to $w$ we applied the $chain \ rule$. Here  we have the chain $f= f_{2}(f_{1})$ where $f_{1} = y_{i} - (wx + b)$ and $f_{1}^{2}$. To find a partial derivate of $f$ with respect to $w$ we have to first find the partial derivate of $f$ with respect to $f_{2}$ which is equal to $2(y_{i} - (wx + b))$ . and then we have to multiply it by the partial derivate of $y_{i} - (wx + b)$ with respect to $w$ which is equal to $-x$ . So overall 
$$
\frac{\partial l}{\partial w} = \frac{1}{N} \sum_{i=1}^{N} -2x_{i} (y_{i} - (wx_{i} + b))
$$
We initialize $w_{0} = 0$ and $b_{0} = 0$ and then iterate through out training examples. each examples having the form of $(x_{i}, y_{i}) = (Spendings_i \ , Sales_i)$. For each examples we update $w$ and $b$ using our partial derivates, The learning rate $\alpha$ controls the size of an update :
$$
\begin{align}
w_{i} &= \alpha \frac{-2x_{i} (y_{i} - (w_{i-1}+ b_{i-1}))}{N} \\
b_{i} & \leftarrow \alpha \frac{-2(y_{i} - (w_{i-1}x_{i} + b_{i-1}))}{N}
\end{align}
$$
Where $w_{i}$ and $b_{i}$ denote the values of $w$ and $b$ after using the example $(x_{i}, y_{i})$ for the update.
One pass through all training examples is called an epoch.
### How machine Learning engineers work
Machine learning engineers use libraries instead of implementing learning algorithm themselves. The most frequently used open-source library is *scikit-learn*:

```python
def train(x, y):
	from sklearn.linear_model import LinearRegression
	modl = LinearRegression().fit(x, y)
	return model

model = train(x, y)

x_new = 23.0
y_new = model.predict(x_new)
print(y_new)
```

___
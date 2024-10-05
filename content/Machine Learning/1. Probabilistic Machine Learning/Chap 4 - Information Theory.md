# Information Theory

### Entropy
The **entropy** of a probability distribution can be interpreted as a measure of uncertainty, or lack of predictability, associated with a random variable drawn from a given distribution.

>[!example]
>Suppose we observe a sequence of symbols $X_{n} \sim p$ generated from distribution $p$. If $p$ has high entropy, it will be hard to predict the value of each observation $Xn$.

##### Entropy for discrete random variables
$$
\mathbb{H}(X) \triangleq - \sum_{k=1}^{K} p(X=k) \log_{2}p(X = k) = - \mathbb{E}_{x}[\log p(X)]
$$
Here $\mathbb{H}(X)$ denotes the entropy of the rv with distribution $p$. 
The discrete distribution with maximum entropy is the uniform distribution. Hence for a K-ary random variable, the entropy is maximized if $p(x=k)=\frac{1}{K};$ 

##### Application : DNA sequence logos

#### Cross entropy
The cross entropy between distribution $p$ and $q$ is defined by
$$
\mathbb{H}_{ce}(p, q) \triangleq - \sum_{k-1}^K p_{k}\log q_{k}
$$
#### Joint entropy
The joint entropy of two random variables $X$ and $Y$ is defined as 
$$
\mathbb{H} (X, Y) = - \sum_{x,y} \space p(x,y) \space\log_{2} p(x,y) 
$$
#### Conditional entropy
The conditional entropy of $Y$ given $X$ is the uncertainty we have in $Y$ after seeing $X$, averaged over possible values for $X$:
$$
\mathbb{H} (Y|X) \triangleq \mathbb{E}_{p(X)} [\mathbb{H}(Y|X)]
$$
#### Perplexity
The perplexity of a discrete probability distribution $p$ is defined as
$$
\text{perplexity}(p) \triangleq 2^{\mathbb{H}(p)}
$$
This is often interpreted as a measure of predictability.

#### Differential entropy for continuous random variables
If $X$ is a continuous random variable with pdf $p(x)$ , we define the differential entropy as 
$$
h(X) \triangleq - \int_{\mathcal{X}} p(x) \log p(x) \, dx 
$$
assuming this integral exists, For example, suppose $X \sim X U(0,a)$ Then
$$
h(X) = -\int_{0}^{a} dx \frac{1}{a} \log \frac{1}{a} = \log a
$$
___
### Relative entropy (KL divergence) *
Given two distributions p and q, it is often useful to define a distance metric to measure how “close” or “similar” they are. In fact, we will be more general and consider a divergence measure D(p, q) which quantifies how far q is from p, without requiring that D be a metric.
It is also known as **information gain** or **relative entropy** between two distributions $p$ and $q$.
For discrete distributions , the KL divergence is defined as follows:
$$
D_{\mathbb{KL}} (p ||q) \triangleq \sum_{k=1}^{K} p_{k}\log \frac{p_{k}}{q_{k}}
$$
Interpretation :
$$
D_{\mathbb{KL}}(p \parallel q) = 
\quad \underbrace{- \sum_{k=1}^{K} p_k \log p_k}_{-\mathbb{H}(p)}
\quad + \underbrace{\sum_{k=1}^{K} p_k \log q_k}_{\mathbb{H}_{ce}(p,q)}
$$
We recognize the first term as the negative entropy and the second term as the cross entropy.
##### Example : KL divergence between two Gaussians
KL divergence between two multivariate Gaussian distribution is given by :
$$ 
\begin{align}
&D_{\mathbb{KL} } \left( \mathcal{N}\left( x|\mu_{1}, \Sigma{1} \right) || \mathcal{N}(x|\mu_{2}, \Sigma_{2} ) \right )  \\
&= \frac{1}{2} \left[ \text{tr}(\Sigma_{2}^{-1} + (\mu_{2}-\mu_{1})^T \Sigma_{2}^{-1}(\mu_{2}-\mu_{1}) - D + \log( \frac {\det( \Sigma_{2}) }{\det(\Sigma_{1})}) \right]
\end{align}
$$

In the scalar case, this becomes
$$
D_{\mathbb{KL}}(\mathcal{N}(x|\mu_{1}, \sigma_{1}) || \mathcal{N}(x|\mu_{2},\sigma_{2})) = \log \frac{\sigma_{2}}{\sigma_{1}} + \sigma_{1}^{2} + \frac{(\mu_{1} - \mu_{2})^{2}} {2\sigma_{2}^{2}} - \frac{1}{2}
$$
##### KL divergence and MLE

##### Forward vs reverse KL
Forwards KL (inclusive KL)
$$
D_{\mathbb{KL}} (p|q) = \int p(x)\log \frac{{p(x)}}{q(x)} \, dx 
$$
Minimizing this wrt $q$ is known as an **M-projection** or **moment project**.
Reverse KL (exclusive KL)
$$
D_{\mathbb{KL}}(p|q) = \int q(x)\log \frac{{q(x)}}{p(x)} \, dx 
$$
Minimizing this wrt $q$ is known as an **I-projection** or **information projection**.
___
### Mutual Information

The mutual information between rv's $X$ and $Y$ is defined as follows:
$$
\mathbb{I} (X; Y) \triangleq D_{\mathbb{KL}} (p(x,y) || p(x)p(y)) = \sum_{y\in Y} \sum_{x \in X} p(x,y) \log \frac{p(x,y)}{p(x)p(y)}
$$
##### Conditional Mutual information
We can define the **conditional mutual information** 

$$
\mathbb{I} (X; Y| Z) \triangleq \mathbb{E}_{p(Z)} [\mathbb{I}(X; Y) | Z]
$$
Chain rule for mutual information:
$$
\mathbb{I} (Z_{1}, \dots, Z_{N}; X) = \sum_{n=1}^{N} \mathbb{I} (Z_{n}; X|Z_{1}, \dots, Z_{n-1})
$$

##### MI as a generalized correlation coefficient
##### Normalized mutual information 
$$
N MI (X, Y) = \frac{\mathbb{I}(X;Y)}{min(\mathbb{H}(X), \mathbb{H}(Y))} \leq 1
$$

##### Maximal information coefficient
$$
MIC (X,Y) = \overset {\max}{G} \frac{\mathbb{I}(X,Y|_{G})}{\log ||G||}
$$
Where $G$ is the set of 2d grids, and $(X, Y )|G$ represents a discretization of the variables onto this grid, and $||G||$ is $min(Gx, Gy)$, where $Gx$ is the number of grid cells in the $x$ direction, and $Gy$ is the number of grid cells in the $y$ direction.
##### Data processing inequality
Suppose we have an unknown variable $X$, and we observe a noisy function of it, call it $Y$ . If we process the noisy observations in some way to create a new variable $Z$, it should be intuitively obvious that we cannot increase the amount of information we have about the unknown quantity, $X$. This is known as the **data processing inequality**.
##### Sufficient Statistics
An important consequence of the DPI is the following. Suppose we have the chain $θ → \mathcal{D} → s(\mathcal{D})$. Then 
$$
\mathbb{I} (θ; s(\mathcal{D})) ≤ \mathbb{I}(θ; \mathcal{D})
$$
If this holds with equality, then we say that $s(\mathcal{D})$ is a sufficient statistic of the data $\mathcal{D}$ for the purposes of inferring $\theta$.

###### Fano's Inequality
A common method for feature selection is to pick input features $X_d$ which have high mutual information with the response variable $Y$ . Below we justify why this is a reasonable thing to do. In particular, we state a result, known as Fano’s inequality, which bounds the probability of misclassification (for any method) in terms of the mutual information between the features X and the class label $Y$ .
$$
***
$$
___
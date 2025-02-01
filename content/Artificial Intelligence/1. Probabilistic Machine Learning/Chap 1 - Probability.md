# Univariate Models
### Introduction
#### Probability 

>[!quote] Pierre Laplace
> Probability Theory is nothing but common sense reduced to calculation.
> 

There are two different interpretation of probability. 
1. Frequentist Interpretation - In this view probabilities represent long run frequencies of **events** that can happen multiple times
2. Bayesian Interpretation - In this view probability is used to quantify out uncertainty about something, It is related to information rather than repeated trails.

#### Types of uncertainty

- **Epistemic uncertainty** - Uncertainty due to our ignorance of the underlying hidden causes or mechanism generating our data. A simpler term for this type of uncertainty is **model uncertainty**.
- **Aleatoric uncertainty** - It arises from intrinsic variability, which we cannot reduced even if we collect more data. A simpler term for this is **data uncertainty**
#### Probability as an extension of logic
###### Probability of an event 
We define an **event**, denoted by the binary variable $A$, as some state of the world that either holds or does not hold. For example, $A$ might be event “It will rain tomorrow”, or “it rained yesterday”, or “the label is $y = 1$”, or “the parameter $θ$ is between 1.5 and 2.0”, etc. The expression $Pr(A)$ denotes the probability with which you believe event $A$ is true (or the long run fraction of times that $A$ will occur). We require that $0 ≤ Pr(A) ≤ 1$, where $Pr(A) = 0$ means the event definitely will not happen, and $Pr(A) = 1$ means the event definitely will happen. 

We write $Pr(\bar{A})$ to denote the probability of event $A$ not happening; this is defined to be $Pr(\bar{A}) = 1 − Pr(A).$

###### Probability of a conjunction of two events
We define the **joint probability** of events $A$ and $B$ both happening as follows: 
$$
Pr(A \cap B) = Pr(A, B)
$$
If $A$ and $B$ are independent events, we have 
$$
Pr(A, B) - Pr(A)\,Pr(B)
$$
>[!example] 
>suppose $X$ and $Y$ are chosen uniformly at random from the set $\mathcal{X} = \{1,2,3,4\}$. Let $A$ be the event that $X \in \{1,2\}$ and $B$ be the event that $Y \in \{3\}$. Then we have $Pr(A, B) = Pr(A) /, Pr(B) = \frac{1}{2} \frac{1}{4}$ .
###### Probability of a union of two events
The probability of even $A$ or $B$ happening is given by
$$
Pr(A \cup B) = Pr(A) + Pr(B) - Pr(A \cap B)
$$
If the events are mutually exclusive we get 
$$
Pr(A \cup B) = Pr(A) + Pr(B)
$$
###### Conditional probability of one event given another
We define the **conditional probability** of event $B$ happening given that $A$ has occurred as follows
$$
Pr(B | A) \triangleq \frac Pr(A, B) \space {Pr(A)} 
$$
This is not defined if $Pr(A) = 0$ , since we cannot condition on an impossible event.

###### Independence of events
We say that event $A$  is independent of event $B$ if 
$$
Pr(A, B) = Pr(A) \space Pr(B)
$$
###### Conditional Independence of events
We say the events $A$ and $B$ are conditionally independent given event $C$ if 
$$
Pr(A, B | C) = Pr(A|C) \space Pr(B|C) 
$$
This is written as $A \perp B|C$ .  

### Random variables
If the value of $X$ is unknown and/or could change, we call it a **random variable** or **rv**. The set of possible values, denoted $\mathcal{X}$ is known as the **sample space** or **state space**. An event is a set of outcomes from a given sample space.
##### Discrete random variables
If the sample space $\mathcal{X}$ is finite or countably infinite, then $X$ is called a **discrete random variable** 
We denote the probability of the event that $X$ has value $x$ by $Pr(X= x)$ . 
We define the **probability mass function** as a function which computes the probability of events which correspond to setting the rv to each possible value:
$$
p(x) \triangleq Pr(X = x)
$$
The pmf satisfies the properties $0\le p(x) \le 1$ and $\sum_{x \in \mathcal{X}} p(x) = 1$.

##### Continuous random variables
if $X \in \mathbb{R}$ is a real-valued quantity, it is called a **continuous random variable**. 
###### Cumulative distribution function (cdf)
Define the events $A = (X \le a) , B = (X \le b )$ and $C= (a < X \le b)$ , where $a<b$ . We have the $B = A \cup C$ and since $A$ and $C$ are mutually exclusive, the sum rules gives
$$
Pr(B) = Pr(A) + Pr(C)
$$
and hence the probability of being in interval $C$ is given by 
$$
Pr(C) = Pr(B) - Pr(A)
$$
In general, we define the cumulative distribution function or cdf of the rv X as follows:
$$
P(x) \stackrel {\small \triangle}{=} Pr(X \le x) 
$$
Using this, we can compute the probability of being in any interval as follows :
$$
Pr(a < X \leq b) = P(b) - P(a)
$$
Cdf's are monotonically non-decreasing functions.

###### Probability Density function (pdf)
We define the **probability density function** as **pdf** as the derivative of the cdf :
$$
p(x) \triangleq \frac{d}{dx} P(x)
$$
Given a pdf, we can compute the probability of a continuous variable being in a finite interval as follows:
$$
Pr(a < X \leq b) = \int_{a}^b p(x) dx = P(b) - P(a)
$$
As the size of interval gets smaller, we can write 
$$
Pr(x < X \leq x + dx) \approx p(x) dx
$$
Intuitively, this says the probability of $X$ being in a small interval around $x$ is the density at $x$ times the width of the interval.
###### Quantiles
If the cdf $P$ is strictly monotonically increasing, it has an inverse, called the inverse cdf or percent point function (ppf) or quantile function.

If P is the cdf of $X$, then $P^{−1} (q)$ is the value $x_q$ such that $Pr(X ≤ xq) = q$; this is called the $q^{th}$ quantile of $P$. The value $P^{−1} (0.5)$ is the **median** of the distribution, with half of the probability mass on the left, and half on the right. The values $P^{−1 }(0.25)$ and $P^{−1} (0.75)$ are the **lower** and **upper** **quartiles**.
##### Sets of related random variables
Given a join distribution, we define the **marginal distribution** of an rv as follows:
$$
p(X=x) = \sum _{y}p(X = x, Y= y)
$$
This is sometimes called the **sum rule** or the rule of total probability.

We define the condition distribution of an rv using 
$$
p(Y= y|X=x) = \frac{p(X=x, Y=y) }{p(X= x)}
$$
We can rearrange this equation to get 
$$
p(x, y) = p(x)p(y|x)
$$
This is called the product rule.
By extending the product rule to $D$ variables, we get the **chain rule of probability**.
$$
p(x_{1:D}) = p(x_{1}) p(x_{2}|x_{1}) p(x_{3}|x_{1},x_{2})p(x_{4}|x_{1},x_{2},x_{3}) \dots p(x_{D}|x_{1:D-1})
$$

##### Independence and conditional independence
We say X and Y are unconditionally independent or marginally independent, denoted $X ⊥ Y$ , if we can represent the joint as the product of the two marginals.
$$
X \perp Y \Longleftrightarrow p(X, Y) = p(X)p(Y)
$$
we say a set of variables $X_{1},X_{2}, \dots X_{n}$ is (mutually) independent if the joint can be written as a product of marginals for all subsets $\{X_{1}, \dots, X_{m}\} \in \{X_{1}, \dots, X_{n}\}$:
$$
p(X_{1}, \dots, X_{m}) = \prod_{i=1}^{m} p(X_{i})
$$
We write $X$ and $Y$ are conditionally independent given $Z$ iff the conditional joint can be written as a product of conditional marginals.
$$
X \perp Y \perp X \Longleftrightarrow p(X, Y| Z) = p(X | Z)p(Y|Z)
$$

##### Moments of a distribution
###### Mean of a distribution
The most familiar property of a distribution is its **mean**, or expected value, often denoted by $\mu$ For continuos rv's the mean if defined as follows:
$$
\mathbb{E} [X] \triangleq \int _{\mathcal{X}} x\space p(x)
$$
If the integral is not finite , the mean is not defined.
For discreate rv's, the mean is defined as follows:
$$
\mathbb{E}[X] \triangleq \sum_{x \in \mathcal{X}} {x \space} p(x)
$$
However this is only meaningful if the values of $x$ are ordered in some way.
$\qquad$ Since the mean is a linear operator, we have
$$
\mathbb{E}[aX+b] = a\mathbb{E}[X] + b
$$
This is called the linearity of expectation.
###### Variance of a distribution
The variance is a measure of the spread of a distribution. often denoted by $\sigma^{2}$ 
This is defined as  :
$$
\begin{align}
\mathbb{V}[X] & \triangleq \mathbb{E}[(X- \mu)^{2}] = \int(x- \mu)^{2} \space p(x) dx  \\
& = \int x^{2}p(x)dx + \mu^{2} \int p(x)dx - 2\mu \int xp(x)dx \\
& = \mathbb{E}[X]^{2}  - \mu^{2}
\end{align}
$$
from which we derive the useful result
$$
\mathbb[{E}X_{2}] = \sigma^{2} + \mu^{2}
$$
The **standard deviation** is defined as 
$$
std[X] \triangleq \sqrt{ \mathbb{V}[X] } = \sigma
$$
###### Mode of a distribution
The **mode** of a distribution is the value with the highest probability mass or probability density : 
$$
\large x^{*} = \underset{x} {argmax} \space p(x)
$$
###### Conditional Moments
When we have two or more dependent random variables, we can compute the moments of one given knowledge of the other. 
- Law of iterated expectations (law of total expectation) :
$$
\mathbb{E}[x] = \mathbb{E}_{Y} [\mathbb{E} [X|Y]]
$$
- Law of total variance (conditional variance formula ):
$$
\mathbb{V}[X] = \mathbb{E}[\mathbb{V}[X|Y]] + \mathbb{V}[\mathbb{E}[X|Y]]
$$
#### Limitation of summary Statistics
Although it is common to summarize a probability distribution using simple statistics such as mean and variance, this can lose a lot of information. 
A striking example of this is known as Anscombe's quartet.
### Bayes' rule

> [!quote] Sir Harold Jefferys, 1973
> Bayes' theorem is to the theory of probability what pythagoras's theory to geometry

Inference means "the act of passing from sample data to generalization, usually with calculated degrees of certainty". And the term "Bayesian" is used to refer to inference methods that represent "degree of certainty" using probability theory.

Bayes' rule itself is very sample; it is just a formula for computing the probability distribution over possible values of an unknown quantity $H$ given some observed data $Y = y$.
$$
p(H = h|Y = y) = \frac{p(H = h) \space p(Y = y) \space p(H = h)}{p(Y = y)}
$$
This follows automatically from the identity 
$$
p(h|y) \space p(y) = p(h) \space p(y|h) = p(h, y)
$$
In this equation the term $p(H)$ represents **prior distribution**, The term $p(Y|H = h)$ represents **observation distribution**. $p(Y = y | H = h)$ represents the **likelihood**. $p(Y = y)$ is known as the **marginal likelihood**. $p(H = h | Y = y)$ is the **posterior distribution**. 

We can summarize Bayes rule in words as follows : 
$$
\text{posterior } \propto \text{ prior } \times \text{likelihood}
$$
Using Bayes rule to update a distribution over unknown values of some quantity of interest, given relevant observed data, is called **Bayesian inference**, or **posterior inference**. It can also just be called **probabilistic inference**.

#### Inverse problems
Probability theory is concerned with predicting a distribution over outcomes $y$ given knowledge (or assumptions) about the state of the world, $h$. By contrast, inverse probability is concerned with inferring the state of the world from observations of outcomes. We can think of this as inverting the $h → y$ mapping.

### Bernoulli and binomial distributions
##### Definition
Consider tossing a coin, where the probability of event that it lands heads is given by $0 ≤ θ ≤ 1$. Let $Y = 1$ denote this event, and let $Y = 0$ denote the event that the coin lands tails. Thus we are assuming that $p(Y = 1) = θ$ and $p(Y = 0) = 1 − θ$. This is called the Bernoulli distribution, and can be written as follows
$$
Y \sim Ber(\theta)
$$
where the symbol $\sim$ means "is sampled from" or "is distributed as", and Ber refers to Bernoulli. The probability mass function of this distribution is defined as follows:
$$
Ber(y|\theta) = \begin{cases}
1 - \theta  & \text{if } y = 0  \\
\theta  & \text{if } y = 1
\end{cases}
$$
We can write this in a more concise manner as follows :
$$
Ber(y|\theta) \stackrel {\triangle} {=} \theta ^y (1- \theta) ^{1-y}
$$
##### Sigmoid (logistic) function
When we want to predict a binary variable $y ∈ {0, 1}$ given some inputs $x ∈ X$ , we need to use a conditional probability distribution of the form
$$
p(y|x, \theta) = Ber(y| f(x; \theta))
$$
where $f(x;\theta)$ is some function that predicts the mean parameter of the output distribution. 

$$
\sigma (a) \triangleq \frac{1}{1+e^{-a}}
$$
where $a = f(x; \theta)$. sigmoid means "s-shaped".
##### Binary logistic regression
In this, we use a conditional bernouli model, where we use a linear predictor of the form $f(y | x;\theta) = w^T x  +b$. Thus the model has the form 
$$
p(y | x; \theta) = Ber(y | \sigma)
$$
In other words, 
$$
p(y = 1 | x; \theta) = \sigma (w^T + b) = \frac{1}{1 + e^{-w^Tx + b}}
$$
This is called the **logistic regression**.

### Categorical and multinomial distributions
To represent a distribution over a finite set of labels $y\in \{1, \dots, C\}$, we can use the categorical distribution which generalizes the Bernoulli to $C>2$ values.
The categorical distribution is a discrete probability distribution with one parameter per class :
$$
Cat(y|\theta) \triangleq {\prod_{c=1}^{C} \theta _{c}^{\mathbb{I}(y=c)}}
$$

##### Softmax function

$$
softmax(a) \triangleq \left[ \frac{e^{a_{1}}}{\sum_{c'=1}^{C} e^{a_{c'}}}, \dots, \frac{e^{a_{C}}} {\sum_{c'=1}^{C} e^{a_{c'}}} \right]
$$

##### Multiclass logistic regression

$$
p(y = c|x;\theta) = \frac{e^{a_{c}}}{\sum_{c'=1}^{C}e^{a_{c'}}}
$$
This is known as multinomial logistic regression.

### Univariate Gaussian distribution
The most widely used distribution of real-valued random variables $y \in \mathbb{R}$ is the Gaussian Distribution, also called the normal distribution.

##### Cumulative distribution function

$$
P(y) \triangleq \text{Pr} (Y \leq y)
$$
$\text{P}$ represents the cdf. Using this, we can compute the probability of being in any interval as follows:
$$
Pr(a < Y \leq b) = P(b) - P(a)
$$
Cdf's are monotonically non-decreasing functions.
The cdf of the Gaussian is defined by 
$$
\Phi (y; \mu, \sigma^{2}) \triangleq \int_{-\infty}^{y} \mathcal{N}(z | \mu, \sigma^{2})dz
$$

##### Probability Density function
We define the probability density function or pdf as a derivate of the cdf:
$$
p(y) \triangleq \frac{d}{dy} P(y)
$$
The pdf of the Gaussian is given by 
$$
\large{
\mathcal{N}(y|\mu, \sigma^{2}) 
\triangleq \frac{1}{\sqrt{ 2\pi \sigma^{2} }} e^{-\frac{1}{2\sigma^{2}}(y- \mu)^{2}}}
$$

where $\sqrt{2\pi \sigma^{2}}$ is the normalization constant needed to ensure the density integrates to 1.

##### Regression

##### Dirac delta function as a limiting case
As the variance of a Gaussian goes to 0, the distribution approaches an infinitely narrow, but infinitely tall, “spike” at the mean. We can write this as follows:
$$
\lim_{ \sigma \to 0 } \mathcal{N}(y|\mu, \sigma^{2}) \to \delta (y-\mu) 
$$
where $\delta$ is the Dira delta function, defined by
$$
\delta (x) = \begin{cases}
+ \infty & if\, x =0 \\
0 & if\, x \neq 0
\end{cases}
$$
where $\int_{-\infty}^{\infty} \delta(x)dx = 1$ .
### Some other common univariate distributions

##### Student t distribution
The Gaussian distribution is quite sensitive to outliers. A robust alternative to the Gaussian is the Student t-distribution, which we shall call the Student distribution for short.9 Its pdf is as follows: 
$$
\large
\mathcal{T}(y|\mu, \sigma^{2}, v) \propto \left[ 1 + \frac{1}{v} (\frac{y-\mu}{\sigma})^{2}\right ]^{(\frac{v+1}{2})}
$$
where $\mu$ is the mean, $\sigma >0$ is the scale parameter and $v>0$ is called the degrees of freedom(degree of normality).
##### Cauchy distribution
If $v=1$ , the Student distribution is known as the Cauchy or Lorentz distribution. Its pdf is defined as
$$
\mathcal{C}(x|\mu, \gamma) = \frac{1}{\gamma \pi} \left[ 1+ \left( \frac{x- \mu}{\gamma} \right)^{2} \right] ^{-1} 
$$

##### Laplace distribution
Another distribution with heavy tails is the Laplace distribution, also known as the double sided exponential distribution. This has the following pdf: 
$$
Laplace(y|\mu, b) \triangleq \frac{1}{2b} \exp \big{(}- \frac{|y- \mu|} {b}\big{)}

$$
Here $\mu$ is the location parameter and $b>0$ is a scale parameter.
##### Beta Distribution 
The beta distribution has support over the interval $[0, 1]$ and is defined as follows:
$$
\text{Beta} (x|a,b) = \frac{1}{B(a, b)} x^{a - 1} (1-x)^{ b-1}
$$
where $B(a, b)$ is the beta function defined by 
$$
B(a, b) \triangleq \frac{\Gamma(a) \Gamma(b)}{\Gamma(a+b)}
$$
where $\Gamma(a)$ is the Gamma function defined by 
$$
\Gamma(a) \triangleq \int_{0}^{\infty}x^{a-1}e^{-x}dx
$$
##### Gamma distribution
The gamma distribution is a flexible distribution for positive real valued rv’s, $x > 0$. It is defined in terms of two parameters, called the shape $a > 0$ and the rate $b > 0$:
$$
Ga(x|\text{shape} = a, \text{rate} = b) \triangleq b^{a-1}e^{-xb}
$$
###### Special cases of Gamma
- Exponential distribution
- Chi-squared distribution
- inverse Gamma distribution
##### Empirical distribution

$$
\hat{p}_{N}(x) = \frac{1}{N} \sum_{n=1}^{N} \delta_{x(n)} (x)
$$
This is called the empirical distribution of the dataset $\mathcal{D}$ 
### Transformation of random variables
Suppose $x \sim p()$ is some random variable, and $y=f(x)$ is some deterministic transformation of it. 
##### Discrete case
If $X$ is a discrete rv, we can derive the pmf for $Y$ by simply summing up the probability mass for all the x's such that $f(x) = y$:
$p_{y(y)} = \sum_{x:f(x) = y} p_{x}(x)$
##### Continuous case
If $X$ is continuous, we work with cdf's as follows:
$$
P_{y}(y) \triangleq \text{Pr}(Y \leq y) = \text{Pr}(f(X) \leq y) = \text{Pr}(X \in \{ x | f(x) \leq y \})
$$
If $f$ is invertible, we can derive the pdf of $y$ by differentiating the cdf, If $f$ is not invertible, we can use numerical integration, or Monte Carlo approximation.
##### Invertible transformation (Bijections)
###### Change of scalars
Suppose $x\sim \mathrm{Unif}(0,1)$ and $y=f(x) = 2x+1$. This function stretches and shifts the probability distribution, 
###### Change of variables
##### Moments of a linear transformation
##### The convolution theorem
Let $y= x_{1}+x_{2}$ where $x_{1}$ and $x_{2}$ are independent rv's. If these are discrete random variables we can compute the pmf for the sum as follows:
$$
p(y=j) = \sum_{k} p(x_{1}=k)p(x_{2}= j-k) 
$$
for $j=\dots, -2, -1, 0, 1, 2, \dots$
If $x_{1}$ and $x_{2}$ have pdf's $p_{1}(x_{1})$ and $p_{2}(x_{2})$. what is the distribution of $y$?
The cdf for $y$ is given by
$$
P_{y}(y^{*}) = \mathrm{Pr}(y\leq y^{*}) = \int_{-\infty} ^{\infty} p_{1}(x_{1}) \left[ \int_{-\infty}^{y^{*}-x_{1}}p_{2}(x_{2})dx_{2}\right] \, dx_{1} 
$$
Where we integrate over the region $R$ defined by $x_{1}+x_{2} < y^{*}$ Thus the pdf for $y$ is 
$$
p(y) = \left[\frac{d}{dy^{*}} P_{y}(y^{*})\right]_{y*=y} = \int p_{1}(x_{1}) \space p_{2}(y- x_{1}) dx_{1}
$$
where we used the rule of differentiating under the integral sign:
$$
\frac{d}{dx} \int_{a(x)}^{b(x)} f(t)dt = f(b(x)) \frac{db(x)}{dx} - f(a(x)) \frac{da(x)}{dx}
$$
We can write this as 
$$
p = p_{1} \circledast p_{2}
$$
where $\circledast$ represents the convolution operator. and this theorem is called convolution theorem.
##### Central limit theorem
Consider $N$ random variables with pdf's (not necessarily Gaussian) $p_{n}(x)$ each with mean $\mu$ and variance $\sigma^{2}$ , We assume each variable is **independent and identically distributed** which means $X_{n} \sim p(X)$ are independent samples from the same distribution.  Let  $S_{N} = \sum_{n=1}^{N} X_{n}$ be the sum of the rv's. As N increases the distribution of this sum approaches 
$$
p(S_{N} = u) = \frac{1}{\sqrt{ 2\pi N \sigma^{2} }} \exp\left( -\frac{(u-N\mu)^{2}}{2N\sigma^{2}} \right)
$$
Hence the distribution of the quantity 
$$
Z_{N} \triangleq \frac{S_{N} - N\mu}{\sigma \sqrt{ N }} = \frac{\bar{X} - u}{\frac{\sigma}{\sqrt{N}}}
$$
converges to the standard normal, where $\bar X = S_{N} / N$ is the sample mean. This is called the **central limit theorem**.
##### Monte Carlo approximation
Suppose $x$ is a random variable, and $y = f(x)$ is some function of $x$. It is often difficult to compute the induced distribution $p(y)$ analytically. One simple but powerful alternative is to draw a large number of samples from the x’s distribution, and then to use these samples (instead of the distribution) to approximate $p(y)$. For example, suppose $x ∼ Unif(−1, 1)$ and $y = f(x) = x^{2}$ . We can approximate $p(y)$ by drawing many samples from $p(x)$ (using a uniform random number generator), squaring them, and computing the resulting empirical distribution, which is given by
$$
P_{S}(y) \triangleq \frac{1}{N} \sum_{s=1}^{N_{s}} \delta (y- y_{s}) 
$$
This approach is called a **Monte Carlo approximation**.
___
# Multivariate Models
### Joint distributions for multiple random variables
#### Covariance
The covariance between two rv's X and Y measures the degree to which X and Y are (linearly) related. 
$$
\text{Cov}[X, Y] \triangleq \mathbb{E}[(X- \mathbb{E}[X]) (Y- \mathbb{E}[Y])] = \mathbb{E}[XY] - \mathbb{E}[X]E[Y]
$$
If $x$ is a D-dimensional random vector, its covariance matrix is defined to be the following symmetric, positive semi definite matrix :
$$
\begin{align}
\text{Cov}[x] & \triangleq \mathbb{E}[(x-\mathbb{E}[x]) (x- \mathbb{E}[x])^{T}] \triangleq \tiny {\sum} \\
&
\left(\begin{array} {cc}
\mathbb{V[X_{1}]} & \text{Cov}[X_{1}, X_{2}] & \dots & \text{Cov}[X_{1}, X_{D}]  \\
\text{Cov}[X_{2}, X_{1}] & \mathbb{V}[X_{2}] & \dots & \text{Cov}[X_{2}, X_{D}]  \\
\vdots & \vdots & \vdots & \vdots  \\
\text{Cov}[X_{D}, X_{1}] & \text{Cov}[X_{D}, X_{2}] & \dots & \mathbb{V}[X_{D}]
\end{array} \right)

\end{align}
$$

The **Cross-variance** between two random vectors is defined as 
$$
\text{Cov}[x,y] = \mathbb{E} [(x- \mathbb{E}[x]) (y-\mathbb{E}[y])^{T}]
$$

#### Correlation
Covariances can be between negative and positive infinity. Sometimes it is more convenient to work with a normalized measure, with a finite lower and upper bound. The (Pearson )Correlation coefficient between $X$ and $Y$ is defined as
$$
\rho \triangleq corr[X, Y] \triangleq \frac{Cov[X, y]}{\sqrt{ \mathbb{V}[X] \mathbb{V}[Y] }}
$$
In the case of a vector $x$ of related random variables, the correlation matrix is given by 
$$
\text{corr}(x) = \left( \begin{array} {cc}
1 & \frac{\mathbb{E}[(X_{1} - \mu_{1}) (X_{2} - \mu_{2})]}{\sigma_{1} \sigma_{2}} &  \dots & \frac{\mathbb{E}[(X_{1} - \mu_{1}) (X_{D} 0 \mu_{D})]}{\sigma_{1} \sigma_{D}}  \\
\frac{\mathbb{E}[X_{2}-\mu_{2} (X_{1} - \mu_{1})]}{\sigma_{2}\sigma_{1}} & 1 & \dots &\frac{\mathbb{E}(X_{2}-\mu_{2})(X_{D - \mu_{D}})}{\sigma_{2} \sigma_{D}}  \\
 \vdots & \vdots & \vdots  & \vdots \\
\frac{\mathbb{E}[(X_{D} - \mu_{D} ) (X_{1} - \mu_{1})]}{\sigma_{D} \sigma_{1}} & \frac{\mathbb{E}[(X_{D}- \mu_{D}) (X_{2}-\mu_{2})]}{\sigma_{D}\sigma_{2}} & \dots 1
\end{array} \right)
$$
This can be written more compactly as 
$$
\text{corr}(x) = (\text{diag}(K_{xx}))^{-1/2} K_{xx}(\text{diag}(K_{xx}))^{-1/2}
$$
where $K_{xx}$ is the auto-covariance matrix
$K_{xx} = \sum=\mathbb{E}[(x-\mathbb{E}[x])(x-\mathbb{E}[x])^{T}]=R_{xx}-\mu \mu^{T}$
and $R_{xx} = \mathbb{E}[xx^{T}]$ is the auto correlation matrix.

- Uncorrelated does not imply independent
- Correlation does not imply causation
### The multivariate Gaussian distribution
The MVN density is defined as 
$$
\mathcal{N}(y|\mu, \Sigma) \triangleq \frac{1}{(2\pi)^{D/2}|\Sigma|^{1/2}} \exp\left[ -\frac{1}{2}  (y_{0} \mu)^{T} \Sigma^{-1} (y -\mu)\right]
$$
where $\mu = \mathbb{E}[y] \in \mathbb{R}^{D}$ is the mean vector, and $\Sigma= Cov[y]$ is the $D\times D$ covariance matrix defined as follows :
$$
\text{Cov}[y] \triangleq \mathbb{E} \left[(y-\mathbb{E}[y]) (y - \mathbb{R}[y]^{T})\right]
$$
### Linear Gaussian systems
Let $z\in \mathbb{R}^{L}$ eb an unknown vector of values, and $y\in R^{D}$ be some noisy measurement of $z$ . we assume these variable are related by the following joint distribution:
$$
\begin{align}
p(z) = \mathcal{N}(z|\mu_{z}, \Sigma_{z})  \\
p(y|z)= \mathcal{N}(y|Wz + b,\Sigma_{y})
\end{align}
$$
Where $W$ is the matrix of size $D\times L$ . This is an example of a linear Gaussian System.

#### Bayes Rule for Gaussians
The posterior over the latent is given by

$$
\begin{align}
p(z|y) & = \mathcal{N}(z|\mu_{z|y}, \Sigma_{z|y}) \\
\Sigma_{z|y}^{-1} &= \Sigma_{z}^{-1} + W^{T}\Sigma_{y}^{-1}W \\
\mu_{z|y} &= \Sigma_{z|y} [W^{T}\Sigma^{-1}_{y}(y-b) + \Sigma^{-1}_{z}\mu_{z}] \\
\end{align}
$$
This is known as Bayes rule for Gaussians. 

### The exponential family
we define the **exponential family** which includes many common probability distributions parameterized by $\eta \in \mathbb{R}^{k}$ with fixed support over $\mathcal{Y}^{D } \subseteq \mathbb{R}^{D}$. we say that the distribution $p(y|\eta)$ is in the exponential family if its density can be written in the following way:
$$
p(y|\eta) \triangleq \frac{1}{Z(\eta)} h(y) \exp[\eta^{T}\mathcal{T}(y)] = h(y) \exp[\eta^{T}(y) - A(\eta)]
$$
where $h(y)$ is the scaling constant  (base measure), $\mathcal{T}(y) \in \mathbb{R}^{K}$ are the sufficient statistics $\eta$ are the natural parameters or canonical parameters, $Z(\eta)$ is a normalization constant known as the **partition function** and $A(\eta)=\log Z(\eta)$ is the **log partition function**.
### Mixture models
One way to create more complex probability models is to take a convex combination of simple distribution, This is called a mixture model and has the form
$$
p(y|\theta) = \sum_{k=1}^K \pi_{k}p_{k}(y) 
$$
where $p_{k}$ is the kth mixture component and $\pi_{k}$ are the mixture weights which satisfy $0\leq \pi_{k} \leq 1$ and $\sum_{k=1}^{K}\pi_{k} = 1$.

##### Gaussian mixture models
A Gaussian mixture model also called a mixture of Gaussians is defined as follows:
$$
p(y|\theta) = \sum_{k=1}^{K} \pi_{k}\mathcal{N}(y|\mu_{k}, \Sigma_{k}) 
$$

##### Bernoulli mixture models
IF the data is binary values, we can use a Bernoulli mixture model where each mixture components has the following form:
$$
p(y|z =k,\theta) = \prod_{d=1}^{D} \mathrm{Ber}(y_{d|\mu_{dk}}) = \prod_{d=1}^{D} \mu_{dk}^{y_{d}} (1- \mu_{dk})^{1-y_{d}} 
$$
Here $\mu_{dk}$ is te probability that bit $d$ turns on in cluster k.
### Probabilistic graphical models
##### Representation
A probabilistic graphical model is a joint probability distribution that uses a graph structure to encode conditional independence assumptions. Ehen the graph is directed acyclic graph the model is sometimes called Bayesian network.

The basic idea in PGMs is that each node in the graph represents a random variable, and each edge represents a direct dependency. More precisely, each lack of edge represents a conditional independency. In the DAG case, we can number the nodes in topological order (parents before children), and then we connect them such that each node is conditionally independent of all its predecessors given its parents:

where $pa(i)$ are the parents of node $i$, and $pred(i)$ are the predecessors of node $i$ in the ordering. (This is called the ordered Markov property.) Consequently, we can represent the joint distribution as follows:
$$
\huge{p(\mathrm{Y}_{1 : N_{G}}) = \prod_{i=1}^{N_{G}} p\left(Y_{i|\mathrm{Y}_{pa(i)}}\right) }
$$
where $N_G$ is the number of nodes in the graph.
##### inference
A PGM defines a joint probability distribution. We can therefore use the rules of marginalization and conditioning to compute $p(Y_i |Y_j = y_j )$ for any sets of variables $i$ and $j$.
##### Learning
f the parameters of the CPDs are unknown, we can view them as additional random variables, add them as nodes to the graph, and then treat them as hidden variables to be inferred.

More precisely, the model encodes the following “generative story” about the data:
$$
\begin{align}
\mathrm{\theta} \sim p(\mathrm{\theta}) \\
\mathrm{y}_{n} \sim p(\mathrm{y|\theta})
\end{align}
$$
where $p(\mathrm{\theta})$ is some prior over the parameters, and $p(y|\theta)$ is some specified function. 

___
$$
***
$$
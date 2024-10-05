# Discrete Probability
## An Introduction to Discrete Probability
#### Finite Probability
An **experiment** is a procedure that yields one of a given set of possible outcomes.
The **sample space** of the experiment is the set of possible outcomes. An **event** is a subset of the sample space. Laplace's definition of the probability of an event with finitely many possible outcomes will now be stated.

* **Definition** :
  If $S$ is a finite nonempty sample space of equally likely outcomes, and $E$ is an event, that is, a subset of $S$, then the probability of $E$ is $p(E) = \huge \frac {|E|}{|S|}$.
#### Probabilities of Complements and Unions of Events
We can use counting techniques to find the probability of events derived from other events.

* **Theorem** :
  Let $E$ be an event in a sample space $S$. The probability of the event $E = S - E$, the complementary event of $E$, is given by $$\begin{align*}
  & p(\overline{E}) = 1 - p(E). &
  \end{align*}$$
* **Theorem** :
  Let $E_1$ and $E_2$ be events in the sample space $S$. Then $$\begin{align*}
  &   p(E_1 \cup E_2) = p(E_1) + p(E_2) - p(E_1 \cap E_2). &
  \end{align*}$$
## Probability Theory
#### Assigning Probabilities
Let $S$ be the sample space of an experiment with a finite or countable number of outcomes. We assign a probability $p(s)$ to each outcome $s$. We require that two conditions be met:
* (I) $0 \leq p(s) \leq 1$ for each $s \in S$ and
* (II) $\sum_{s \in S} \space p(s) = 1$.

(Note that when the sample space is infinite, $\sum_{s \in S} \space p(s)$ is a convergent infinite series.)
This is a generalization of Laplace's definition in which each of n outcomes is assigned a probability of $1 / n$. Indeed, conditions (I) and (II) are met when Laplace's definition of probabilities of equally likely outcomes is used and $S$ is finite.
Note that when there are $n$ possible outcomes, $x_1, x_2, \ldots, x_n$, the two conditions to be
met are 
* (I) $0 \leq p(x_i) \leq 1$ for $i = 1, 2, \ldots, n$ and
* (II) $\sum_{i = 1}^n \space p(x_i) = 1$.

The function $p$ from the set of all outcomes of the sample space $S$ is called a **probability distribution**.
To model an experiment, the probability $p(s)$ assigned to an outcome $s$ should equal the limit of the number of times $s$ occurs divided by the number of times the experiment is performed, because this number grows without bound.
* **Definition** :
  Suppose that $S$ is a set with $n$ elements. The uniform distribution assigns the probability $1 / n$ to each element of $S$.
* **Definition** :
  The probability of the event $E$ is the sum of the probabilities of the outcomes in $E$. That is, $$\begin{align*}
  & p(E) = \sum_{s \in E} p(s). &
  \end{align*}$$(Note that when $E$ is an infinite set, $\sum_{s \in E} \space p(s)$ is a convergent infinite series.)

Note that the uniform distribution assigns the same probability to an event that Laplace's original definition of probability assigns to this event.
The experiment of selecting an element from a sample space with a uniform distribution is called selecting an element of $S$ **at random**.
* **Theorem** :
  If $E_1, E_2, \ldots$ is a sequence of pairwise disjoint events in a sample space $S$, then $$\begin{align*}
  & p (\bigcup_i E_i) = \sum_i p(E_i). &
  \end{align*}$$(Note that this theorem applies when the sequence $E_1, E_2, \ldots$ consists of a finite number or a countably infinite number of pairwise disjoint events.)
#### Conditional Probability
In general, to find the **conditional probability** of $E$ given $F$, we use $F$ as the sample space. For an outcome from $E$ to occur, this outcome must also belong to $E \cap F$.
* **Definition** :
  Let $E$ and $F$ be events with $p(F) > 0$. The **conditional probability** of $E$ given $F$, denoted by $p(E \mid F)$, is defined as $$\begin{align*}
  & p (E \mid F) = \frac{p(E \cap F)}{p(F)}. &
  \end{align*}$$
#### Independence
* **Definition** :
  The events $E$ and $F$ are **independent** if and only if $p(E \cap F) = p(E)p(F)$.
###### Pairwise and Mutual Independence
* **Definition** :
  The events $E_1, E_2, \ldots, E_n$ are **pairwise independent** 
  if and only if $p(E_i \cap E_j) = p(E_i)p(E_j)$ for all pairs of integers $i$ and $j$ with $1 \leq i < j \leq n$.
  These events are **mutually independent** 
  if $p(E_{i_1} \cap E_{i_2} \cap \ldots \cap E_{i_m}) = p(E_{i_1})p(E_{i_2}) \ldots p(E_{i_m})$ whenever $i_j, j = 1, 2, \ldots, m$, are integers with $1 \leq i_1 < i_2 < \ldots < i_m \leq n$ and $m \geq 2$.

#### Bernoulli Trials and the Binomial Distribution
Suppose that an experiment can have only two possible outcomes. For instance, when a bit is generated at random, the possible outcomes are $0$ and $1$. When a coin is flipped, the possible outcomes are heads and tails. Each performance of an experiment with two possible outcomes is called a **Bernoulli trial**, after James Bernoulli.
In general, a possible outcome of a Bernoulli trial is called a **success** or a **failure**. If $p$ is the probability of a success and $q$ is the probability of a failure, it follows that $p + q = 1$. Many problems can be solved by determining the probability of $k$ successes when an experiment consists of $n$ mutually independent Bernoulli trials.
(Bernoulli trials are **mutually independent** if the conditional probability of success on any given trial is $p$, given any information whatsoever about the outcomes of the other trials.)

* **Theorem** :
  The probability of exactly $k$ successes in $n$ independent Bernoulli trials, with probability of success $p$ and probability of failure $q = 1 - p$, is $C(n, k)p^k q^{n - k}$.
#### Random Variables
A **random variable** is a function from the sample space of an experiment to the set of real numbers. That is, a random variable assigns a real number to each possible outcome.

* **Definition** :
  The distribution of a random variable $X$ on a sample space $S$ is the set of pairs $(r, p(X = r))$ for all $r \in X(S)$, where $p(X = r)$ is the probability that $X$ takes the value $r$.
  The set of pairs in this distribution is determined by the probabilities $p(X = r)$ for $r \in X(S)$.

#### The Probabilistic Method
* **Theorem** : The Probabilistic Method
  If the probability that an element chosen at random from a $S$ does not have a particular property is less than $1$, there exists an element in $S$ with this property.
* **Theorem** :
  If $k$ is an integer with $k \geq 2$, then $R(k, k) \geq 2^{k /2}$.
## Bayes' Theorem
* **Theorem** : Bayes' Theorem
  Suppose that $E$ and $F$ are events from a sample space $S$ such that $p(E) \ne 0$ and $p(F) \ne 0.$
  Then $$\begin{align*}
  & p(F \mid E) = \frac {p(E \mid F)p(F)} {p(E \mid F)p(F) + p(E \mid \overline{F})p(\overline{F})}. &
  \end{align*}$$
###### Generalizing Bayes' Theorem
Note that in the statement of Bayes' theorem, the events $F$ and $\overline{F}$ are mutually exclusive and cover the entire sample space $S$ (that is, $F \cup \overline{F} = S$). We can extend Bayes' theorem to any collection of mutually exclusive events that cover the entire sample space $S$, in the following way.
* **Theorem** : Generalized Bayes' Theorem
  Suppose that $E$ is an event from a sample space $S$ and that $F_1, F_2, \ldots, F_n$ are mutually exclusive events such that $\bigcup_{i = 1}^n F_i = S$.
  Assume that $p(E) \ne 0$ and $p(F_i) \ne 0$ for $i = 1, 2, \ldots, n$. Then $$\begin{align*}
  & p(F_j \mid E) = \frac {p(E \mid F_j)p(F_j)} {\sum_{i = 1}^n p(E \mid F_i)p(F_i)}. &
  \end{align*}$$
## Expected Value and Variance
The **expected value** of a random variable is the sum over all elements in a sample space of the product of the probability of the element and the value of the random variable at this element. Consequently, the expected value is a weighted average of the values of a random variable. The expected value of a random variable provides a central point for the distribution of values of this random variable.
* **Definition** :
  The **expected value**, also called the **expectation** or **mean**, of the random variable $X$ on the sample space $S$ is equal to $$\begin{align*}
  & E(X) = \sum_{s \in S} p(s) X(s). &
  \end{align*}$$The **deviation** of $X$ at $s \in S$ is $X(s) - E(X)$, the difference between the value of $X$ and the mean of $X$.

* **Theorem** :
  If $X$ is a random variable and $p(X = r)$ is the probability that $X = r$, so that $p(X = r) = \sum_{s \in S, X(s)=r} p(s)$, then $$\begin{align*}
  & E(X) = \sum_{r \in X(S)} p(X = r)r. &
  \end{align*}$$

* **Theorem** :
  The expected number of successes when $n$ mutually independent Bernoulli trials are performed, where $p$ is the probability of success on each trial, is $np$.

#### Linearity of Expectations
* **Theorem** :
  If $X_i, i = 1, 2, \ldots, n$ with $n$ a positive integer, are random variables on $S$, and if $a$ and $b$ are real numbers, then
  * (I) $E(X_1 + X_2 + \ldots + X_n) = E(X_1) + E(X_2) + \ldots + E(X_n)$,
  * (II) $E(aX + b) = aE(X) + b$.

#### Average-Case Computational Complexity
Computing the average-case computational complexity of an algorithm can be interpreted as computing the expected value of a random variable.
Let the sample space of an experiment be the set of possible inputs $a_j, j = 1, 2, \ldots, n,$ and let $X$ be the random variable that assigns to $a_j$ the number of operations used by the algorithm when given $a_j$ as input. Based on our knowledge of the input, we assign a probability $p(a_j)$ to each possible input value $a_j$. Then, the average-case complexity of the algorithm is $$\begin{align*}
& E(X) = \sum_{j = 1}^{n} p(a_j)X(a_j). &
\end{align*}$$This is the expected value of $X$.

#### The Geometric Distribution
We now turn our attention to a random variable with infinitely many possible outcomes.
* **Definition** :
  A random variable $X$ has a **geometric distribution with parameter** $p$ if $p(X = k) = (1 - p)^{k - 1}p$ for $k = 1, 2, 3, \ldots$, where $p$ is a real number with $0 \leq p \leq 1$.
* **Theorem** :
  If the random variable $X$ has the geometric distribution with parameter $p$, then $E(X) = 1 / p$.
#### Independent Random Variables
* **Definition** :
  The random variables $X$ and $Y$ on a sample space $S$ are independent if $$\begin{align*}
  & p(X = r_1 \space \text{and} \space Y = r_2) = p(X = r_1) \cdot p(Y = r_2), &
  \end{align*}$$Or in words, if the probability that $X = r_1$ and $Y = r_2$ equals the product of the probabilities that $X = r_1$ and $Y = r_2$, for all real numbers $r_1$ and $r_2$.

* **Theorem** :
  If $X$ and $Y$ are independent random variables on a sample space $S$, then $E(XY) = E(X)E(Y)$.
  
#### Variance
The expected value of a random variable tells us its average value, but nothing about how widely its values are distributed. However, the random variable $X$ never varies from $0$, while the random variable $Y$ always differs from $0$ by $1$. The variance of a random variable helps us characterize how widely a random variable is distributed. In particular, it provides a measure of how widely $X$ is distributed about its expected value.
* **Definition** :
  Let $X$ be a random variable on a sample space $S$. The **variance** of $X$, denoted by $V(X)$, is $$\begin{align*}
  & V(X) = \sum_{s \in S}(X(s) - E(X))^2 p(s). &
  \end{align*}$$That is, $V(X)$ is the weighted average of the square of the deviation of $X$. 
The **standard deviation** of $X$, denoted $\sigma (X)$, is defined to be $\sqrt{V(X)}$.

* **Theorem** :
  If $X$ is a random variable on a sample space $S$, then $V(X) = E(X^2) − E(X)^2$.
* **Corollary** :
  If $X$ is a random variable on a sample space $S$ and $E(X) = \mu$, then $V(X) = E((X - μ)^2)$.
* **Theorem** : Bienaymé's Formula
   If $X$ and $Y$ are two independent random variables on a sample space $S$, then $V(X + Y) = V(X) + V(Y)$.
   Furthermore, if $X_i, i = 1, 2, \ldots, n$, with $n$ a positive integer, are pairwise independent random variables on $S$, then $V(X_1 + X_2 + \ldots + X_n) = V(X_1) + V(X_2) + \ldots + V(X_n)$.

#### Chebyshev’s Inequality
* **Theorem** : Chebyshev’s Inequality
  Let $X$ be a random variable on a sample space $S$ with probability function $p$. If $r$ is a positive real number, then $p(|X(s) - E(X)| \geq r) \leq V(X) / r^2$.


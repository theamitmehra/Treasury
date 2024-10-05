# Counting
## The Basics of Counting
Counting problems arise throughout mathematics and computer science. For example, we must count the successful outcomes of experiments and all the possible outcomes of these experiments to determine probabilities of discrete events. We need to count the number of operations used by an algorithm to study its time complexity.
#### Basic Counting Principles
We first present two basic counting principles, the **product rule** and the **sum rule**.
* **The Product Rule** :
  Suppose that a procedure can be broken down into a sequence of two tasks. If there are $n_1$ ways to do the first task and for each of these ways of doing the first task, there are $n_2$ ways to do the second task, then there are $n_1 n_2$ ways to do the procedure.
* **The Sum Rule** :
  If a task can be done either in one of $n_1$ ways or in one of $n_2$ ways, where none of the set of $n_1$ ways is the same as any of the set of $n_2$ ways, then there are $n1 + n2$ ways to do the task.

The sum rule can be phrased in terms of sets as: If $A_1, A_2, \ldots, A_m$ are pairwise disjoint finite sets, then the number of elements in the union of these sets is the sum of the numbers of
elements in the sets.
To relate this to our statement of the sum rule, note there are $|A_i|$ ways to choose an element from $A_i$ for $i = 1, 2, \ldots, m$. Because the sets are pairwise disjoint, when we select an element from one of the sets $A_i$, we do not also select an element from a different set $A_j$. Consequently, by the sum rule, because we cannot select an element from two of these sets at the same time, the number of ways to choose an element from one of the sets, which is the number of elements in the union, is $$\begin{align*}
& |A_1 \cup A_2 \cup \ldots \cup A_m| = |A_1| + |A_2| + \ldots + |A_m| \space \text{when} \space A_i \cap A_j = \phi \space \text{for all} \space i, j. &
\end{align*}$$This equality applies only when the sets in question are pairwise disjoint. 

Suppose that a task can be done in one of two ways, but some of the ways to do it are common to both ways. In this situation, we cannot use the sum rule to count the number of ways to do the task. To correctly count the number of ways to do the two tasks, we must subtract the number of ways that are counted twice. This leads us to an important counting rule.
* **The Subtraction Rule** :
  If a task can be done in either $n_1$ ways or $n_2$ ways, then the number of ways to do the task is $n_1 + n_2$ minus the number of ways to do the task that are common to the two different ways.

The subtraction rule is also known as the **principle of inclusion–exclusion**, especially when it is used to count the number of elements in the union of two sets.

## The Pigeonhole Principle
The pigeonhole principle is also called the **Dirichlet drawer principle**, after the nineteenth century German mathematician G. Lejeune Dirichlet, who often used this principle in his work.

* **Theorem** : Pigeonhole Principle
  If $k$ is a positive integer and $k + 1$ or more objects are placed into $k$ boxes, then there is at least one box containing two or more of the objects.
* **Corollary** :
  A function $f$ from a set with $k + 1$ or more elements to a set with $k$ elements is not 
  one-to-one.
#### The Generalized Pigeonhole Principle
* **Theorem** : The Generalized Pigeonhole Principle
  If $N$ objects are placed into $k$ boxes, then there is at least one box containing at least $\lceil N /k \rceil$ objects.
## Permutations and Combinations
Many counting problems can be solved by finding the number of ways to arrange a specified number of distinct elements of a set of a particular size, where the order of these elements matters.
#### Permutations
A **permutation** of a set of distinct objects is an ordered arrangement of these objects. An ordered arrangement of $r$ elements of a set is called an $r$-**permutation**.
The number of $r$-permutations of a set with $n$ elements is denoted by $P(n, r)$. We can find $P(n, r)$ using the product rule.

* **Theorem** :
  If $n$ is a positive integer and $r$ is an integer with $1 \leq r \leq n$, then there are $P(n, r) = n(n - 1)(n - 2) \ldots (n - r + 1)$ $r$-permutations of a set with $n$ distinct elements.
* **Corollary** :
  If $n$ and $r$ are integers with $0 \leq r \leq n$, then $P(n, r) = \huge{\frac{n!}{(n - r)!}}$.
#### Combinations
An $r$-**combination** of elements of a set is an unordered selection of $r$ elements from the set. Thus, an $r$-combination is simply a subset of the set with $r$ elements.
The number of $r$-combinations of a set with $n$ distinct elements is denoted by $C(n, r)$. Note that $C(n, r)$ is also denoted by $\huge{( ^n_r)}$ and is called a **binomial coefficient**.
* **Theorem** :
  The number of $r$-combinations of a set with $n$ elements, where $n$ is a nonnegative integer and $r$ is an integer with $0 \leq r \leq n$, equals $$\begin{align*}
  & C(n, r) = {\frac{n!}{r! (n - r)!}}. &
  \end{align*}$$

 * **Corollary** :
   Let $n$ and $r$ be nonnegative integers with $r \leq n$. Then $C(n, r) = C(n, n - r)$.

* **Definition** :
  A **combinatorial proof** of an identity is a proof that uses counting arguments to prove that both sides of the identity count the same objects but in different ways or a proof that is based on showing that there is a bijection between the sets of objects counted by the two sides of the identity. These two types of proofs are called **double counting proofs** and **bijective proofs**, respectively.
## Binomial Coefficients and Identities
As we remarked previously, the number of $r$-combinations from a set with $n$ elements is often denoted by $\big (^n_r)$. This number is also called a **binomial coefficient** because these numbers occur as coefficients in the expansion of powers of binomial expressions such as $(a + b)^n$.
#### The Binomial Theorem
The binomial theorem gives the coefficients of the expansion of powers of binomial expressions. A binomial expression is simply the sum of two terms, such as $x + y$.
* **Theorem** : The Binomial Theorem
  Let $x$ and $y$ be variables, and let $n$ be a nonnegative integer. Then $$\begin{align*}
  & (x + y)^n = \sum_{j=0}^{n} \big (^n_j) x^{n-j} y^j = \big (^n_0) x^{n} + \big (^n_1) x^{n-1} y + \ldots + \big (^n_{n-1}) x y^{n-1} + \big (^n_n) y^n. &
  \end{align*}$$
  
* **Corollary** :
  Let $n$ be a nonnegative integer. Then $$\begin{align*}
  & \sum_{k = 0}^{n} \big (^n_k) = 2^n. &
  \end{align*}$$
  
* **Corollary** :
  Let $n$ be a positive integer. Then $$\begin{align*}
  & \sum_{k = 0}^{n} (-1)^k \big (^n_k) = 0. &
  \end{align*}$$
  
* **Corollary** :
  Let $n$ be a nonnegative integer. Then $$\begin{align*}
  & \sum_{k = 0}^{n} (2^k) \big (^n_k) = 3^n. &
  \end{align*}$$
#### Identities Involving Binomial Coefficients

* **Theorem** : Pascal's Identity
  Let $n$ and $k$ be positive integers with $n \geq k$. Then $$\begin{align*}
  & \big (^{n + 1}_k) = \big (^n_{k - 1}) + \big (^n_k) . &
  \end{align*}$$
* **Theorem** : Vandermonde's Identity
  Let $m, n,$ and $r$ be nonnegative integers with $r$ not exceeding either $m$ or $n$. Then $$\begin{align*}
  & \big (^{m + n}_r) = \sum_{k = 0}^{r} \big (^m_{r - k}) + \big (^n_k) . &
  \end{align*}$$
* **Corollary** :
  Let $n$ be a nonnegative integer. Then $$\begin{align*}
  & \big (^{2n}_n) = \sum_{k = 0}^{n} \big (^n_k)^2 . &
  \end{align*}$$
* **Theorem** :
  Let $n$ and $r$ be a nonnegative integers with $r \leq n$. Then $$\begin{align*}
  & \big (^{n + 1}_{r + 1}) = \sum_{j = r}^{n} \big (^j_r). &
  \end{align*}$$
## Generating Permutations and Combinations

Any set with $n$ elements can be placed in one-to-one correspondence with the set $\{1, 2, 3, \ldots, n\}$. We can list the permutations of any set of n elements by generating the permutations of the $n$ smallest positive integers and then replacing these integers with the corresponding elements.
* **Algorithm** : Generating the Next Permutation in Lexicographic Order.
  **procedure** $next \space permutation$($a_1 a_2 \ldots a_n$: permutation of {$1, 2, \ldots, n$} not equal to 
  $\qquad \qquad \quad$$n \space n - 1 \space \ldots \space 2 \space 1$)
  $j := n - 1$
  while $a_j > a_{j + 1}$
  $\qquad$$j := j - 1$
  {$j$ is the largest subscript with $a_j < a_{j + 1}$}
  $k := n$
  while $a_j > a_k$
  $\qquad$$k := k - 1$
  {$a_k$ is the smallest integer greater than $a_j$ to the right of $a_j$}
  interchange $a_j$ and $a_k$
  $r := n$
  $s := j + 1$
  while $r > s$
  $\qquad$interchange $a_r$ and $a_s$
  $\qquad$$r := r - 1$
  $\qquad$$s := s + 1$
  {this puts the tail end of the permutation after the $j$th position in increasing order}
  {$a_1 a_2 \ldots a_n$ is now the next permutation}

* **Algorithm** : Generating the Next $r$-Combination in Lexicographic Order.
  **procedure** $next \space r\text{-}combination$($\{a_1, a_2, \ldots, a_r\}$: proper subset of $\{1, 2, \ldots, n\}$ not equal to 
  $\qquad \qquad \quad$$\{n - r + 1, \ldots, n\}$ with $a_1 < a_2 < \ldots < a_r$)
  $i := r$
  while $a_i = n - r + i$
  $\qquad$$i := i - 1$
  $a_i := a_i + 1$
  for $j := i + 1$ to $r$
  $\qquad$$a_j := a_i + j - i$
  {$\{a_1, a_2, \ldots, a_r\}$ is now the next combination}

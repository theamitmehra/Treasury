# Advanced Counting Techniques

In this chapter, we will see that many counting problems can be solved using formal power series, called generating functions, where the coefficients of powers of $x$ represent terms of the sequence we are interested in. Besides solving counting problems, we will also be able to use generating functions to solve recurrence relations and to prove combinatorial identities.

## Applications of Recurrence Relations

We can use recurrence relations to model a wide variety of problems, such as finding compound interest, counting rabbits on an island, determining the number of moves in the Tower of Hanoi puzzle, and counting bit strings with certain properties.

**Rabbits and the Fibonacci Numbers**:
Consider this problem, which was originally posed by Leonardo Pisano, also known as Fibonacci, in the thirteenth century. A young pair of rabbits (one of each sex) is placed on an island. A pair of rabbits does not breed until they are 2 months old. After they are 2 months old, each pair of rabbits produces another pair each month. Find a recurrence relation for the number of pairs of rabbits on the island after $n$ months, assuming that no rabbits ever die.

**Solution**:
Denote by $f_n$ the number of pairs of rabbits after $n$ months. We claim that $f_n, n = 1, 2, 3, \ldots,$ are the terms of the *Fibonacci sequence*.

The rabbit population can be modeled using a recurrence relation. At the end of the first month, the number of pairs of rabbits on the island is $f_1 = 1$. Because this pair does not breed during the second month, $f_2 = 1$ also. To find the number of pairs after $n$ months, add
the number on the island the previous month, $f_{n - 1}$, and the number of newborn pairs, which equals $f_{n-2}$, because each newborn pair comes from a pair at least $2$ months old.

Consequently, the sequence $\{f_n\}$ satisfies the recurrence relation $f_n = f_{n-1} + f_{n-2}$ for $n \geqslant 3$ together with the initial conditions $f_1 = 1$ and $f_2 = 1$. Because this recurrence relation and the initial conditions uniquely determine this sequence, the number of pairs of rabbits on
the island after $n$ months is given by the $n$th Fibonacci number.

**Parenthesis Problem**:
Find a recurrence relation for $C_n,$ the number of ways to parenthesize the product of $n + 1$ numbers, $x_0 \cdot x_1 \cdot x_2 \cdot \ldots \cdot x_n,$ to specify the order of multiplication.

**Solution**:
To develop a recurrence relation for $C_n$, we note that however we insert parentheses in the product $x_0 \cdot x_1 \cdot x_2 \cdot \ldots \cdot x_n,$, one "$\cdot$" operator remains outside all parentheses, namely, the operator for the final multiplication to be performed. This final operator appears between two of the $n + 1$ numbers, say, $x_k$ and $x_{k + 1}$. 
There are $C_k C_{n-k-1}$ ways to insert parentheses to determine the order of the $n + 1$ numbers to be multiplied when the final operator appears between $x_k$ and $xk+1,$ because there are $C_k$ ways to insert parentheses in the product $x_0 \cdot x_1 \cdot x_2 \cdot \ldots \cdot x_k,$ to determine the order in which these $k + 1$ numbers are to be multiplied and $C_{n-k-1}$ ways to insert parentheses in the product $x_{k+1} \cdot x_{k+2} \cdot \ldots \cdot x_n$ to determine the order in which these $n - k$ numbers are to be multiplied. Because this final operator can appear between any two of the $n + 1$ numbers, it follows that $$\begin{align*}
& C_n = C_0 C_{n - 1} + C_1 C_{n - 2} + \ldots + C_{n - 2} C_1 + C_{n - 1} C_0 & \\
& \quad \space= \sum^{n - 1}_{k = 0} C_k C_{n - k -1}.&
\end{align*}$$Note that the initial conditions are $C_0 = 1$ and $C_1 = 1$. The sequence $\{C_n\}$ is the sequence of **Catalan numbers**, named after Eugène Charles Catalan.

#### Algorithms and Recurrence Relations

We conclude this section by introducing another algorithmic paradigm known as **dynamic programming**, which can be used to solve many optimization problems efficiently.

An algorithm follows the dynamic programming paradigm when it recursively breaks down a problem into simpler overlapping subproblems, and computes the solution using the solutions of the subproblems.  Generally, recurrence relations are used to find the overall solution from the solutions of the subproblems. In this section we will illustrate the use of dynamic programming by constructing an algorithm for solving a scheduling problem.

We formalize this problem by supposing that we have $n$ talks, where talk $j$ begins at time $t_j,$ ends at time $e_j$, and will be attended by $w_j$ students. We want a schedule that maximizes the total number of student attendees.  That is, we wish to schedule a subset of talks to maximize the sum of $w_j$ over all scheduled talks. (Note that when a student attends more than one talk, this student is counted according to the number of talks attended.)
We denote by $T(j)$ the maximum number of total attendees for an optimal schedule from the first $j$ talks, so $T(n)$ is the maximal number of total attendees for an optimal schedule for all $n$ talks.

We first sort the talks in order of increasing end time. After doing this, we renumber the talks so that $e_1 \leqslant e_2 \leqslant ⋯ \leqslant e_n$. We say that two talks are **compatible** if they can be part of the same schedule, that is, if the times they are scheduled do not overlap (other than the possibility one ends and the other starts at the same time). We define $p(j)$ to be largest integer $i, i < j,$ for which $e_i \leqslant t_j$, if such an integer exists, and $p(j) = 0$ otherwise. 
That is, talk $p(j)$ is the talk ending latest among talks compatible with talk $j$ that end before talk $j$ ends, if such a talk exists, and $p(j) = 0$ if there are no such talks.

To develop a dynamic programming algorithm for this problem, we first develop a key recurrence relation. To do this, first note that if $j \leqslant n,$ there are two possibilities for an optimal schedule of the first $j$ talks (recall that we are assuming that the $n$ talks are ordered by increasing end time): (a) talk $j$ belongs to the optimal schedule or (b) it does not.

**Case $(a)$**:
We know that talks $p(j) + 1, \ldots, j - 1$ do not belong to this schedule, for none of these other talks are compatible with talk $j$. Furthermore, the other talks in this optimal schedule must comprise an optimal schedule for talks $1, 2, \ldots, p(j)$. For if there were a better schedule for talks $1, 2, \ldots, p(j),$ by adding talk $j,$ we will have a schedule better than the overall optimal schedule. Consequently, in case $(a),$ we have $T(j) = w_j + T(p(j))$.

**Case $(b)$**:
When talk $j$ does not belong to an optimal schedule, it follows that an optimal schedule from talks $1, 2, \ldots, j$ is the same as an optimal schedule from talks $1, 2, \ldots, j - 1$. Consequently, in case $(b),$ we have $T(j) = T(j - 1)$.

Combining cases $(a)$ and $(b)$ leads us to the recurrence relation $$\begin{align*}
& T(j) = \max(w_j + T(p(j)), T(j - 1)). & (I)
\end{align*}$$
Now we can construct an efficient algorithm for computing the maximum total number of attendees. We ensure that the algorithm is efficient by storing the value of each $T(j)$ after we compute it. This allows us to compute $T(j)$ only once. If we did not do this, the algorithm would have exponential worst-case complexity. The process of storing the values as each is computed is known as **memoization** and is an important technique for making recursive algorithms efficient.

* **Algorithm**: Dynamic Programming Algorithm for Scheduling Talks
  **procedure** $Maximum \space Attendees$ $(s_1 , s_2, \ldots, s_n$: start times of talks;
  $\qquad$$e_1, e_2, \ldots, e_n$: end times of talks; $w_1, w_2, \ldots, w_n$: number of attendees to talks)
  $\qquad$sort talks by end time and relabel so that $e_1 \leqslant e_2 \leqslant \ldots \leqslant e_n$
  
  for $j := 1$ to $n$
  $\qquad$if no job $i$ with $i < j$ is compatible with job $j$
  $\qquad \qquad$$p(j) = 0$
  $\qquad$else $p(j) := \max \{i \mid i < j$ and job $i$ is compatible with job $j\}$
  $\qquad$$T(0) := 0$
  for $j := 1$ to $n$
  $\qquad$$T(j) := \max(w_j + T(p(j)), T(j - 1))$
  return $T(n)\space \{T(n)$ is the maximum number of attendees$\}$

## Solving Linear Recurrence Relations

One important class of recurrence relations can be explicitly solved in a systematic way. These are recurrence relations that express the terms of a sequence as linear combinations of previous terms.

* **Definition**:
  A **linear homogeneous recurrence relation** of degree $k$ with **constant coefficients** is a recurrence relation of the form $$\begin{align*}
  & a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k}, &
  \end{align*}$$where $c_1, c_2, \ldots, c_k$ are real numbers, and $c_k \ne 0$.

A consequence of the second principle of mathematical induction is that a sequence satisfying the recurrence relation in the definition above is uniquely determined by this recurrence relation and the $k$ initial conditions $a_0 = C_0, a_1 = C_1, \ldots, a_{k-1} = C_{k-1}$.

#### Solving Linear Homogeneous RR with Constant Coefficients

We can use two key ideas to find all solutions of linear homogeneous recurrence relations. First, these recurrence relations have solutions of the form $a_n = r^n,$ where $r$ is a constant.

We claim $a_n = r^n$ is a solution of the recurrence relation $a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k}$ if and only if $$\begin{align*}
& r^n = c_1 r^{n-1} + c_2 r^{n-2} + \ldots + c_k r^{n-k}. &
\end{align*}$$When both sides of this equation are divided by $r^{n-k}$ (when $r \ne 0$) and the right-hand side is subtracted from the left, we obtain the equation $$\begin{align*}
& r^k - c_1 r^{k-1} - c_2 r^{k-2} - \ldots - c_{k - 1} r - c_k =0. &
\end{align*}$$
Consequently, the sequence $\{a_n\}$ with $a_n = r^n$ where $r \ne 0$ is a solution if and only if $r$ is a solution of this last equation. We call this the **characteristic equation** of the recurrence relation. The solutions of this equation are called the **characteristic roots** of the recurrence relation.

The other key observation is that a linear combination of two solutions of a linear homogeneous recurrence relation is also a solution. To see this, suppose that $s_n$ and $t_n$ are both solutions of $a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k}$. Then $$\begin{align*}
& s_n = c_1 s_{n-1} + c_2 s_{n-2} + \ldots + c_k s_{n-k}. &
\end{align*}$$and $$\begin{align*}
& t_n = c_1 t_{n-1} + c_2 t_{n-2} + \ldots + c_k t_{n-k}. &
\end{align*}$$Now suppose that $b_1$ and $b_2$ are real numbers. Then $$\begin{align*}
& b_1 s_n + b_2 t_n = b_1 (c_1 s_{n-1} + c_2 s_{n-2} + \ldots + c_k s_{n-k}) + b_2 (c_1 t_{n-1} + c_2 t_{n-2} + \ldots + c_k t_{n-k}). & \\
& \qquad \qquad \quad = c_1 (b_1 s_{n - 1} + b_2 t_{n - 1}) + c_2 (b_1 s_{n - 2} + b_2 t_{n - 2}) + \ldots + c_k (b_1 s_{n - k} + b_2 t_{n - k}).&
\end{align*}$$This means that $b_1 s_n + b_2 t_n$ is also a solution of the same linear homogeneous recurrence relation.

We will now state the general result about the solution of linear homogeneous recurrence relations with constant coefficients, where the degree may be greater than two, under the assumption that the characteristic equation has distinct roots.

* **Theorem**: **The General Case**
  Let $c_1, c_2, \ldots, c_k$ be real numbers. Suppose that the characteristic equation $$\begin{align*}
  & r^k - c_1 r^{k-1} - c_2 r^{k-2} - \ldots - c_{k - 1} r - c_k =0. &
  \end{align*}$$has $k$ distinct roots $r_1, r_2, \ldots, r_k$. Then a sequence $\{a_n\}$ is a solution of the recurrence relation $$\begin{align*}
  & a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k} &
  \end{align*}$$if and only if $$\begin{align*}
  & a_n = \alpha_1 r^n_1 + \alpha_2 r^n_2 + \ldots + \alpha_k r^n_k &
  \end{align*}$$for $n = 0, 1, 2, \ldots,$ where $\alpha_1, \alpha_2, \ldots, \alpha_k$ are constants.

We now state the most general result about linear homogeneous recurrence relations with constant coefficients, allowing the characteristic equation to have multiple roots.

The key point is that for each root $r$ of the characteristic equation, the general solution has a summand of the form $P(n)r^n,$ where $P(n)$ is a polynomial of degree $m - 1,$ with $m$ the multiplicity of this root.

* **Theorem**: **The General Case**
  Let $c_1, c_2, \ldots, c_k$ be real numbers. Suppose that the characteristic equation $$\begin{align*}
  & r^k - c_1 r^{k-1} - c_2 r^{k-2} - \ldots - c_{k - 1} r - c_k =0. &
  \end{align*}$$has $t$ distinct roots $r_1, r_2, \ldots, r_t$ with multiplicities $m_1, m_2, \ldots, m_t,$ respectively, so that $1 \leqslant m_i$ for $i = 1, 2, \ldots, t$ and $m_1 + m_2 + \ldots + m_t = k$. Then a sequence $\{a_n\}$ is a solution of the recurrence relation $$\begin{align*}
  & a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k} &
  \end{align*}$$if and only if $$\begin{align*}
  & a_n = (\alpha_{1, 0} + \alpha_{1,1} n + \ldots + \alpha_{1, m_1 - 1} n^{m_1 - 1})r^n_1 + ... + (\alpha_{t, 0} + \alpha_{t, 1} n + \ldots + \alpha_{t, m_t - 1} n^{m_t - 1})r^n_t &
  \end{align*}$$for $n = 0, 1, 2, \ldots,$ where $\alpha_{i, j}$ are constants for $1 \leqslant i \leqslant t$ and $0 \leqslant j \leqslant m_i - 1$.

#### Linear Nonhomogeneous RR with Constant Coefficients

Let's look at an example of **linear nonhomogeneous recurrence relation with constant coefficients**. For example, $a_n = 3a_{n-1} + 2n$ is an example of a linear nonhomogeneous recurrence relation with constant coefficients, that is, a recurrence relation of the form $$\begin{align*}
& a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k} + F(n) &
\end{align*}$$where $c_1, c_2, \ldots, c_k$ are real numbers and $F(n)$ is a function not identically zero depending only on $n$. The recurrence relation $$\begin{align*}
& a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k} &
\end{align*}$$is called the **associated homogeneous recurrence relation**. It plays an important role in the solution of the nonhomogeneous recurrence relation.

* **Theorem**:
  If $\{a^{(p)}_n\}$ is a particular solution of the nonhomogeneous linear recurrence relation with constant coefficients $$\begin{align*}
  & a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k} + F(n), &
  \end{align*}$$then every solution is of the form $\{a^{(p)}_n\} + \{a^{(h)}_n\}$, where $\{a^{(h)}_n\}$ is a solution of the associated homogeneous recurrence relation $$\begin{align*}
  & a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k}. &
  \end{align*}$$
We see that the key to solving nonhomogeneous recurrence relations with constant coefficients is finding a particular solution. Then every solution is a sum of this solution and a solution of the associated homogeneous recurrence relation. Although there is no general method for finding such a solution that works for every function $F(n),$ there are techniques that work for certain types of functions $F(n),$ such as polynomials and powers of constants.

* **Theorem**:
  Suppose that $\{a_n\}$ satisfies the linear nonhomogeneous recurrence relation $$\begin{align*}
  & a_n = c_1 a_{n-1} + c_2 a_{n-2} + \ldots + c_k a_{n-k} + F(n), &
  \end{align*}$$where $c_1, c_2, \ldots, c_k$ are real numbers, and $$\begin{align*}
  & F(n) = (b_tn^t + b_{t-1}n^{t-1} + \ldots + b_1 n + b_0)s^n, &
  \end{align*}$$where $b_0, b_1, \ldots, b_t$ and $s$ are real numbers. When $s$ is not a root of the characteristic equation of the associated linear homogeneous recurrence relation, there is a particular solution of the form $$\begin{align*}
  & (p_tn^t + p_{t-1}n^{t-1} + \ldots + p_1 n + p_0)s^n. &
  \end{align*}$$When $s$ is a root of this characteristic equation and its multiplicity is $m,$ there is a particular solution of the form $$\begin{align*}
  & n^m (p_tn^t + p_{t-1}n^{t-1} + \ldots + p_1 n + p_0)s^n. &
  \end{align*}$$
## Generating Functions

Generating functions are used to represent sequences efficiently by coding the terms of a sequence as coefficients of powers of a variable $x$ in a formal power series. Generating functions can be used to solve many types of counting problems, such as the number of ways to select or distribute objects of different kinds, subject to a variety of constraints, and the number of ways to make change for a rupee using coins of different denominations. 

Generating functions can be used to solve recurrence relations by translating a recurrence relation for the terms of a sequence into an equation involving a generating function. This equation can then be solved to find a closed form for the generating function. From this closed form, the coefficients of the power series for the generating function can be found, solving the original recurrence relation.

Generating functions can also be used to prove combinatorial identities by taking advantage of relatively simple relationships between functions that can be translated into identities involving the terms of sequences.

* **Theorem**:
  The **generating function** for the sequence $a_0, a_1, \ldots, a_k, \ldots$ of real numbers is the infinite series $$\begin{align*} 
  & G(x) = a_0 + a_1 x + \ldots + a_k x_k + \ldots = \sum^{\infty}_{k = 0}a_k x^k .&
  \end{align*}$$

When generating functions are used to solve counting problems, they are usually considered to be **formal power series**. We will now state some widely important facts about infinite series used when working with generating functions.

* **Theorem**:
  Let $f(x) = \sum^{\infty}_{k = 0}a_k x^k$ and $g(x) = \sum^{\infty}_{k = 0}b_k x^k$. Then $$\begin{align*}
  & f(x) + g(x) = \sum^{\infty}_{k = 0}(a_k + b_k) x^k \quad \text{and} \quad f(x)g(x) = \sum^{\infty}_{k = 0} \left( \sum^{k}_{j = 0} a_j b_{k - j} \right) x^k.&
  \end{align*}$$

Theorem above is valid only for power series that converge in an interval. However, the theory of generating functions is not limited to such series. In the case of series that do not converge, the statements in Theorem above can be taken as definitions of addition and multiplication of generating functions.

To use generating functions to solve many important problems, we will need to apply the binomial theorem for exponents that are not positive integers. Before we state an extended version of the binomial theorem, we need to define extended binomial coefficients.

* **Definition**:
  Let $u$ be a real number and $k$ a nonnegative integer. Then the **extended binomial coefficient** is defined by $$\begin{align*} 
  & \binom{u}{k} = \begin{cases} u(u - 1) \ldots (u - k + 1) / k! \quad \text {if} \space k > 0. \\ 1  \qquad \qquad \qquad \qquad \qquad \quad \space \space \space \text {if} \space k = 0. \end{cases} &
  \end{align*}$$
  
* **Theorem**:
  Let $x$ be a real number with $|x| < 1$ and let $u$ be a real number. Then $$\begin{align*}
  & (1 + x)^n = \sum^{\infty}_{k = 0} \binom{u}{k} x^k.&
  \end{align*}$$

Here is the table for useful generating functions:

| $G(x)$                                                                                                                                             | $a_k$                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| $\displaystyle (1 + x)^n = \sum_{k=0}^{n} \binom{n}{k} x^k = 1 + \binom{n}{1}x + \binom{n}{2}x^2 + \cdots + x^n$                                   | $\displaystyle \binom{n}{k}$                                             |
| $\displaystyle (1 + ax)^n = \sum_{k=0}^{n} \binom{n}{k} a^k x^k = 1 + \binom{n}{1} ax + \binom{n}{2} a^2 x^2 + \cdots + a^n x^n$                   | $\displaystyle \binom{n}{k} a^k$                                         |
| $\displaystyle (1 + x^r)^n = \sum_{k=0}^{n} \binom{n}{k} x^{rk} = 1 + \binom{n}{1} x^r + \binom{n}{2} x^{2r} + \cdots + x^{nr}$                    | $\displaystyle \binom{n}{k/r} \text{ if } r \mid k; 0 \text{ otherwise}$ |
| $\displaystyle \frac{1 - x^{n+1}}{1 - x} = \sum_{k=0}^{n} x^k = 1 + x + x^2 + \cdots + x^n$                                                        | $\displaystyle 1 \text{ if } k \leq n; 0 \text{ otherwise}$              |
| $\displaystyle \frac{1}{1 - x} = \sum_{k=0}^{\infty} x^k = 1 + x + x^2 + \cdots$                                                                   | $\displaystyle 1$                                                        |
| $\displaystyle \frac{1}{1 - ax} = \sum_{k=0}^{\infty} a^k x^k = 1 + ax + a^2 x^2 + \cdots$                                                         | $\displaystyle a^k$                                                      |
| $\displaystyle \frac{1}{1 - x^r} = \sum_{k=0}^{\infty} x^{rk} = 1 + x^r + x^{2r} + \cdots$                                                         | $\displaystyle 1 \text{ if } r \mid k; 0 \text{ otherwise}$              |
| $\displaystyle \frac{1}{(1 - x)^2} = \sum_{k=0}^{\infty} (k+1) x^k = 1 + 2x + 3x^2 + \cdots$                                                       | $\displaystyle k + 1$                                                    |
| $\displaystyle e^x = \sum_{k=0}^{\infty} \frac{x^k}{k!} = 1 + \frac{x}{1!} + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots$                             | $\displaystyle \frac{1}{k!}$                                             |
| $\displaystyle \ln(1 + x) = \sum_{k=1}^{\infty} (-1)^{k+1} \frac{x^k}{k} = x - \frac{x^2}{2} + \frac{x^3}{3} - \frac{x^4}{4} + \cdots$             | $\displaystyle (-1)^{k+1}/k$                                             |

## Inclusion-Exclusion

*How many elements are in the union of two finite sets?*
Previously we showed that the number of elements in the union of the two sets $A$ and $B$ is the sum of the numbers of elements in the sets minus the number of elements in their intersection. That is, $$\begin{align*}
& |A \cup B| = |A| + |B| - |A \cap B|. &
\end{align*}$$
* **Theorem**: **The Principle of Inclusion-Exclusion**
  Let $A_1, A_2, \ldots, A_n$ be finite sets. Then $$\begin{align*}
  & |A_1 \cup A_2 \cup \ldots \cup A_n| = \sum_{1 \leqslant i \leqslant n} |A_i| - \sum_{1 \leqslant i < j\leqslant n} |A_i \cap A_j| + \sum_{1 \leqslant i < j < k \leqslant n} |A_i \cap A_j \cap A_k| - \ldots + (-1)^{n+1} |A_1 \cap A_2 \cap \ldots \cap A_n|. &
  \end{align*}$$

#### Applications of Inclusion–Exclusion

Many counting problems can be solved using the principle of inclusion–exclusion. For instance, we can use this principle to find the number of primes less than a positive integer.

**An Alternative Form**:
There is an alternative form of the principle of inclusion–exclusion that is useful in counting problems. In particular, this form can be used to solve problems that ask for the number of elements in a set that have none of $n$ properties $P_1, P_2, \ldots, P_n$.

Let $A_i$ be the subset containing the elements that have property $P_i$. The number of elements with all the properties $P_{i_1}, P_{i_2}, \ldots, P_{i_k}$ will be denoted by $N(P_{i_1} P_{i_2} \ldots P_{i_k}$). Writing these quantities in terms of sets, we have $$\begin{align*}
& |A_{i_1} \cap A_{i_2} \cap \ldots \cap A_{i_n}| = N(P_{i_1} P_{i_2} \ldots P_{i_k}). &
\end{align*}$$If the number of elements with none of the properties $P_1, P_2, \ldots, P_n$ is denoted by following, $N(P'_1 P'_2 \ldots P'_n)$ and the number of elements in the set is denoted by $N,$ it follows that $$\begin{align*}
& N(P'_1 P'_2 \ldots P'_n) = N - |A_1 \cup A_2 \cup \ldots \cup A_n|. &
\end{align*}$$From the inclusion–exclusion principle, we see that $$\begin{align*}
  & N(P'_1 P'_2 \ldots P'_n) = N - \sum_{1 \leqslant i \leqslant n} N(P_i) + \sum_{1 \leqslant i < j\leqslant n} N(P_i P_j) - \sum_{1 \leqslant i < j < k \leqslant n} N(P_i P_j P_k) + \ldots + (-1)^{n+1} N(P_1 P_2 \ldots P_k). &
  \end{align*}$$
The next general result that tells us how many onto functions there are from a set with $m$ elements to one with $n$ elements.

* **Theorem**:
  Let $m$ and $n$ be positive integers with $m \geqslant n$. Then, there are $$\begin{align*}
  & n^m - C(n, 1)(n - 1)^m + C(n, 2)(n - 2)^m - \ldots + (-1)^{n - 1} C(n, n - 1) \cdot 1^m &
  \end{align*}$$onto functions from a set with $m$ elements to a set with $n$ elements.

An onto function from a set with $m$ elements to a set with $n$ elements corresponds to a way to distribute the $m$ elements in the domain to $n$ indistinguishable boxes so that no box is empty, and then to associate each of the $n$ elements of the codomain to a box. This means that the number of onto functions from a set with $m$ elements to a set with $n$ elements is the number of ways to distribute $m$ distinguishable objects to $n$ indistinguishable boxes so that no box is empty multiplied by the number of permutations of a set with $n$ elements. 

Consequently, the number of onto functions from a set with $m$ elements to a set with $n$ elements equals $n! \, S(m, n),$ where $S(m, n)$ is a **Stirling number of the second kind**.

A **derangement** is a permutation of objects that leaves no object in its original position. To solve the problem of similar kind we will need to determine the number of derangements of a set of $n$ objects.

* **Theorem**:
  The number of derangements of a set with $n$ elements is $$\begin{align*}
  & D_n = n! \left[ 1 - \frac{1}{1!} + \frac{1}{2!} - \frac{1}{3!} + \ldots + (-1)^n \frac{1}{n!} \right]. &
  \end{align*}$$

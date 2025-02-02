# Dynamic Programming

Dynamic programming, like the divide-and-conquer method, solves problems by combining the solutions to subproblems. ("Programming" in this context refers to a tabular method, not to writing computer code.)

As we saw, divide-and-conquer algorithms partition the problem into disjoint subproblems, solve the subproblems recursively, and then combine their solutions to solve the original problem. In contrast, dynamic programming applies when the subproblems overlap$-$that is, when subproblems share subproblems. In this context, a divide-and-conquer algorithm does more work than necessary, repeatedly solving the common subproblems.
A dynamic-programming algorithm solves each subproblem just once and then saves its answer in a table, thereby avoiding the work of recomputing the answer every time it solves each subproblem.

Dynamic programming typically applies to **optimization problems**. Such problems can have many possible solutions. Each solution has a value, and you want to find a solution with the optimal (minimum or maximum) value. We call such a solution an optimal solution to the problem, as opposed to the optimal solution, since there may be several solutions that achieve the optimal value.

To develop a dynamic-programming algorithm, follow a sequence of four steps:

* $(1):$ Characterize the structure of an optimal solution.
* $(2):$ Recursively define the value of an optimal solution.
* $(3):$ Compute the value of an optimal solution, typically in a bottom-up fashion.
* $(4):$ Construct an optimal solution from compute= information.

Steps $1$-$3$ form the basis of a dynamic-programming solution to a problem. If you need only the value of an optimal solution, and not the solution itself, then you can omit step $4$. When you do perform step $4,$ it often pays to maintain additional information during step $3$ so that you can easily construct an optimal solution.

## Rod Cutting


Our first example uses dynamic programming to solve a simple problem in deciding where to cut steel rods. Serling Enterprises buys long steel rods and cuts them into shorter rods, which it then sells. Each cut is free. The management of Serling Enterprises wants to know the best way to cut up the rods.

Serling Enterprises has a table giving, for $i = 1, 2, \ldots, n,$ the price $p_i$ in dollars that they charge for a rod of length $i$ inches. The length of each rod in inches is always an integer. 

The **rod-cutting problem** is the following. Given a rod of length $n$ inches and a table of prices $p_i$ for $i = 1, 2, \ldots, n,$ determine the maximum revenue $r_n$ obtainable by cutting up the rod and selling the pieces. If the price $p_n$ for a rod of length $n$ is large enough, an optimal solution might require no cutting at all.

Serling Enterprises can cut up a rod of length $n$ in $2^{n-1}$ different ways, since they have an independent option of cutting, or not cutting, at distance $i$ inches from the left end, for $i = 1, 2, \ldots, n - 1$. We denote a decomposition into pieces using ordinary additive notation, so that $7 = 2 + 2 + 3$ indicates that a rod of length $7$ is cut into three pieces$-$two of length $2$ and one of length $3$. If an optimal solution cuts the rod into $k$ pieces, for some $1 \leqslant k \leqslant n,$ then an optimal decomposition $$\begin{align*}
& n = i_1 + i_2 + \ldots + i_k 
\end{align*}$$of the rod into pieces of lengths $i_1, i_2, \ldots, i_k$ provides maximum corresponding revenue $$\begin{align*}
& r_n = p_{i_1} + p_{i_2} + \ldots + p_{i_k}. 
\end{align*}$$
More generally, we can express the values $r_n$ for $n - 1$ in terms of optimal revenues from shorter rods: $$\begin{align*}
& r_n = \max \{p_n, r_1 + r_{n - 1}, r_2 + r_{n - 2}, \ldots, r_{n - 1} + r_1\}. & (I)
\end{align*}$$
The first argument, $p_n,$ corresponds to making no cuts at all and selling the rod of length $n$ as is. The other $n - 1$ arguments to max correspond to the maximum revenue obtained by making an initial cut of the rod into two pieces of size $i$ and $n - i,$ for each $i = 1, 2, \ldots, n - 1,$ and then optimally cutting up those pieces further, obtaining revenues $r_i$ and $r_{n - i}$ from those two pieces. Since you don't know ahead of time which value of $i$ optimizes revenue, you have to consider all possible values for $i$ and pick the one that maximizes revenue. You also have the option of picking no $i$ at all if the greatest revenue comes from selling the rod uncut.

To solve the original problem of size $n,$ you solve smaller problems of the same type. Once you make the first cut, the two resulting pieces form independent instances of the rod-cutting problem. The overall optimal solution incorporates optimal solutions to the two resulting subproblems, maximizing revenue from each of those two pieces. We say that the rod-cutting problem exhibits **optimal substructure**: optimal solutions to a problem incorporate optimal solutions to related subproblems, which you may solve independently.

In a related, but slightly simpler, way to arrange a recursive structure for the rod-cutting problem, let's view a decomposition as consisting of a first piece of length $i$ cut off the left-hand end, and then a right-hand remainder of length $n - i$. Only the remainder, and not the first piece, may be further divided. Think of every decomposition of a length-$n$ ro= in this way: as a first piece followed by some decomposition of the remainder. Then we can express the solution with no cuts at all by saying that the first piece has size $i = n$ and revenue $p_n$ and that the remainder has size $0$ with corresponding revenue $r_0 = 0$. We thus obtain the following simpler version of equation $(I):$ $$\begin{align*}
& r_n = \max \{p_i + r_{n - i} : 1 \leqslant i \leqslant n\}. & (II)
\end{align*}$$In this formulation, an optimal solution embodies the solution to only one related subproblem rather than two (the remainder).

#### Recursive Top-down Implementation

The **Cut-Rod** procedure implements the computation implicit in equation $(II)$ in a straightforward, top-down, recursive manner.

Procedure takes as input an array $p[1 : n]$ of prices and an integer $n,$ an= it returns the maximum revenue possible for a rod of length $n$. For length $n = 0,$ no revenue is possible, and so **Cut-Rod** returns $0$. Procedure initializes the maximum revenue $q$ to $-\infty,$ so that the for loop correctly computes $q = \max \{p_i +$ **Cut-Rod**$(p, n - i) : 1 \leqslant i \leqslant n\}$. A simple induction on $n$ proves that this answer is equal to the desired answer $r_n,$ using equation $(II)$.

* **procedure** Cut-Rod$(p, n)$
  
  if $n == 0$  
  $\qquad$return $0$  
  $q = - \infty$  
  for $i = 1$ to $n$  
  $\qquad$$q = \max \{q, p[i] + \text{Cut-Rod}(p, n - i)\}$  
  return $q$  

> [!summary] Cut-Rod$\,(p,n)$
> if $n == 0$  
> $\qquad$return $0$  
> $q = - \infty$  
> for $i = 1$ to $n$  
> $\qquad$$q = \max \{q, p[i] + \text{Cut-Rod}(p, n - i)\}$  
> return $q$  

*Why is* **Cut-Rod** *so inefficient?* 
The problem is that **Cut-Rod** calls itself recursively over and over again with the same parameter values, which means that it solves the same subproblems repeatedly.

We can design a recursion tree demonstrating what happens for $n = 4$: **Cut-Rod** $(p, n)$ calls **Cut-Rod** $(p, n - i)$ for $i = 1, 2, \ldots, n$. Equivalently, **Cut-Rod** $(p, n)$ calls **Cut-Rod** $(p, j)$ for each
$j = 0, 1, \ldots, n - 1$. When this process unfolds recursively, the amount of work done, as a function of $n,$ grows explosively.

To analyze the running time of **Cut-Rod**, let $T(n)$ denote the total number of calls made to **Cut-Rod** $(p, n)$ for a particular value of $n$. This expression equals the number of nodes in a subtree whose root is labeled $n$ in the recursion tree. The count includes the initial call at its root. Thus, $T(0) = 1$ and $$\begin{align*}
& T(n) = 1 + \sum_{j = 0}^{n - 1} T(j). & (III)
\end{align*}$$The initial $1$ is for the call at the root, and the term $T(j)$ counts the number of calls (including recursive calls) due to the call **Cut-Rod**$(p, n - i),$ where $j = n - i$. We can show that $$\begin{align*}
& T(n) = 2^n, & (IV)
\end{align*}$$and so the running time of **Cut-Rod** is exponential in $n$.

In retrospect, this exponential running time is not so surprising. **Cut-Rod** explicitly considers all possible ways of cutting up a rod of length $n$.

A rod of length $n$ has $n - 1$ potential locations to cut. Each possible way to cut up the rod makes a cut at some subset of these $n - 1$ locations, including the empty set, which makes for no cuts. Viewing each cut location as a distinct member of a set of $n - 1$ elements, you can see that there are $2^{n - 1}$ subsets. Each leaf in the recursion tree corresponds to one possible way to cut up the rod. Hence, the recursion tree has $2^{n - 1}$ leaves. The labels on the simple path from the root to a leaf give the sizes of each remaining right-hand piece before making each cut. That is, the labels give the corresponding cut points, measured from the right-hand end of the rod.

#### Using Dynamic Programming for Optimal Rod Cutting

The dynamic-programming method works as follows. Instead of solving the same subproblems repeatedly, as in the naive recursion solution, arrange for each subproblem to be solved only once. There's actually an obvious way to do so: the first time you solve a subproblem, save its solution. If you need to refer to this subproblem's solution again later, just look it up, rather than recomputing it.

Saving subproblem solutions comes with a cost: the additional memory needed to store solutions. Dynamic programming thus serves as an example of a **time-memory trade-off**. The savings may be dramatic. For example, we're about to use dynamic programming to go from the exponential-time algorithm for rod cutting down to a $\Theta(n^2)$-time algorithm.
A dynamic-programming approach runs in polynomial time when the number of distinct subproblems involve= is polynomial in the input size and you can solve each such subproblem in polynomial time.

There are usually two equivalent ways to implement a dynamic-programming approach. Solutions to the rod-cutting problem illustrate both of them.

* The first approach is **top-down** with **memoization**. In this approach, you write the procedure recursively in a natural manner, but modified to save the result of each subproblem (usually in an array or hash table). The procedure now first checks to see whether it has previously solved this subproblem. If so, it returns the saved value, saving further computation at this level. If not, the procedure computes the value in the usual manner but also saves it.
  We say that the recursive procedure has been **memoized**: it "remembers" what results it has computed previously.

* The second approach is the **bottom-up** method. This approach typically depends on some natural notion of the "size" of a subproblem, such that solving any particular subproblem depends only on solving "smaller" subproblems. Solve the subproblems in size order, smallest first, storing the solution to each subproblem when it is first solved. In this way, when solving a particular subproblem, there are already saved solutions for all of the smaller subproblems its solution depends upon.
  You need to solve each subproblem only once, and when you first see it, you have already solved all of its prerequisite subproblems.

These two approaches yield algorithms with the same asymptotic running time, except in unusual circumstances where the top-down approach does not actually recurse to examine all possible subproblems. The bottom-up approach often has much better constant factors, since it has lower overhead for procedure calls.

The procedures **Memoized-Cut-Rod** and **Memoized-Cut-Rod-Aux** demonstrate how to memoize the top-down **Cut-Rod** procedure. The main procedure **Memoized-Cut-Rod** initializes a new auxiliary array $r[0 : n]$ with the value $-\infty$ which, since known revenue values are always nonnegative, is a convenient choice for denoting "unknown."
**Memoized-Cut-Rod** then calls its helper procedure, **Memoized-Cut-Rod-Aux**, which is just the memoized version of the exponential-time procedure, **Cut-Rod**. It first checks to see whether the desired value is already known and, if it is, then lines returns it. Otherwise, lines compute the desired value $q$ in the usual manner, saves it in $r[n],$ and returns it.

* **procedure** Memoized-Cut-Rod$(p, n)$
  
  let $r[0 : n]$ be a new array
  for $i = 0$ to $n$
  $\qquad$$r[i] = -\infty$
  return Memoized-Cut-Rod$(p, n, r)$

> [!summary] Memoized-Cut-Rod$(p,n)$
>   let $r[0 : n]$ be a new array
>   for $i = 0$ to $n$
>   $\qquad$$r[i] = -\infty$
>   return Memoized-Cut-Rod$(p, n, r)$

* **procedure** Memoized-Cut-Rod-Aux$(p, n, r)$
  
  if $r[n] \geqslant 0$
  $\qquad$return $r[n]$
  
  if $n == 0$
  $\qquad$$q = 0$
  else
  $\qquad$$q = -\infty$
  $\qquad$for $i = 1$ to $n$
  $\qquad \qquad$$q = \max \{q, p[i] + \text{Memoized-Cut-Rod-Aux}(p, n - i, r)\}$
  $r[n] = q$
  return $q$


> [!summary] Memoized-Cut-Rod-Aux $(p, n, r)$
>if $r[n] \geqslant 0$
> $\qquad$ return $r[n]$ 
> if $n == 0$
>$\qquad$$q = 0$
> else
> $\qquad$$q = -\infty$
> $\qquad$for $i = 1$ to $n$
> $\qquad \qquad$$q = \max \{q, p[i] + \text{Memoized-Cut-Rod-Aux}(p, n - i, r)\}$
> $r[n] = q$
> return $q$

The bottom-up version, **Bottom-Up-Cut-Rod**, is even simpler. Using the bottom-up dynamic-programming approach, **Bottom-Up-Cut-Rod** takes advantage of the natural ordering of the subproblems: a subproblem of size $i$ is "smaller" than a subproblem of size $j$ if $i < j$. Thus, the procedure solves subproblems of sizes $j = 0, 1, \ldots, n,$ in that order.

First line of **Bottom-Up-Cut-Rod** creates a new array $r[0 : n]$ in which to save the results of the subproblems, and then next line initializes $r[0]$ to $0,$ since a rod of length $0$ earns no revenue. Lines solve each subproblem of size $j,$ for $j = 0, 1, \ldots, n,$ in order of increasing size. The approach used to solve a problem of a particular size $j$ is the same as that used by **Cut-Rod**, except that procedure now directly references array entry $r[j - i]$ instead of making a recursive call to solve the subproblem of size $j - i$. Lines then saves in $r[j]$ the solution to the subproblem of size $j$. Finally, procedure returns $r[n],$ which equals the optimal value $r_n$.

* **procedure** Bottom-Up-Cut-Rod$(p, n)$
  
  let $r[0 : n]$ be a new array
  $r[0] = 0$
  
  for $j = 1$ to $n$
  $\qquad$$q = -\infty$
  $\qquad$for $i = 1$ to $j$
  $\qquad \qquad$$q = \max \{q, p[i] + r[j - i]\}$
  $\qquad$$r[j] = q$
  return $r[n]$


> [!summary] $\text{Bottom-Up-Cut-Rod}(p, n)$
>   let $r[0 : n]$ be a new array
  $r[0] = 0$
  **for** $j = 1$ **to** $n$
  $\qquad$$q = -\infty$
  $\qquad$**for** $i = 1$ **to** $j$
  $\qquad \qquad$$q = \max \{q, p[i] + r[j - i]\}$
  $\qquad$$r[j] = q$
  **return** $r[n]$

The bottom-up and top-down versions have the same asymptotic running time. The running time of **Bottom-Up-Cut-Rod** is $\Theta(n^2),$ due to its doubly nested loop structure. The number of iterations of its inner for loop forms an arithmetic series.
The running time of its top-down counterpart, **Memoized-Cut-Rod**, is also $\Theta(n^2),$ although this running time may be a little harder to see. Because a recursive call to solve a previously solved subproblem returns immediately, **Memoized-Cut-Rod** solves each subproblem just once. It solves subproblems for sizes $0, 1, \ldots, n$. To solve a subproblem of size $n,$ the for loop iterates $n$ times. Thus, the total number of iterations of this for loop, over all recursive calls of **Memoized-Cut-Rod**, forms an arithmetic series, giving a total of $\Theta(n^2)$ iterations, just like the inner for loop of **Bottom-Up-Cut-Rod**.

#### Subproblem Graphs

When you think about a dynamic-programming problem, you need to understand the set of subproblems involved and how subproblems depend on one another. The subproblem graph for the problem embodies exactly this information. The subproblem graph has a directed edge from the vertex for subproblem $x$ to the vertex for subproblem $y$ if determining an optimal solution for subproblem $x$ involves directly considering an optimal solution for subproblem $y$.
For example, the subproblem graph contains an edge from $x$ to $y$ if a top-down recursive procedure for solving $x$ directly calls itself to solve $y$. You can think of the subproblem graph as a "reduced" or "collapsed" version of the recursion tree for the top-down recursive method, with all nodes for the same subproblem coalesced into a single vertex and all edges directed from parent to child.

The bottom-up method for dynamic programming considers the vertices of the subproblem graph in such an order that you solve the subproblems $y$ adjacent to a given subproblem $x$ before you solve subproblem $x$. (The adjacency relation in a directed graph is not necessarily symmetric.) In a bottom-up dynamic-programming algorithm, you consider the vertices of the subproblem graph in an order that is a "reverse topological sort," or a "topological sort of the transpose" of the subproblem graph.
In other words, no subproblem is considered until all of the subproblems it depends upon have been solved. Similarly, you can view the top-down method (with memoization) for dynamic programming as a "depth-first search" of the subproblem graph.

The size of the subproblem graph $G = (V, E)$ can help you determine the running time of the dynamic-programming algorithm. Since you solve each subproblem just once, the running time is the sum of the times needed to solve each subproblem. Typically, the time to compute the solution to a subproblem is proportional to the degree (number of outgoing edges) of the corresponding vertex in the subproblem graph, and the number of subproblems is equal to the number of vertices in the subproblem graph. In this common case, the running time of dynamic programming is linear in the number of vertices and edges.

#### Reconstructing a Solution

The procedures **Memoized-Cut-Rod** and **Bottom-Up-Cut-Rod** return the value of an optimal solution to the rod-cutting problem, but they do not return the solution itself: a list of piece sizes.

Let's see how to extend the dynamic-programming approach to record not only the optimal value computed for each subproblem, but also a choice that led to the optimal value. With this information, you can readily print an optimal solution.
The procedure **Extended-Bottom-Up-Cut-Rod** computes, for each rod size $j,$ not only the maximum revenue $r_j,$ but also $s_j,$ the optimal size of the first piece to cut off. It's similar to **Bottom-Up-Cut-Rod**, except that it creates the array $s,$ an= it updates $s[j]$ to hold the optimal size $i$ of the first piece to cut off when solving a subproblem of size $j$.

The procedure **Print-Cut-Rod-Solution** takes as input an array $p[1 : n]$ of prices and a rod size $n$. It calls **Extended-Bottom-Up-Cut-Rod** to compute the array $s[1 : n]$ of optimal first-piece sizes. Then it prints out the complete list of piece sizes in an optimal decomposition of a rod of length $n$.
* **procedure** Extended-Bottom-Up-Cut-Rod$(p, n)$
  
  let $r[0 : n]$ and $s[1 : n]$ be new arrays
  $r[0] = 0$
  
  for $j = 1$ to $n$
  $\qquad$$q = -\infty$
  $\qquad$for $i = 1$ to $j$
  $\qquad \qquad$if $q < p[i] + r[j - i]$
  $\qquad \qquad \qquad$$q = p[i] + r[j - i]$
  $\qquad \qquad \qquad$$s[j] = i$
  $\qquad$$r[j] = q$
  return $r$ and $s$

> [!summary] Extended-Bottom-Up-Cut-Rod$(p,n)$
>   let $r[0 : n]$ and $s[1 : n]$ be new arrays
  $r[0] = 0$
  for $j = 1$ to $n$
  $\qquad$$q = -\infty$
  $\qquad$for $i = 1$ to $j$
  $\qquad \qquad$if $q < p[i] + r[j - i]$
  $\qquad \qquad \qquad$$q = p[i] + r[j - i]$
  $\qquad \qquad \qquad$$s[j] = i$
  $\qquad$$r[j] = q$
  return $r$ and $s$

* **procedure** Print-Cut-Rod-Solution$(p, n)$
  
  $(r, s) = \text{Extended-Bottom-Up-Cut-Rod}(p, n)$
  while $n > 0$
  $\qquad$print $s[n]$
  $\qquad$$n = n - s[n]$

> [!summary] Print-Cut-Rod-Solution $(p, n)$
> $(r, s) =$ Extended-Bottom-Up-Cut-Rod$(p, n)$
  while $n > 0$
  $\qquad$print $s[n]$
  $\qquad$$n = n - s[n]$

## Matrix-chain Multiplication

Our next example of dynamic programming is an algorithm that solves the problem of matrix-chain multiplication. Given a sequence (chain) $\braket{A_1, A_2, \ldots, A_n}$ of $n$ matrices to be multiplied, where the matrices aren't necessarily square, the goal is to compute the product $$\begin{align*}
& A_1 A_2 \cdots A_n. & (V)
\end{align*}$$using the standard algorithm for multiplying rectangular matrices, while minimizing the number of scalar multiplications.

You can evaluate the expression $(V)$ using the algorithm for multiplying pairs of rectangular matrices as a subroutine once you have parenthesize= it to resolve all ambiguities in how the matrices are multiplied together. Matrix multiplication is associative, and so all parenthesizations yield the same product. A product of matrices is **fully parenthesized** if it is either a single matrix or the product of two fully parenthesized matrix products, surrounded by parentheses.
For example, if the chain of matrices is $\braket{A_1, A_2, A_3, A_4},$ then you can fully parenthesize the product $A_1 A_2 A_3 A_4$ in five distinct ways: $$\begin{align*}
& (A_1 (A_2 (A_3 A_4))), & \\
& (A_1 ((A_2 A_3 )A_4)), & \\
& ((A_1 A_2 )(A_3A_4)), & \\
& ((A_1 (A_2 A_3 ))A_4), & \\
& (((A_1 A_2 )A_3)A_4).
\end{align*}$$
How you parenthesize a chain of matrices can have a dramatic impact on the cost of evaluating the product. Consider first the cost of multiplying two rectangular matrices. The standard algorithm is given by the procedure **Rectangular-Matrix-Multiply**, which generalizes the square-matrix multiplication procedure **Matrix-Multiply**.
The **Rectangular-Matrix-Multiply** procedure computes $C = C + A \cdot B$ for three matrices $A = (a_{ij}), B = (b_{ij}),$ and $C = (c_{ij}),$ where $A$ is $p \times q,$ $B$ is $q \times r$, and $C$ is $p \times r$.

* **procedure** Rectangular-Matrix-Multiply$(A, B, C, p, q, r)$
  
  for $i = 1$ to $p$
  $\qquad$for $j = 1$ to $q$
  $\qquad \qquad$for $k = 1$ to $r$
  $\qquad \qquad \qquad$$c_{ij} = c_{ij} + a_{ik} \cdot b_{kj}$

The running time of **Rectangular-Matrix-Multiply** is dominated by the number of scalar multiplications in last line, which is $pqr$. Therefore, we'll consider the cost of multiplying matrices to be the number of scalar multiplications. (The number of scalar multiplications dominates even if we consider initializing $C = 0$ to perform just $C = A \cdot B$.)

We state the **matrix-chain multiplication problem** as follows:
* Given a chain $\braket{A_1, A_2, \ldots, A_n}$ of $n$ matrices, where for $i = 1, 2, \ldots, n,$ matrix $A_i$ has dimension $p_{i - 1} \times p_i,$ fully parenthesize the product $A_1 A_2 \cdot \cdot \cdot A_n$ in a way that minimizes the number of scalar multiplications. The input is the sequence of dimensions $\braket{p_0, p_1, p_2, \ldots, p_n}$.

The matrix-chain multiplication problem does not entail actually multiplying matrices. The goal is only to determine an order for multiplying matrices that has the lowest cost. Typically, the time invested in determining this optimal order is more than paid for by the time saved later on when actually performing the matrix multiplications.

#### Counting the Number of Parenthesizations

Before solving the matrix-chain multiplication problem by dynamic programming, let us convince ourselves that exhaustively checking all possible parenthesizations is not an efficient algorithm.
Denote the number of alternative parenthesizations of a sequence of $n$ matrices by $P(n)$. When $n = 1,$ the sequence consists of just one matrix, and therefore there is only one way to fully parenthesize the matrix product. When $n \geqslant 2,$ a fully parenthesized matrix product is the product of two fully parenthesized matrix subproducts, and the split between the two subproducts may occur between the $k$th and $(k + 1)$st matrices for any $k = 1, 2, \ldots n - 1$. Thus, we obtain the recurrence $$\begin{align*}
& P(n) = \begin{cases} 1 \qquad \qquad \qquad \qquad \text{if} \space n = 1, \\ \displaystyle\sum_{k = 1}^{n - 1} P(k) P(k - 1) \quad \, \text{if} \space n \geqslant 2. \end{cases} & (VI)
\end{align*}$$We claim that the solution to a similar recurrence is the sequence of **Catalan numbers**, which grows as $\Omega(4^n /n^{3/2} )$. We can also show that the solution to the recurrence $(VI)$ is $\Omega(2^n)$. The number of solutions is thus exponential in n, and the brute-force method of exhaustive search makes for a poor strategy when determining how to optimally parenthesize a matrix chain.

#### Applying Dynamic Programming

Let's use the dynamic-programming method to determine how to optimally parenthesize a matrix chain, by following the four-step sequence that we stated at the beginning of this chapter:
###### Step 1: The Structure of an Optimal Parenthesization
 
In the first step of the dynamic-programming method, you find the optimal substructure and then use it to construct an optimal solution to the problem from optimal solutions to subproblems.
To perform this step for the matrix-chain multiplication problem, it's convenient to first introduce some notation. Let $A_{i : j},$ where $i \leqslant j,$ denote the matrix that results from evaluating the product $A_i A_{i + 1} \cdots A_j$. If the problem is nontrivial, that is, $i < j,$ then to parenthesize the product $A_i A_{i + 1} \cdots A_j,$ the product must split between $A_k$ and $A_{k + 1}$ for some integer $k$ in the range $i \leqslant k < j$. That is, for some value of $k,$ first compute the matrices $A_{i : k}$ and $A_{k + 1 : j},$ and then multiply them together to produce the final product $A_{i : j}$. The cost of parenthesizing this way is the cost of computing the matrix $A_{i : k},$ plus the cost of computing $A_{k + 1 : j},$ plus the cost of multiplying them together.

The optimal substructure of this problem is as follows. Suppose that to optimally parenthesize $A_i A_{i + 1} \cdots A_j,$ you split the product between $A_k$ and $A_{k + 1}$. Then the way you parenthesize the "prefix" subchain $A_i A_{i + 1} \cdots A_k$ within this optimal parenthesization of $A_i A_{i + 1} \cdots A_j$ must be an optimal parenthesization of $A_i A_{i + 1} \cdots A_k$. If there were a less costly way to parenthesize $A_i A_{i + 1} \cdots A_k,$ then you could substitute that parenthesization in the optimal parenthesization of $A_i A_{i + 1} \cdots A_j$ to produce another way to parenthesize $A_i A_{i + 1} \cdots A_j$ whose cost is lower than the optimum: a contradiction. A similar observation holds for how to parenthesize the subchain $A_{k + 1} A_{k + 2} \cdots A_j$ in the optimal parenthesization of
$A_i A_{i + 1} \cdots A_j :$ it must be an optimal parenthesization of $A_{k + 1} A_{k + 2} \cdots A_j$.

Now let's use the optimal substructure to show how to construct an optimal solution to the problem from optimal solutions to subproblems. Any solution to a nontrivial instance of the matrix-chain multiplication problem requires splitting the product, and any optimal solution contains within it optimal solutions to subproblem instances. Thus, to build an optimal solution to an instance of the matrix-chain multiplication problem, split the problem into two subproblems, find optimal solutions to the two subproblem instances, and then combine these optimal subproblem solutions. To ensure that you've examined the optimal split, you must consider all possible splits.

###### Step 2: A Recursive Solution

The next step is to define the cost of an optimal solution recursively in terms of the optimal solutions to subproblems. For the matrix-chain multiplication problem, a subproblem is to determine the minimum cost of parenthesizing $A_{i} A_{i + 1} \cdots A_j$ for $1 \leqslant i \leqslant j \leqslant n$. Given the input dimensions $\braket{p_0, p_1, p_2, \ldots, p_n},$ an index pair $i, j$ specifies a subproblem. Let $m[i, j]$ be the minimum number of scalar multiplications needed to compute the matrix $A_{i : j}$. For the full problem, the lowest-cost way to compute $A_{1 : n}$ is thus $m[1, n]$.

We can define $m[i, j]$ recursively as follows. If $i = j,$ the problem is trivial: the chain consists of just one matrix $A_{i : i} = A_{i},$ so that no scalar multiplications are necessary to compute the product. Thus, $m[i, i] = 0$ for $i = 1, 2, \ldots, n$. To compute $m[i, j]$ when $i < j,$ we take advantage of the structure of an optimal solution from step $1$.
Suppose that an optimal parenthesization splits the product $A_{i} A_{i + 1} \cdots A_j$ between $A_k$ and $A_{k + 1},$ where $i \leqslant k < j$. Then, $m[i, j]$ equals the minimum cost $m[i, k]$ for computing the subproduct $A_{i : k},$ plus the minimum cost $m[k + 1, j]$ for computing the subproduct, $A_{k + 1 : j},$ plus the cost of multiplying these two matrices together. Because each matrix $A_{i}$ is $p_{i - 1} \times p_i,$ computing the matrix product $A_{i : k} A_{k + 1 : j}$ takes $p_{i - 1} p_k p_j$ scalar multiplications. Thus, we obtain $$\begin{align*}
& m[i, j] = m[i, k] + m[k + 1, j] + p_{i - 1} p_k p_j. &
\end{align*}$$
This recursive equation assumes that you know the value of $k$. But you don't, at least not yet. You have to try all possible values of $k$. How many are there?
Just $j - i,$ namely $k = i, i + 1, \ldots, j - 1$. Since the optimal parenthesization must use one of these values for $k,$ you need only check them all to find the best. Thus, the recursive definition for the minimum cost of parenthesizing the product $A_{i} A_{i + 1} \cdots A_j$ becomes $$\begin{align*}
& m[i, j] = \begin{cases} 0 \qquad \qquad \qquad \qquad \qquad \qquad \qquad \qquad \qquad \qquad \quad \space \, \text{if} \space i = j, \\ \min \, \{m[i, k] + m[k + 1, j] + p_{i - 1} p_k p_j : i \leqslant k < j \} \quad \text{if} \space i < j. \end{cases} & (VII)
\end{align*}$$
The $m[i, j]$ values give the costs of optimal solutions to subproblems, but they do not provide all the information you need to construct an optimal solution. 
To help you do so, let's define $s[i, j]$ to be a value of $k$ at which you split the product $A_{i} A_{i + 1} \cdots A_j$ in an optimal parenthesization. That is, $s[i, j]$ equals a value $k$ such that $m[i, j] = m[i, k] +  m[k + 1, j] + p_{i - 1} p_k p_j$.

###### Step 3: Computing the Optimal Costs

At this point, you could write a recursive algorithm based on recurrence $(VII)$ to compute the minimum cost $m[1, n]$ for multiplying $A_1, A_2 \cdots A_n$. But as we saw for the rod-cutting problem, this recursive algorithm takes exponential time.

Fortunately, there aren't all that many distinct subproblems: just one subproblem for each choice of $i$ and $j$ satisfying $1 \leqslant i \leqslant j \leqslant n,$ or $\binom{n}{2} + n = \Theta(n^2)$ in all. A recursive algorithm may encounter each subproblem many times in different branches of its recursion tree. This property of overlapping subproblems is the second hallmark of when dynamic programming applies (the first hallmark being optimal substructure).

Instead of computing the solution to recurrence $(VII)$ recursively, let's compute the optimal cost by using a tabular, bottom-up approach, as in the procedure **Matrix-Chain-Order**. The input is a sequence $p = \braket{p_0, p_1, p_2, \ldots, p_n}$ of matrix dimensions, along with $n,$ so that for $i = 1, 2, \ldots, n,$ matrix $A_i$ has dimensions $p_{i - 1} \times p_i$. The procedure uses an auxiliary table $m[1 : n, 1 : n]$ to store the $m[i, j]$ costs and another auxiliary table $s[1 : n - 1, 2 : n]$ that records which index $k$ achieved the optimal cost in computing $m[i, j]$. The table $s$ will help in constructing an optimal solution.

 * **procedure** Matrix-Chain-Order$(p, n)$
   
   let $m[1 : n, 1 : n]$ and $s[1 : n - 1, 2 : n]$ be new tables
   for $i = 1$ to $n$
   $\qquad$$m[i, i] = 0$
   
   for $l = 2$ to $n$
   $\qquad$for $i = 1$ to $n - l + 1$
   $\qquad \qquad$$j = i + l - 1$
   $\qquad \qquad$$m[i, j] = \infty$
   
   $\qquad \qquad$for $k = i$ to $j - 1$
   $\qquad \qquad \qquad$$q = m[i, k] + m[k + 1, j] + p_{i - 1} p_k p_j$
   $\qquad \qquad \qquad$if $q < m[i, j]$
   $\qquad \qquad \qquad \qquad$$m[i, j] = q$
   $\qquad \qquad \qquad \qquad$$s[i, j] = k$
   return $m$ and $s$

*In what order should the algorithm fill in the table entries?* 
To answer this question, let's see which entries of the table need to be accessed when computing the cost $m[i, j]$. Equation $(VII)$ tells us that to compute the cost of matrix product $A_{i : j},$ first the costs of the products $A_{i : k}$ and $A_{k + 1 : j}$ need to have been computed for all $k = i, i + 1, \ldots, j - 1$. The chain $A_{i} A_{i + 1} \cdots A_j$ consists of $j - i + 1$ matrices, and the chains $A_{i} A_{i + 1} \cdots A_k$ and $A_{k + 1} A_{k + 2} \cdots A_j$ consist of $k - i + 1$ and $j - k$ matrices, respectively. Since $k < j,$ a chain of $k - i + 1$ matrices consists of fewer than $j - i + 1$ matrices. Likewise, since $k \geqslant i,$ a chain of $j - k$ matrices consists of fewer than $j - i + 1$ matrices. Thus, the algorithm should fill in the table $m$ from shorter matrix chains to longer matrix chains. That is, for the subproblem of optimally parenthesizing the chain $A_{i} A_{i + 1} \cdots A_j,$ it makes sense to consider the subproblem size as the length $j - i + 1$ of the chain.

Now, let's see how the **Matrix-Chain-Order** procedure fills in the $m[i, j]$ entries in order of increasing chain length. Lines initialize $m[i, i] = 0$ for $i = 1, 2, \ldots, n,$ since any matrix chain with just one matrix requires no scalar multiplications. In the first for loop, the loop variable $l$ denotes the length of matrix chains whose minimum costs are being computed. Each iteration of this loop uses recurrence $(VII)$ to compute $m[i, i + l - 1]$ for $i = 1, 2, \ldots, n - l + 1$. In the first iteration, $l = 2,$ and so the loop computes $m[i, i + 1]$ for $i = 1, 2, \ldots, n-1$: the minimum costs for chains of length $l = 2$. The second time through the loop, it computes $m[i, i + 2]$ for $i = 1, 2, \ldots, n - 2:$ the minimum costs for chains of length $l = 3$. And so on, ending with a single matrix chain of length $l = n$ and computing $m[1, n]$. When lines compute an $m[i, j]$ cost, this cost depends only on table entries $m[i, k]$ and $m[k + 1, j],$ which have already been computed.

A simple inspection of the nested loop structure of **Matrix-Chain-Order** yields a running time of $O(n^3)$ for the algorithm. The loops are nested three deep, and each loop index $(l, i,$ and $k)$ takes on at most $n - 1$ values. We claim that the running time of this algorithm is in fact also $\Omega(n^3)$. The algorithm requires $\Theta(n^2)$ space to store the $m$ and $s$ tables.
Thus, **Matrix-Chain-Order** is much more efficient than the exponential-time method of enumerating all possible parenthesizations and checking each one.

###### Step 4: Constructing an Optimal Solution

Although **Matrix-Chain-Order** determines the optimal number of scalar multiplications needed to compute a matrix-chain product, it does not directly show how to multiply the matrices. The table $s[1 : n - 1, 2 : n]$ provides the information needed to do so. Each entry $s[i, j]$ records a value of $k$ such that an optimal parenthesization of $A_{i} A_{i + 1} \cdots A_j$ splits the product between $A_k$ and $A_{k + 1}$.
The final matrix multiplication in computing $A_{1 : n}$ optimally is $A_{1 : s[1, n]} A_{s[1, n] + 1 : n}$. The $s$ table contains the information needed to determine the earlier matrix multiplications as well, using recursion: $s[1, s[1, n]]$ determines the last matrix multiplication when computing $A_{1 : s[1, n]}$ and $s[s[1, n] + 1, n]$ determines the last matrix multiplication when computing $A_{s[1, n] + 1 : n}$.

The recursive procedure **Print-Optimal-Parenthesization** prints an optimal parenthesization of the matrix chain product $A_{i} A_{i + 1} \cdots A_j,$ given the $s$ table computed by **Matrix-Chain-Order** and the indices $i$ and $j$. The initial call **Print-Optimal-Parenthesization** $(s, 1, n)$ prints an optimal parenthesization of the full matrix chain product $A_1 A_2 \cdots A_n$.

* **procedure** Print-Optimal-Parenthesization$(s, i, j)$
  
  if $i == j$
  $\qquad$print "A"$_i$
  else
  $\qquad$print "$($"
  $\qquad$Print-Optimal-Parenthesization$(s, i, s[i, j])$
  $\qquad$Print-Optimal-Parenthesization$(s, s[i, j] + 1, j)$
  $\qquad$print "$)$"


## Elements of Dynamic Programming

Although you have just seen two complete examples of the dynamic-programming method, you might still be wondering just when the method applies. From an engineering perspective, when should you look for a dynamic-programming solution to a problem?

#### Optimal Substructure

The first step in solving an optimization problem by dynamic programming is to characterize the structure of an optimal solution. Recall that a problem exhibits **optimal substructure** if an optimal solution to the problem contains within it optimal solutions to subproblems.
When a problem exhibits optimal substructure, that gives you a good clue that dynamic programming might apply. Dynamic programming builds an optimal solution to the problem from optimal solutions to subproblems. Consequently, you must take care to ensure that the range of subproblems you consider includes those used in an optimal solution.

You will find yourself following a common pattern in discovering optimal substructure:

* You show that a solution to the problem consists of making a choice, such as choosing an initial cut in a rod or choosing an index at which to split the matrix chain. Making this choice leaves one or more subproblems to be solved.

* You suppose that for a given problem, you are given the choice that leads to an optimal solution. You do not concern yourself yet with how to determine this choice. You just assume that it has been given to you.

* Given this choice, you determine which subproblems ensue and how to best characterize the resulting space of subproblems.

* You show that the solutions to the subproblems used within an optimal solution to the problem must themselves be optimal by using a "*cut-and-paste*" technique.
  You do so by supposing that each of the subproblem solutions is not optimal and then deriving a contradiction. In particular, by "cutting out" the non-optimal solution to each subproblem and "pasting in" the optimal one, you show that you can get a better solution to the original problem, thus contradicting your supposition that you already had an optimal solution. If an optimal solution gives rise to more than one subproblem, they are typically so similar that you can modify the cut-and-paste argument for one to apply to the others with little effort.


To characterize the space of subproblems, a good rule of thumb says to try to keep the space as simple as possible and then expand it as necessary. For example, the space of subproblems for the rod-cutting problem contained the problems of optimally cutting up a rod of length $i$ for each size $i$. This subproblem space worked well, and it was not necessary to try a more general space of subproblems.

Optimal substructure varies across problem domains in two ways:

* how many subproblems an optimal solution to the original problem uses, and
* how many choices you have in determining which subproblem(s) to use in an optimal solution.

Informally, the running time of a dynamic-programming algorithm depends on the product of two factors: the number of subproblems overall and how many choices you look at for each subproblem. In rod cutting, we had $\Theta(n)$ subproblems overall, and at most $n$ choices to examine for each, yielding an $O(n^2)$ running time. Matrix-chain multiplication had $\Theta(n^2)$ subproblems overall, and each had at most $n - 1$ choices, giving an $O(n^3)$ running time (actually, a $\Theta(n^3)$ running time. Usually, the subproblem graph gives an alternative way to perform the same analysis. Each vertex corresponds to a subproblem, and the choices for a subproblem are the edges incident from that subproblem.

Dynamic programming often uses optimal substructure in a bottom-up fashion. That is, you first find optimal solutions to subproblems and, having solved the subproblems, you find an optimal solution to the problem. Finding an optimal solution to the problem entails making a choice among subproblems as to which you will use in solving the problem. The cost of the problem solution is usually the subproblem costs plus a cost that is directly attributable to the choice itself.

Next chapter explores "greedy algorithms," which have many similarities to dynamic programming. In particular, problems to which greedy algorithms apply have optimal substructure. One major difference between greedy algorithms and dynamic programming is that instead of first finding optimal solutions to subproblems and then making an informed choice, greedy algorithms first make a "greedy" choice$-$the choice that looks best at the time$-$and then solve a resulting subproblem, without bothering to solve all possible related smaller subproblems.

#### Overlapping Problems

The second ingredient that an optimization problem must have for dynamic programming to apply is that the space of subproblems must be "small" in the sense that a recursive algorithm for the problem solves the same subproblems over and over, rather than always generating new subproblems. Typically, the total number of distinct subproblems is a polynomial in the input size. When a recursive algorithm revisits the same problem repeatedly, we say that the optimization problem has overlapping subproblems.

In contrast, a problem for which a divide-and-conquer approach is suitable usually generates brand-new problems at each step of the recursion. Dynamic-programming algorithms typically take advantage of overlapping subproblems by solving each subproblem once and then storing the solution in a table where it can be looked up when needed, using constant time per lookup.

If we compare top-down, recursive algorithm (without memoization) with the bottom-up dynamic-programming algorithm; the latter is more efficient because it takes advantage of the overlapping-subproblems property. Matrix-chain multiplication has only $\Theta(n^2)$ distinct subproblems, and the dynamic-programming algorithm solves each exactly once.
The recursive algorithm, on the other hand, must solve each subproblem every time it reappears in the recursion tree. Whenever a recursion tree for the natural recursive solution to a problem contains the same subproblem repeatedly, and the total number of distinct subproblems is small, dynamic programming can improve efficiency.

#### Reconstructing an Optimal Solution : Memoization

As we saw for the rod-cutting problem, there is an alternative approach to dynamic programming that often offers the efficiency of the bottom-up dynamic-programming approach while maintaining a top-down strategy. The idea is to memoize the natural, but inefficient, recursive algorithm. As in the bottom-up approach, you maintain a table with subproblem solutions, but the control structure for filling in the table is more like the recursive algorithm.

A memoized recursive algorithm maintains an entry in a table for the solution to each subproblem. Each table entry initially contains a special value to indicate that the entry has yet to be filled in. When the subproblem is first encountered as the recursive algorithm unfolds, its solution is computed and then stored in the table. Each subsequent encounter of this subproblem simply looks up the value stored in the table and returns it.

In general practice, if all subproblems must be solved at least once, a bottom-up dynamic-programming algorithm usually outperforms the corresponding top-down memoized algorithm by a constant factor, because the bottom-up algorithm has no overhead for recursion and less overhead for maintaining the table.
Moreover, for some problems you can exploit the regular pattern of table accesses in the dynamic-programming algorithm to reduce time or space requirements even further. On the other hand, in certain situations, some of the subproblems in the subproblem space might not need to be solved at all. In that case, the memoized solution has the advantage of solving only those subproblems that are definitely required.

## Longest Common Subsequence

Biological applications often need to compare the DNA of two (or more) different organisms. A strand of DNA consists of a string of molecules called **bases**, where the possible bases are adenine, cytosine, guanine, and thymine.

We formalize the notion of similarity between DNA as the longest-common-subsequence problem. A subsequence of a given sequence is just the given sequence with $0$ or more elements left out. Formally, given a sequence $X = \braket{x_1, x_2, \ldots, x_m}$, another sequence $Z = \braket{z_1, z_2, \ldots, z_k}$ is a **subsequence** of $X$ if there exists a strictly increasing sequence $\braket{i_1, i_2, \ldots, i_k}$ of indices of $X$ such that for all $j = 1, 2, \ldots, k,$ we have $x_{i_j} = z_j$. 

Given two sequences $X$ and $Y,$ we say that a sequence $Z$ is a common subsequence of $X$ and $Y$ if $Z$ is a subsequence of both $X$ and $Y$. In the longest-common-subsequence **(LCS)** problem, the input is two sequences $X = \braket{x_1, x_2, \ldots, x_m}$ and $Y  = \braket{y_1, y_2, \ldots, y_n},$ and the goal is to find a maximum-length common subsequence of $X$ and $Y$.

#### Step 1: Characterizing a Longest Common Subsequence

You can solve the LCS problem with a brute-force approach: enumerate all subsequences of $X$ and check each subsequence to see whether it is also a subsequence of $Y,$ keeping track of the longest subsequence you find. Each subsequence of $X$ corresponds to a subset of the indices $\{1, 2, \ldots, m\}$ of $X$. Because $X$ has $2^m$ subsequences, this approach requires exponential time, making it impractical for long sequences.

The LCS problem has an optimal-substructure property, however, as the following theorem shows. As we'll see, the natural classes of subproblems correspond to pairs of "prefixes" of the two input sequences. To be precise, given a sequence $X = \braket{x_1, x_2, \ldots, x_m},$ we define the $i$th prefix of $X,$ for $i = 0, 1, \ldots, m,$ as $X = \braket{x_1, x_2, \ldots, x_i}$.

* **Theorem (I)** (Optimal Substructure of an LCS)
  $\newline$
  Let $X = \braket{x_1, x_2, \ldots, x_m}$ and $Y  = \braket{y_1, y_2, \ldots, y_n}$ be sequences, and let $Z = \braket{z_1, z_2, \ldots, z_k}$ be any LCS of $X$ and $Y$.
  
  * If $x_m = y_n,$ then $z_k = x_m = y_n$ and $Z_{k - 1}$ is an LCS of $X_{m - 1}$ and $Y_{n - 1}$.
  * If $x_m \neq y_n$ and $z_k \neq x_m,$ then $Z$ is an LCS of $X_{m - 1}$ and $Y$.
  * If $x_m \neq y_n$ and $z_k \neq y_n,$ then $Z$ is an LCS of $X$ and $Y_{n - 1}$.
  
  $\newline$
  **Proof**:
  * $(1):$ If $z_k \neq x_m,$ then we could append $x_m = y_n$ to $Z$ to obtain a common subsequence of $X$ and $Y$ of length $k + 1,$ contradicting the supposition that $Z$ is a longest common subsequence of $X$ and $Y$. Thus, we must have $z_k = x_m = y_n$.
    Now, the prefix $Z_{k - 1}$ is a length-$(k - 1)$ common subsequence of $X_{m - 1}$ and $Y_{n - 1}$. We wish to show that it is an LCS. Suppose for the purpose of contradiction that there exists a common subsequence $W$ of $X_{m - 1}$ and $Y_{n - 1}$ with length greater than $k - 1$. Then, appending $x_m = y_n$ to $W$ produces a common subsequence of $X$ and $Y$ whose length is greater than $k,$ which is a contradiction.
    $\newline$
  * $(2):$ If $z_k \neq x_m,$ then $Z$ is a common subsequence of $X_{m - 1}$ and $Y$. If there were a common subsequence $W$ of $X_{m - 1}$ and $Y$ with length greater than $k,$ then $W$ would also be a common subsequence of $X_m$ and $Y,$ contradicting the assumption that $Z$ is an LCS of $X$ and $Y$.
    $\newline$
  * $(2):$ If $z_k \neq y_n,$ then $Z$ is a common subsequence of $X$ and $Y_{n - 1}$. If there were a common subsequence $W$ of $X$ and $Y_{n - 1}$ with length greater than $k,$ then $W$ would also be a common subsequence of $X$ and $Y_n,$ contradicting the assumption that $Z$ is an LCS of $X$ and $Y$.    

The way that **Theorem (I)** characterizes longest common subsequences says that an LCS of two sequences contains within it an LCS of prefixes of the two sequences. Thus, the LCS problem has an optimal-substructure property. A recursive solution also has overlapping-subproblems property.

#### Step 2: A Recursive Solution

**Theorem (I)** implies that you should examine either one or two subproblems when finding an LCS of $X = \braket{x_1, x_2, \ldots, x_m}$ and $Y  = \braket{y_1, y_2, \ldots, y_n}$:

* If $x_m = y_n,$ you need to find an LCS of $X_{m - 1}$ and $Y_{n - 1}$. Appending $x_m = y_n$ to this LCS yields an LCS of $X$ and $Y$.
* If $x_m \neq y_n,$ then you have to solve two subproblems: finding an LCS of $X_{m- 1}$ and $Y$ and finding an LCS of $X$ and $Y_{n - 1}$.

Whichever of these two LCSs is longer is an LCS of $X$ and $Y$. Because these cases exhaust all possibilities, one of the optimal subproblem solutions must appear within an LCS of $X$ and $Y$.

The LCS problem has the overlapping-subproblems property. To find an LCS of $X$ and $Y,$ you might need to find the LCSs of $X$ and $Y_{n - 1}$ and of $X_{m - 1}$ and $Y$. But each of these subproblems has the subsubproblem of finding an LCS of $X_{m - 1}$ and $Y_{n - 1}$. Many other subproblems share subsubproblems.

As in the matrix-chain multiplication problem, solving the LCS problem recursively involves establishing a recurrence for the value of an optimal solution. Let's define $c[i, j]$ to be the length of an LCS of the sequences $X_i$ and $Y_j$. If either $i = 0$ or $j = 0,$ one of the sequences has length $0,$ and so the LCS has length $0$. The optimal substructure of the LCS problem gives the recursive formula $$\begin{align*}
& c[i, j] =
\begin{cases}
0 \qquad \qquad \qquad \qquad \qquad \qquad \quad \text{if} \space i = 0 \space \text{or} \space j = 0, \\ 
c[i - 1, j - 1] + 1 \qquad \qquad \qquad \, \text{if} \space i, j > 0 \space \text{and} \space x_i = y_j, \\
\max \, \{c[i, j - 1], c[i - 1, j]\} \qquad \space \text{if} \space i, j > 0 \space \text{and} \space x_i \ne y_j.
\end{cases} & (VIII)
\end{align*}$$
In this recursive formulation, a condition in the problem restricts which subproblems to consider. When $x_i = y_j,$ you can and should consider the subproblem of finding an LCS of $X_{i - 1}$ and $Y_{j - 1}$. Otherwise, you instead consider the two subproblems of finding an LCS of $X_i$ and $Y_{j - 1}$ and of $X_{i - 1}$ and $Y_j$.
In the previous dynamic-programming algorithms we have examined, we didn't rule out any subproblems due to conditions in the problem. Finding an LCS is not the only dynamic-programming algorithm that rules out subproblems based on conditions in the problem.

#### Step 3: Computing the Length of an LCS

Based on equation $(VIII),$ you could write an exponential-time recursive algorithm to compute the length of an LCS of two sequences. Since the LCS problem has only $\Theta(mn)$ distinct subproblems (computing $c[i, j]$ for $0 \leqslant i \leqslant m$ and $0 \leqslant j \leqslant n),$ dynamic programming can compute the solutions bottom up.

The procedure **LCS-Length** takes two sequences $X = \braket{x_1, x_2, \ldots, x_m}$ and $Y  = \braket{y_1, y_2, \ldots, y_n}$ as inputs, along with their lengths. It stores the $c[i, j]$ values in a table $c[0 : m, 0 : n],$ and it computes the entries in **row-major order**. That is, the procedure fills in the first row of $c$ from left to right, then the second row, and so on.
The procedure also maintains the table $b[1 : m, 1 : n]$ to help in constructing an optimal solution. Intuitively, $b[i, j]$ points to the table entry corresponding to the optimal subproblem solution chosen when computing $c[i, j]$. The procedure returns the $b$ and $c$ tables, where $c[m, n]$ contains the length of an LCS of $X$ and $Y$. The running time of the procedure is $\Theta(mn),$ since each table entry takes $\Theta(1)$ time to compute.

* **procedure** LCS-Length$(X, Y, m, n)$
  $\newline$
  let $b[1 : m, 1 : n]$ and $c[0 : m, 0 : n]$ be new tables
  
  for $i = 1$ to $m$
  $\qquad$$c[i, 0] = 0$
  for $j = 0$ to $n$
  $\qquad$$c[0, j] = 0$
  
  for $i = 1$ to $m$
  $\qquad$for $j = 1$ to $n$
  $\qquad \qquad$if $x_i == y_j$
  $\qquad \qquad \qquad$$c[i, j] = c[i - 1, j - 1] + 1$
  $\qquad \qquad \qquad$$b[i, j] =$ $\nwarrow$
  $\qquad \qquad$else if $c[i - 1, j] \geqslant c[i, j - 1]$
  $\qquad \qquad \qquad$$c[i, j] = c[i - 1, j]$
  $\qquad \qquad \qquad$$b[i, j] =$ $\uparrow$
  $\qquad \qquad$else
  $\qquad \qquad \qquad$$c[i, j] = c[i, j - 1]$
  $\qquad \qquad \qquad$$b[i, j] =$ $\leftarrow$
 return $c$ and $b$

#### Step 4: Constructing an LCS

With the $b$ table returned by **LCS-Length**, you can construct an LCS of $X = \braket{x_1, x_2, \ldots, x_m}$ and $Y  = \braket{y_1, y_2, \ldots, y_n}$. Begin at $b[m, n]$ and trace through the table by following the arrows. Each $\nwarrow$ encountered in an entry $b[i, j]$ implies that $x_i = y_j$ is an element of the LCS that **LCS-Length** found. This method gives you the elements of this LCS in reverse order. The recursive procedure **Print-LCS** prints out an LCS of $X$ and $Y$ in the proper, forward order.

* **procedure** Print-LCS$(b, X, i, j)$
  $\newline$
  if $i == 0$ or $j == 0$
  $\qquad$return
  
  if $b[i, j] ==$ $\nwarrow$
  $\qquad$Print-LCS$(b, X, i - 1, j - 1)$
  $\qquad$print $x_i$
  else if $b[i, j] ==$ $\uparrow$
  $\qquad$Print-LCS$(b, X, i - 1, j)$
  else
  $\qquad$Print-LCS$(b, X, i, j - 1)$

The initial call is **Print-LCS**$(b, X, m, n)$. The procedure takes $O(m + n)$ time, since it decrements at least one of $i$ and $j$ in each recursive call.

#### Improving the Code

Once you have developed an algorithm, you will often find that you can improve on the time or space it uses. Some changes can simplify the code and improve constant factors but otherwise yield no asymptotic improvement in performance. Others can yield substantial asymptotic savings in time and space.

In the LCS algorithm, for example, you can eliminate the $b$ table altogether. Each $c[i, j]$ entry depends on only three other $c$ table entries: $c[i - 1, j - 1], c[i - 1, j],$ and $c[i, j - 1]$. Given the value of $c[i, j],$ you can determine in $O(1)$ time which of these three values was used to compute $c[i, j],$ without inspecting table $b$. Thus, you can reconstruct an LCS in $O(m + n)$ time using a procedure similar to **Print-LCS**. Although this method saves $\Theta(mn)$ space, the auxiliary space requirement for computing an LCS does not asymptotically decrease, since the $c$ table takes $\Theta(mn)$ space anyway.

You can, however, reduce the asymptotic space requirements for **LCS-Length**, since it needs only two rows of table $c$ at a time: the row being computed and the previous row. (In fact, you can use only slightly more than the space for one row of c to compute the length of an LCS.) This improvement works if you need only the length of an LCS. If you need to reconstruct the elements of an LCS, the smaller table does not keep enough information to retrace the algorithm's steps in $O(m + n)$ time.

## Optimal Binary Search Trees

Suppose that you are designing a program to translate text from English to Latvian. For each occurrence of each English word in the text, you need to look up its Latvian equivalent. You can perform these lookup operations by building a binary search tree with n English words as keys and their Latvian equivalents as satellite data. Because you will search the tree for each individual word in the text, you want the total time spent searching to be as low as possible.
You can ensure an $O(\lg n)$ search time per occurrence by using a red-black tree or any other balanced binary search tree. Words appear with different frequencies. You want words that occur frequently in the text to be placed nearer the root.

*How can you organize a binary search tree so as to minimize the number of nodes visited in all searches, given that you know how often each word occurs?*

What you need is an **optimal binary search tree**.
Formally, given a sequence $K = \braket{k_1, k_2, \ldots, k_n}$ of $n$ distinct keys such that $k_1 < k_2 < \ldots < k_n,$ build a binary search tree containing them. For each key $k_i,$ you are given the probability $p_i$ that any given search is for key $k_i$. Since some searches may be for values not in $K,$ you also have $n + 1$ "dummy" keys $d_0, d_1, d_2, \ldots, d_n$ representing those values.
In particular, $d_0$ represents all values less than $k_1,$ $d_n$ represents all values greater than $k_n,$ and for $i = 1, 2, \ldots n - 1,$ the dummy key $d_i$ represents all values between $k_i$ and $k_{i + 1}$. For each dummy key $d_i,$ you have the probability $q_i$ that a search corresponds to $d_i$. (Each key $k_i$ is an internal node, and each dummy key $d_i$ is a leaf.) Since every search is either successful (finding some key $k_i$) or unsuccessful (finding some dummy key $d_i),$ we have $$\begin{align*}
& \sum_{i = 1}^{n} p_i + \sum_{i = 0}^{n - 1} q_i = 1. & (IX)
\end{align*}$$
Knowing the probabilities of searches for each key and each dummy key allows us to determine the expected cost of a search in a given binary search tree $T$. Let us assume that the actual cost of a search equals the number of nodes examined, which is the depth of the node found by the search in $T,$ plus $1$. Then the expected cost of a search in $T$ is $$\begin{align*}
& \, E[\mathrm{search \space cost \space in} \space T] = \sum_{i = 1}^{n} (\operatorname{depth}_T(k_i) + 1) \cdot p_i + \sum_{i = 0}^{n} (\operatorname{depth}_T(d_i) + 1) \cdot q_i & \\
& \qquad \qquad \qquad \qquad \space = 1 + \sum_{i = 1}^{n} \operatorname{depth}_T(k_i) \cdot p_i + \sum_{i = 0}^{n} \operatorname{depth}_T(d_i) \cdot q_i, & (X)
\end{align*}$$
where $\operatorname{depth}_T$ denotes a node's depth in the tree $T$. The last equation follows from equation $(IX)$.

For a given set of probabilities, your goal is to construct a binary search tree whose expected search cost is smallest. We call such a tree an **optimal binary search tree**. An  optimal binary search tree is not necessarily a tree whose overall height is smallest. Nor does an optimal binary search tree always have the key with the greatest probability at the root.

As with matrix-chain multiplication, exhaustive checking of all possibilities fails to yield an efficient algorithm. You can label the nodes of any $n$-node binary tree with the keys $k_1, k_2, \ldots, k_n$ to construct a binary search tree, and then add in the dummy keys as leaves. Earlier, we saw that the number of binary trees with $n$ nodes is $\Omega(4^n/n^{3/2})$.
Thus you would need to examine an exponential number of binary search trees to perform an exhaustive search. We'll see how to solve this problem more efficiently with dynamic programming.

#### Step 1: The Structure of an Optimal Binary Search Tree

To characterize the optimal substructure of optimal binary search trees, we start with an observation about subtrees. Consider any subtree of a binary search tree. It must contain keys in a contiguous range $k_i, \ldots, k_j,$ for some $1 \leqslant i \leqslant j \leqslant n$. In addition, a subtree that contains keys $k_i, \ldots, k_j$ must also have as its leaves the dummy keys $d_{i - 1}, \ldots, d_j$.

Now we can state the optimal substructure:

* If an optimal binary search tree $T$ has a subtree $T'$ containing keys $k_i, \ldots, k_j,$ then this subtree $T'$ must be optimal as well for the subproblem with keys $k_i, \ldots, k_j$ and dummy keys $d_{i - 1}, \ldots, d_j$. The usual cut-and-paste argument applies. If there were a subtree $T''$ whose expected cost is lower than that of $T',$ then cutting $T'$ out of $T$ and pasting in $T''$ would result in a binary search tree of lower expected cost than $T,$ thus contradicting the optimality of $T$.

With the optimal substructure in hand, here is how to construct an optimal solution to the problem from optimal solutions to subproblems. Given keys $k_i, \ldots, k_j,$ one of these keys, say $k_r \, (i \leqslant r \leqslant j ),$ is the root of an optimal subtree containing these keys. The left subtree of the root $k_r$ contains the keys $k_i, \ldots, k_{r - 1}$ (and dummy keys $d_{i - 1}, \ldots, d_{r - 1}$), and the right subtree contains the keys $k_{r + 1}, \ldots, k_j$ (and dummy keys $d_r, \ldots, d_j$).
As long as you examine all candidate roots $k_r,$ where $i \leqslant r \leqslant j,$ and you determine all optimal binary search trees containing $k_i, \ldots, k_{r - 1}$ and those containing $k_{r + 1}, \ldots, k_j,$ you are guaranteed to find an optimal binary search tree.

There is one technical detail worth understanding about "empty" subtrees. Suppose that in a subtree with keys $k_i, \ldots, k_j,$ you select $k_i$ as the root. By the above argument, $k_i$'s left subtree contains the keys $k_i, \ldots, k_{i - 1}$: no keys at all. Bear in mind, however, that subtrees also contain dummy keys.
We adopt the convention that a subtree containing keys $k_i, \ldots, k_{i - 1}$ has no actual keys but does contain the single dummy key $d_{i - 1}$. Symmetrically, if you select $k_j$ as the root, then $k_j$'s right subtree contains the keys $k_{j + 1}, \ldots, k_j$. This right subtree contains no actual keys, but it does contain the dummy key $d_j$.

#### Step 2: A Recursive Solution

To define the value of an optimal solution recursively, the subproblem domain is finding an optimal binary search tree containing the keys $k_i, \ldots, k_j,$ where $i \geqslant 1, j \leqslant n,$ and $j \geqslant i - 1$. (When $j = i - 1,$ there is just the dummy key $d_{i - 1},$ but no actual keys.) Let $e[i, j]$ denote the expected cost of searching an optimal binary search tree containing the keys $k_i, \ldots, k_j$. Your goal is to compute $e[1, n],$ the expected cost of searching an optimal binary search tree for all the actual and dummy keys.

The easy case occurs when $j = i - 1$. Then the subproblem consists of just the dummy key $d_{i - 1}$. The expected search cost is $e[i, i - 1] = q_{i - 1}$. 

When $j \geqslant i,$ you need to select a root $k_r$ from among $k_i, \ldots, k_j$ and then make an optimal binary search tree with keys $k_i, \ldots, k_{r - 1}$ as its left subtree and an optimal binary search tree with keys $k_{r + 1}, \ldots, k_j$ as its right subtree. 

*What happens to the expected search cost of a subtree when it becomes a subtree of a*
*node?* 
The depth of each node in the subtree increases by $1$. By equation $(X),$ the expected search cost of this subtree increases by the sum of all the probabilities in the subtree. For a subtree with keys $k_i, \ldots, k_j,$ denote this sum of probabilities as $$\begin{align*}
& w(i, j) = \sum_{l = i}^{j} p_l + \sum_{l = i - 1}^{j} q_l. & (XI)
\end{align*}$$Thus, if $k_r$ is the root of an optimal subtree containing keys $k_i, \ldots, k_j,$ we have $$\begin{align*}
& e[i, j] = p_r + (e[i, r - 1] + w(i, r - 1)) + (e[r + 1, j] + w(r + 1, j)). &
\end{align*}$$
Noting that $$\begin{align*}
& w(i, j) = w(i, r - 1) + p_r + w(r + 1, j), &
\end{align*}$$we rewrite $e[i, j]$ as $$\begin{align*}
& e[i, j] = e[i, r - 1] + e[r + 1, j] + w(i, j). & (XII)
\end{align*}$$
The recursive equation $(XII)$ assumes that you know which node $k_r$ to use as the root. Of course, you choose the root that gives the lowest expected search cost, giving the final recursive formulation: $$\begin{align*}
& e[i, j] = \begin{cases} q_{i - 1} \qquad \qquad \qquad \qquad \qquad \qquad \qquad \qquad \qquad \qquad \text{if} \space j = i - 1, \\ \min \, \{e[i, r - 1] + e[r + 1, j] + w(i, j) : i \leqslant r \leqslant j\} \quad \text{if} \space i \leqslant j. \end{cases} & (XIII)
\end{align*}$$The $e[i, j]$ values give the expected search costs in optimal binary search trees.

To help keep track of the structure of optimal binary search trees, define $\mathrm{root}[i, j],$ for $1 \leqslant i \leqslant j \leqslant n,$ to be the index $r$ for which $k_r$ is the root of an optimal binary search tree containing keys $k_i, \ldots, k_j$.

#### Step 3: Computing the Expected Search Cost of an Optimal BST

At this point, you may have noticed some similarities between our characterizations of optimal binary search trees and matrix-chain multiplication. For both problem domains, the subproblems consist of contiguous index subranges. A direct, recursive implementation of equation $(XIII)$ would be just as inefficient as a direct, recursive matrix-chain multiplication algorithm.
Instead, you can store the $e[i, j]$ values in a table $e[1 : n + 1, 0 : n]$. The first index needs to run to $n + 1$ rather than $n$ because in order to have a subtree containing only the dummy key $d_n,$ you need to compute and store $e[n + 1, n]$. The second index needs to start from $0$ because in order to have a subtree containing only the dummy key $d_0,$ you need to compute and store $e[1; 0]$. Only the entries $e[i, j]$ for which $j \geqslant i - 1$ are filled in.
The table $\mathrm{root}[i, j]$ records the root of the subtree containing keys $k_i, \ldots, k_j$ and uses only the entries for which $1 \leqslant i \leqslant j \leqslant n$.

One other table makes the dynamic-programming algorithm a little faster. Instead of computing the value of $w(i, j)$ from scratch every time you compute $e[i, j],$ which would take $\Theta(j - i)$ additions, store these values in a table $w[1 : n + 1, 0 : n]$.

For the base case, compute $w[i, i - 1] = q_{i - 1}$ for $1 \leqslant i \leqslant n + 1$. For $j \geqslant i,$ compute $$\begin{align*}
& w[i, j] = w[i, j - 1] + p_j + q_j. & (XIV)
\end{align*}$$Thus, you can compute the $\Theta(n^2)$ values of $w[i, j]$ in $\Theta(1)$ time each.

The **Optimal-BST** procedure takes as inputs the probabilities $p_1, \ldots, p_n$ and $q_0, \ldots, q_n$ and the size $n,$ and it returns the tables $e$ and $\mathrm{root}$.

 * **procedure** Optimal-BST$(p, q, n)$
   
   let $e[1 : n + 1; 0 : n], w[1 : n + 1, 0 : n],$ and $\mathrm{root}[1 : n; 1 : n]$ be new tables
   
   for $i = 1$ to $n + 1$
   $\qquad$$e[i, i - 1] = q_{i - 1}$
   $\qquad$$w[i, i - 1] = q_{i - 1}$
   
   for $l = 1$ to $n$
   $\qquad$for $i = 1$ to $n - l + 1$
   $\qquad \qquad$$j = i + l - 1$
   $\qquad \qquad$$e[i, j] = 1$
   $\qquad \qquad$$w[i, j] = w[i, j - 1] + p_j + q_j$
   
   $\qquad \qquad$for $r = i$ to $j$
   $\qquad \qquad \qquad$$t = e[i, r - 1] + e[r + 1, j] + w[i, j]$
   $\qquad \qquad \qquad$if $t < e[i, j]$
   $\qquad \qquad \qquad \qquad$$e[i, j] = t$
   $\qquad \qquad \qquad \qquad$$\mathrm{root}[i, j] = r$
   return $e$ and $\mathrm{root}$

The very first for loop initializes the values of $e[i, i - 1]$ and $w[i, i - 1]$. Then the second for loop uses the recurrences $(XIII)$ and $(XIV)$ to compute e$[i, j]$ and $w[i, j]$ for all $1 \leqslant i \leqslant j \leqslant n$. In the first iteration, when $l = 1,$ the loop computes $e[i, i]$ and $w[i, i]$ for $i = 1, 2, \ldots, n$. The second iteration, with $l = 2,$ computes $e[i, i + 1]$ and $w[i, i + 1]$ for $i = 1, 2, \ldots, n - 1,$ and so on. The innermost for loop, tries each candidate index $r$ to determine which key $k_r$ to use as the root of an optimal binary search tree containing keys $k_i, \ldots, k_j$. This for loop saves the current value of the index $r$ in $\mathrm{root}[i, j]$ whenever it finds a better key to use as the root.

The **Optimal-BST** procedure takes $\Theta(n^3)$ time, just like **Matrix-Chain-Order**. Its running time is $O(n^3),$ since its for loops are nested three deep and each loop index takes on at most $n$ values. The loop indices in **Optimal-BST** do not have exactly the same bounds as those in **Matrix-Chain-Order**, but they are within at most $1$ in all directions. Thus, like **Matrix-Chain-Order**, the **Optimal-BST** procedure takes $\Omega(n^3)$ time.





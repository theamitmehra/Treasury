# Induction and Recursion
## Mathematical Induction
#### Introduction
In general, mathematical induction can be used to prove statements that assert that $P(n)$ is true for all positive integers $n$, where $P(n)$ is a propositional function.

* **PRINCIPLE OF MATHEMATICAL INDUCTION** :
  To prove that $P(n)$ is true for all positive integers $n$, where $P(n)$ is a propositional function, we complete two steps:
	 * **Basis Step** : We verify that $P(1)$ is true.
	 * **Inductive Step** : We show that the conditional statement $P(k) \rightarrow P(k + 1)$ is true for all positive integers $k$.

To complete the inductive step of a proof using the principle of mathematical induction, we assume that $P(k)$ is true for an arbitrary positive integer $k$ and show that under this assumption, $P(k + 1)$ must also be true. The assumption that $P(k)$ is true is called the **inductive hypothesis**. Expressed as a rule of inference, this proof technique can be stated as $$ \begin{align*}
& (P(1) \land ∀ k(P(k) \rightarrow P(k + 1))) \rightarrow \forall nP(n), &
\end{align*}$$when the domain is the set of positive integers.
#### Why Mathematical Induction Is Valid ? 
The reason comes from the well-ordering property.
* **Axiom** : The Well-Ordering Property
  Every nonempty subset of the set of positive integers has a least element.

So, suppose we know that $P(1)$ is true and that the proposition $P(k) \rightarrow P(k + 1)$ is true for all positive integers $k$. To show that $P(n)$ must be true for all positive integers $n$, assume that there is at least one positive integer $n$ for which $P(n)$ is false. Then the set $S$ of positive integers $n$ for which $P(n)$ is false is nonempty. Thus, by the well-ordering property, $S$ has a least element, which will be denoted by $m$. We know that $m$ cannot be $1$, because $P(1)$ is true. Because $m$ is positive and greater than $1$, $m - 1$ is a positive integer. 
Furthermore, because $m - 1$ is less than $m$, it is not in $S$, so $P(m - 1)$ must be true. Because the conditional statement $P(m - 1) \rightarrow P(m)$ is also true, it must be the case that $P(m)$ is true. This contradicts the choice of $m$. Hence, $P(n)$ must be true for every positive integer $n$.

#### Guidelines For Proofs by Mathematical Induction
Before we give these proofs, we will provide some useful guidelines for constructing correct proofs by mathematical induction.

*Template for Proofs by Mathematical Induction*
* Express the statement that is to be proved in the form "for all $n \geq b, P(n)$" for a fixed integer $b$. 
* For statements of the form "$P(n)$ for all positive integers $n$," let $b = 1$, and 
* for statements of the form "$P(n)$ for all non-negative integers $n$," let $b = 0$.
* For some statements of the form $P(n)$, such as inequalities, you may need to determine the appropriate value of $b$ by checking the truth values of $P(n)$ for small values of $n$.
* Write out the words "Basis Step." Then show that $P(b)$ is true, taking care that the correct value of $b$ is used. This completes the first part of the proof.
* Write out the words "Inductive Step" and state, and clearly identify, the inductive hypothesis, in the form "Assume that $P(k)$ is true for an arbitrary fixed integer $k \geq b$."
* State what needs to be proved under the assumption that the inductive hypothesis is true. That is, write out what $P(k + 1)$ says.
* Prove the statement $P(k + 1)$ making use of the assumption $P(k)$.
  (Generally, this is the most difficult part of a mathematical induction proof.
  Decide on the most promising proof strategy and look ahead to see how to use the induction hypothesis to build your proof of the inductive step. Also, be sure that your proof is valid for all integers $k$ with $k \geq b$, taking care that the proof works for small values of $k$, including $k = b$.)
* Clearly identify the conclusion of the inductive step, such as by saying "This completes the inductive step."
* After completing the basis step and the inductive step, state the conclusion, namely, "By mathematical induction, $P(n)$ is true for all integers $n$ with $n \geq b$".

## Strong Induction and Well-Ordering
#### Strong Induction
Strong induction is sometimes called the **second principle of mathematical induction** or **complete induction**. When the terminology "complete induction" is used, the principle of mathematical induction is called **incomplete induction**.
In a proof by strong induction, the inductive step shows that if $P(j)$ is true for all positive integers $j$ not exceeding $k$, then $P(k + 1)$ is true. That is, for the inductive hypothesis we assume that $P(j)$ is true for $j = 1, 2, \ldots, k$.

* **STRONG INDUCTION** :
  To prove that $P(n)$ is true for all positive integers $n$, where $P(n)$ is a propositional function, we complete two steps:
	* **Basis Step** : We verify that the proposition $P(1)$ is true.
	* **Inductive Step** : We show that the conditional statement $[P(1) \land P(2) \land \ldots \land P(k)] \rightarrow P(k + 1)$ is true for all positive integers $k$.

#### Using Strong Induction in Computational Geometry
A **polygon** is a closed geometric figure consisting of a sequence of line segments $s_1, s_2, \ldots, s_n,$ called **sides**. Each pair of consecutive sides, $s_i$ and $s_{i+1}$, $i = 1, 2, \ldots, n − 1,$ as well as the last side $s_n$ and the first side $s_1$, of the polygon meet at a common endpoint, called a **vertex**.
A polygon is called **simple** if no two nonconsecutive sides intersect. Every simple polygon divides the plane into two regions: its **interior**, consisting of the points inside the curve, and its **exterior**, consisting of the points outside the curve. A polygon is called **convex** if every line segment connecting, two points in the interior of the polygon lies entirely inside the polygon. (A polygon that is not convex is said to be **non-convex**.)
A **diagonal** of a simple polygon is a line segment connecting two nonconsecutive vertices of the polygon, and a diagonal is called an **interior diagonal** if it lies entirely inside the polygon, except for its endpoints.

One of the most basic operations of computational geometry involves dividing a simple polygon into triangles by adding non-intersecting diagonals. This process is called **triangulation**.

* **Lemma** :
  Every simple polygon with at least four sides has an interior diagonal.
* **Theorem** :
  A simple polygon with $n$ sides, where $n$ is an integer with $n \geq 3$, can be triangulated into $n - 2$ triangles.
  
  **Proof** :
  Let $T(n)$ be the statement that every simple polygon with $n$ sides can be triangulated into $n - 2$ triangles.
	* **Basic Step** :
	  $T(3)$ is true because a simple polygon with three sides is a triangle. We do not need to add any diagonals to triangulate a triangle; it is already triangulated into one triangle, itself.
	* **Inductive Step** :
	  For the inductive hypothesis, we assume that $T(j)$ is true for all integers $j$ with $3 \leq j \leq k$. That is, we assume that we can triangulate a simple polygon with $j$ sides into $j - 2$ triangles whenever $3 \leq j \leq k$.
	  To complete the inductive step, we must show that when we assume the inductive hypothesis, $P(k + 1)$ is true, that is, that every simple polygon with $k + 1$ sides can be triangulated into $(k + 1) - 2 = k - 1$ triangles.
	  So, suppose that we have a simple polygon $P$ with $k + 1$ sides. Because $k + 1 \geq 4$, Lemma tells us that $P$ has an interior diagonal $ab$. Now, $ab$ splits $P$ into two simple polygons $Q$, with $s$ sides, and $R$, with $t$ sides. The sides of $Q$ and $R$ are the sides of $P$, together with the side $ab$, which is a side of both $Q$ and $R$.
	  Note that $3 \leq s \leq k$ and $3 \leq t \leq k$ because both $Q$ and $R$ have at least one fewer side than $P$ does (after all, each of these is formed from $P$ by deleting at least two sides and replacing these sides by the diagonal $ab$). Furthermore, the number of sides of $P$ is two less than the sum of the numbers of sides of $Q$ and the number of sides of R. That is, $k + 1 = s + t - 2$.
	  
	  We now use the inductive hypothesis. Because both $3 \leq s \leq k$ and $3 \leq t \leq k$, by the inductive hypothesis we can triangulate $Q$ and $R$ into $s - 2$ and $t - 2$ triangles, respectively. Next, note that these triangulations together produce a triangulation of $P$. (Each diagonal added to triangulate one of these smaller polygons is also a diagonal of $P$.) Consequently, we can triangulate $P$ into a total of $(s - 2) + (t - 2) = s + t - 4 = (k + 1) - 2$ triangles. 
	  This completes the proof by strong induction.
## Recursive Definitions and Structural Induction
Sometimes it is difficult to define an object explicitly. However, it may be easy to define this object in terms of itself. This process is called **recursion**.
#### Recursively Defined Functions
We use two steps to define a function with the set of non-negative integers as its domain:
* **Basis Step** : Specify the value of the function at zero.
* **Recursive Step** : Give a rule for finding its value at an integer from its values at smaller integers.

Such a definition is called a **recursive** or **inductive** definition.
* **Theorem** : Lamé's Theorem
  Let $a$ and $b$ be positive integers with $a \geq b$. Then the number of divisions used by the Euclidean algorithm to find gcd$(a, b)$ is less than or equal to five times the number of decimal digits in $b$.
#### Recursively Defined Sets and Structures
* **Definition** :
  The set $\Sigma$\* of **strings** over the alphabet $\Sigma$ is defined recursively by
	* **Basis Step** : $\lambda \in \Sigma$\* (where $\lambda$ is the empty string containing no symbols).
	* **Recursive Step** : If $w \in \Sigma$\* and $x \in \Sigma$, then $wx \in \Sigma$\* .
* **Definition** :
  Two strings can be combined via the operation of **concatenation**. Let $\Sigma$ be a set of symbols and $\Sigma$\* the set of strings formed from symbols in $\Sigma$. We can define the concatenation of two strings, denoted by $\cdot$, recursively as follows.
	* **Basis Step** : If $w \in \Sigma$\*, then $w \cdot \lambda = w$, where $\lambda$ is the empty string.
	* **Recursive Step** : If $w_1 \in \Sigma$\* and $w_2 \in \Sigma$\* and $x \in \Sigma$, then $w_1 \cdot (w_2 x) = (w_1 \cdot w_2)x$.

Another important use of recursive definitions is to define **well-formed formulae** of various types.
* **Well-Formed Formulae in Propositional Logic** :
  We can define the set of well-formed formulae in propositional logic involving $T, F$, propositional variables, and operators from the set $\{\lnot, \land, \lor, \rightarrow, \leftrightarrow\}$.
  * **Basis Step** : $T, F,$ and $s,$ where $s$ is a propositional variable, are well-formed formulae.
  * **Recursive Step** : If $E$ and $F$ are well-formed formulae, then $(\lnot E), (E \land F), (E \lor F), (E \rightarrow F),$ and $(E \leftrightarrow F)$ are well-formed formulae.
## Recursive Algorithms
* **Definition** :
  An algorithm is called **recursive** if it solves a problem by reducing it to an instance of the same problem with smaller input.

We will now see a recursive algorithm for computing $b^n$ mod $m$, where $b, n,$ and $m$ are integers with $m \geq 2, n \geq 0,$ and $1 \leq b < m$.

* **Algorithm** : Recursive Modular Exponentiation.
  **procedure** $mpower$($b, n, m$ : integers with $b > 0$ and $m \geq 2$, $n \geq 0$)
  if $n = 0$ then
  $\qquad$return 1
  else if $n$ is even then
  $\qquad$return $mpower(b, n/2, m)^2$ mod $m$
  else
  $\qquad$return ($mpower(b, \lfloor n/2 \rfloor, m)^2$ mod $m \cdot b$ mod $m$) mod $m$
  {output is $b^n$ mod $m$}
#### Recursion and Iteration
A recursive definition expresses the value of a function at a positive integer in terms of the values of the function at smaller integers. This means that we can devise a recursive algorithm to evaluate a recursively defined function at a positive integer.
Instead of successively reducing the computation to the evaluation of the function at smaller integers, we can start with the value of the function at one or more integers, the base cases, and successively apply the recursive definition to find the values of the function at successive larger integers. Such a procedure is called **iterative**.

* **Algorithm** : A Recursive Algorithm for Fibonacci Numbers.
  **procedure** $fibonacci$($n$ : nonnegative integer)
  if $n = 0$ then return $0$
  else if $n = 1$ then return $1$
  else return $fibonacci(n - 1) + fibonacci(n - 2)$
  {output is $fibonacci(n)$}
#### The Merge Sort
A merge sort begins by splitting the list into individual elements by successively splitting lists in two. Sorting is done by successively merging pairs of lists. At the first stage, pairs of individual elements are merged into lists of length two in increasing order. Then successive merges of pairs of lists are performed until the entire list is put into increasing order.
In general, a merge sort proceeds by iteratively splitting lists into two sublists of equal length (or where one sublist has one more element than the other) until each sublist contains one element. This succession of sublists can be represented by a balanced binary tree. The procedure continues by successively merging pairs of lists, where both lists are in increasing order, into a larger list with elements in increasing order, until the original list is put into increasing order. The succession of merged lists can be represented by a balanced binary tree.

* **Algorithm** : A Recursive Merge Sort.
  **procedure** $mergesort(L = a_1, \ldots, a_n)$
  if $n > 1$ then
  $\qquad m := \lfloor n/2 \rfloor$
  $\qquad L_1 := a_1, a_2, \ldots, a_m$
  $\qquad L_2 := a_{m + 1}, a_{m + 2}, \ldots, a_n$
  $\qquad L := merge(mergesort(L_1), mergesort(L_2))$
  {$L$ is now sorted into elements in non-decreasing order}

* **Algorithm** : Merging Two Lists.
  **procedure** $merge$($L_1, L_2$ : sorted lists)
  $L :=$ empty list
  while $L_1$ and $L_2$ are both nonempty
  $\quad$remove smaller of first elements of$L_1$ and $L_2$ from its list; put it at the right end of $L$
  $\quad$if this removal makes one list empty then remove all elements from the other list and
   $\quad$append them to L
  return $L\{L$ is the merged list with elements in increasing order$\}$

* **Lemma** :
  Two sorted lists with $m$ elements and $n$ elements can be merged into a sorted list using no more than $m + n - 1$ comparisons.
* **Theorem** :
  The number of comparisons needed to merge sort a list with $n$ elements is $O(n \log n)$.

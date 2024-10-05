# Algorithms
## Algorithms

An **algorithm** is a finite sequence of precise instructions for performing a computation or for solving a problem. A pseudocode description of the algorithm for finding the maximum element in a finite sequence follows.
* **Algorithm** : Finding the maximum element in a finite sequence.
* **procedure** max($a_1, \ldots, a_n$ : integers)
	max $:=$ $a_1$
	for $i := 2$ to $n$
	$\qquad$ if max $< a_i$ then max $:= a_i$
	return max
#### Searching Algorithms
The general searching problem can be described as follows: 
Locate an element $x$ in a list of distinct elements $a_1, \ldots, a_n,$ or determine that it is not in the list. The solution to this search problem is the location of the term in the list that equals $x$ (that is, $i$ is the solution if $x = a_i$) and is $0$ if $x$ is not in the list.

###### The Linear Search
The first searching algorithm that we will present is called the linear search algorithm.
* **Algorithm** : The Linear Search Algorithm.
  **procedure** linear search($x$ : integer, $a_1, \ldots, a_n$ : distinct integers)
  $i := 1$
  while ($i \le n$ and $x \ne a_i$)
  $\qquad i := i + 1$
  if $i \le n$ then location $:= i$
  else location $:= 0$
  return location

###### The Binary Search
We will now consider another searching algorithm. This algorithm can be used when the list has terms occurring in order of increasing size. This second searching algorithm is called the binary search algorithm.
* **Algorithm** : The Binary Search Algorithm.
  **procedure** binary search($x$ : integer, $a_1, \ldots, a_n$ : distinct integers)
  $i := 1$ \[Left\]
  $j := n$ \[Right\]
  while ($i < j$)
  $\qquad m := \lfloor (i + j) / 2 \rfloor$
  $\qquad$if $x > a_m$ then $i:= m + 1$
  $\qquad$else $j := m$
  if $x = a_i$ then location $:= 1$
  else location $:= 0$
  return location

#### Sorting
Suppose that we have a way to order elements of the set. Sorting is putting these elements into a list in which the elements are in increasing order. For instance, sorting the list 7, 2, 1, 4, 5, 9 produces the list 1, 2, 4, 5, 7, 9. Sorting the list d, h, c, a, f (using alphabetical order) produces the list a, c, d, f, h.
###### The Bubble Sort
The bubble sort is one of the simplest sorting algorithms. It puts a list into increasing order by successively comparing adjacent elements, interchanging them if they are in the wrong order.
* **Algorithm** : The Bubble Sort.
  **procedure** bubble sort($a_1, \ldots, a_n$ : real numbers with $n \ge 2$)
  for $i := 1$ to $n - 1$
  $\qquad$for $i := 1$ to $n - i$
  $\qquad \qquad$if $a_j > a_{j + 1}$ then interchange $a_j$ and $a_{j + 1}$
  {$a_1, \ldots, a_n$ $ is in increasing order}

###### The Insertion Sort
In general, in the $j$th step of the insertion sort, the $j$th element of the list is inserted into the correct position in the list of the previously sorted $j - 1$ elements.
To insert the $j$th element in the list, a linear search technique is used; the $j$th element is successively compared with the already sorted $j - 1$ elements at the start of the list until the first element that is not less than this element is found or until it has been compared with all $j - 1$ elements; the $j$th element is inserted in the correct position so that the first $j$ elements are sorted. The algorithm continues until the last element is placed in the correct position relative to the already sorted list of the first $n - 1$ elements.
* **Algorithm**: The Insertion Sort.
  **procedure** insertion sort($a_1, \ldots, a_n$ : real numbers with $n \ge 2$)
  for $j := 2$ to $n$
  $\qquad i := 1$
  $\qquad$while $a_j > a$  
  $\qquad \qquad i := i + 1$
  $\qquad m := a_j$
  $\qquad$for $k := 0$ to $j - i - 1$  
  $\qquad \qquad a_{j - k} := a_{j - k - 1}$
  $\qquad a_i := m$
  {$a_1, \ldots, a_n$ $ is in increasing order}

## The Growth of Functions

Big-$O$ notation is used extensively to estimate the number of operations an algorithm uses as its input grows. With the help of this notation, we can determine whether it is practical to use a particular algorithm to solve a problem as the size of the input increases. Furthermore, using big-$O$ notation, we can compare two algorithms to determine which is more efficient as the size of the input grows.
#### Big-$O$ Notation
Let $f$ and $g$ be functions from the set of integers or the set of real numbers to the set of real numbers. We say that $f(x)$ is $O(g(x))$ if there are constants $C$ and $k$ such that $$\begin{align*}
& |f(x)| \leq C|g(x)| &
\end{align*}$$whenever $x > k$.

#### Big-$O$ Estimates for Some Important Functions

Polynomials can often be used to estimate the growth of functions. Instead of analyzing the growth of polynomials each time they occur, we would like a result that can always be used to estimate the growth of a polynomial.
* **Theorem** :
  Let $f(x) = a_{n}x^{n} + a_{n-1}x^{n-1} + \ldots + a_1x + a_0,$ where $a_0, a_1, \ldots, a_{n-1},$ an are real numbers. Then $f(x)$ is $O(x^n)$.

We now give some useful facts that help us determine whether big-$O$ relationships hold between pairs of functions when each of the functions is a power of a logarithm, a power, or an exponential function of the form $b^n$ where $b > 1$.
* If $f(n)$ is a polynomial of degree $d$ or less, then $f(n)$ is $O(n^d)$, but the reverse of this relationship does not hold.
  If $d > c > 1 ,$ then
  $\quad n^c$ is $O(n^d) ,$ but $n^d$ is not $O(n^c)$.
* Every positive power of the logarithm of $n$ to the base $b$, where $b > 1$, is big-$O$ of every positive power of $n$, but the reverse relationship never holds. 
  Whenever $b > 1$ and $c$ and $d$ are positive, we have
  $\quad (\log_b n)^c$ is $O(n^d)$, but $n^d$ is not $(O(\log_b n)^c)$.
* Every power of $n$ is big-$O$ of every exponential function of $n$ with a base that is greater than one, but the reverse relationship never holds.
  Whenever $b > 1$ and $d$ is positive, we have
  $\quad n^d$ is $O(b^n) ,$ but $b^n$ is not $O(n^d)$.
* If we have two exponential functions with different bases greater than one, one of these functions is big-$O$ of the other if and only if its base is smaller or equal.
  When $c > b > 1$, we have
  $\quad b^n$ is $O(c^n) ,$ but $c^n$ is not $O(b^n)$.
* If $c > 1$, we have
  $\quad c^n$ is $O(n!) ,$ but $n!$ is not $O(c^n)$.

#### The Growth of Combinations of Functions
Many algorithms are made up of two or more separate subprocedures. The number of steps used by a computer to solve a problem with input of a specified size using such an algorithm is the sum of the number of steps used by these subprocedures. To give a big-$O$ estimate for the number of steps needed, it is necessary to find big-$O$ estimates for the number of steps used by each subprocedure and then combine these estimates.
* Suppose that $f_1(x)$ is $O(g_1(x))$ and that $f_2(x)$ is $O(g_2(x))$. Then $(f_1 + f_2)(x)$ is $O(g(x))$, where $g(x) = (max(|g_1(x)|, |g_2(x)|)$ for all $x$.
* Suppose that $f_1(x)$ is $O(g_1(x))$ and $f_2(x)$ is $O(g_2(x))$. Then $(f_1f_2)(x)$ is $O(g_1(x)g_2(x))$.
#### Big-Omega and Big-Theta Notation
Big-$O$ notation is used extensively to describe the growth of functions, but it has limitations.
In particular, when $f(x)$ is $O(g(x))$, we have an upper bound, in terms of $g(x)$, for the size of $f(x)$ for large values of $x$. However, big-$O$ notation does not provide a lower bound for the size of $f(x)$ for large $x$. For this, we use big-Omega (big-$\Omega$) notation. When we want to give both an upper and a lower bound on the size of a function $f(x)$, relative to a reference function $g(x)$, we use big-Theta (big-$\Theta$) notation.

* Let $f$ and $g$ be functions from the set of integers or the set of real numbers to the set of real numbers. We say that $f(x)$ is $\Omega(g(x))$ if there are constants $C$ and $k$ with $C$ positive such that $|f(x)| \ge C|g(x)|$ whenever $x > k$.

## Complexity of Algorithms
Questions such as these involve the computational complexity of the algorithm. An analysis of the time required to solve a problem of a particular size involves the time complexity of the algorithm. An analysis of the computer memory required involves the space complexity of the algorithm. Considerations of the time and space complexity of an algorithm are essential when algorithms are implemented. It is important to know whether an algorithm will produce an answer in a microsecond, a minute, or a billion years.
#### Time Complexity
The time complexity of an algorithm can be expressed in terms of the number of operations used by the algorithm when the input has a particular size. The operations used to measure time complexity can be the comparison of integers, the addition of integers, the multiplication of integers, the division of integers, or any other basic operation.

###### Worst-Case Complexity
By the worst-case performance of an algorithm, we mean the largest number of operations needed to solve the given problem using this algorithm on input of specified size. 
Worst-case analysis tells us how many operations an algorithm requires to guarantee that it will produce a solution.

###### Average-Case Complexity
Another important type of complexity analysis, besides worst-case analysis, is called average-case analysis. The average number of operations used to solve the problem over all possible inputs of a given size is found in this type of analysis. Average-case time complexity analysis is usually much more complicated than worst-case.


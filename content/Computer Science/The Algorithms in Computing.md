Informally, an algorithm is any well-defined computational procedure that takes some value, or set of values, as input and produces some value, or set of values, as output in a finite amount of time. An algorithm is thus a sequence of computational steps that transform the input into the output.
An algorithm for a computational problem is correct if, for every problem instance provided as input, it halts $-$ finishes its computing in finite time and outputs the correct solution to the problem instance. A correct algorithm solves the given computational problem.

This book also presents several data structures. A data structure is a way to store and organize data in order to facilitate access and modifications. Using the appropriate data structure or structures is an important part of algorithm design.

To express an algorithm, we will use Pseudocode. What separates pseudocode from real code is that in pseudocode, we employ whatever expressive method is most clear and concise to specify a given algorithm. Another difference between pseudocode and real code is that pseudocode often ignores aspects of software engineering$-$such as data abstraction, modularity, and error handling$-$in order to convey the essence of the algorithm more concisely.
## Insertion Sort

Our first algorithm, **insertion sort**, solves the sorting problem :
* **Input**: A sequence of $n$ numbers $\braket{a_1, a_2, \ldots, a_n}$.
* **Output**: A permutation (reordering) $\braket{a'_1, a'_2, \ldots, a'_n}$ of the input sequence such that $\qquad \quad \quad a'_1 \leqslant a'_2 \leqslant \ldots \leqslant a'_n$.

The numbers to be sorted are also known as the **keys**. When we want to sort numbers, it's often because they are the keys associated with other data, which we call **satellite data**. Together, a *key* and *satellite data* form a **record**.

The pseudocode for insertion sort is given as the procedure **Insertion-Sort**. 
It takes two parameters: an array $A$ containing the values to be sorted and the number $n$ of values of sort. The values occupy positions $A[1]$ through $A[n]$ of the array, which we denote by $A[1:n]$. When the Insertion-Sort procedure is finished, array $A[1:n]$ contains the original values, but in sorted order.

* **Algorithm**: The Insertion Sort.
  **procedure** Insertion-sort($A$: real numbers with size $n \geqslant 2$)
  for $i := 2$ to $n$
  $\qquad key := A[i]$
  $\qquad$$j = i - 1$
  $\qquad$while $j > 0$ and $A[j] > key$  
  $\qquad \qquad A[j + 1] := A[j]$
  $\qquad \qquad j := j - 1$
  $\qquad A[j + 1] := key$
  
  **Output**: {$a_1, \ldots, a_n$ is in increasing order}

The index $i$ indicates the "current key" being inserted into the final array. At the beginning of each iteration of the for loop, which is indexed by $i$, the subarray (a contiguous portion of the array) consisting of elements $A[1: i - 1]$ constitutes the currently sorted array, and the remaining subarray $A[i + 1 : n]$ corresponds to the elements remaining in the given array. In fact, elements $A[1: i - 1]$ are the elements originally in positions $1$ through $i - 1$, but now in sorted order. We state these properties of $A[1: i - 1]$ formally as a **loop invariant**: $$\begin{align*}
& \text{At the start of each iteration of the for loop, the subarray A[1 : i - 1] }&  \\ 
& \text{consists of the elements originally in A[1 : i - 1], but in sorted order.} &
\end{align*}$$
Loop invariants help us understand why an algorithm is correct. When you're using a loop invariant, you need to show three things:

* **Initialization**: It is true prior to the first iteration of the loop.
* **Maintenance**: If it is true before an iteration of the loop, it remains true before the next iteration.
* **Termination**: The loop terminates, and when it terminates, the invariant$-$usually along with the reason that the loop terminated$-$gives us a useful property that helps show that the algorithm is correct.

A loop-invariant proof is a form of mathematical induction, where to prove that a property holds, you prove a base case and an inductive step.

Let's see how these properties hold for insertion sort.
* **Initialization**:
  We start by showing that the loop invariant holds before the first loop iteration, when $i = 2$. The subarray $A[1 : i - 1]$ consists of just the single element $A[1]$, which is in fact the original element in $A[1]$. Moreover, this subarray is sorted.
* **Maintenance**:
  Next, we tackle the second property: showing that each iteration  Next,  maintains the loop invariant. Informally, the body of the for loop works by moving the values in $A[i - 1]$, $A[i - 2]$, $A[i - 3]$, and so on by one position to the right until it finds the proper position for $A[i]$, at which point it inserts the value of $A[i]$. The subarray $A[1 : i]$ then consists of the elements originally in $A[1 : i]$, but in sorted order. **Incrementing** $i$ for the next iteration of the for loop then preserves the loop invariant.
* **Termination**:
  Finally, we examine loop termination. The loop variable $i$ starts at $2$ and increases by $1$ in each iteration. Once $i$'s value exceeds $n$, the loop terminates. So, the loop terminates once $i$ equals $n + 1$. Substituting $n + 1$ for $i$ in the wording of the loop invariant yields that the subarray $A[1 : n]$ consists of the elements originally in $A[1 : n]$, but in sorted order. Hence, the algorithm is correct.

We typically organize compound data into **objects**, which are composed of **attributes**. We access a particular attribute using the syntax: the object name, followed by a dot, followed by the attribute name.

## Analyzing Algorithms

Analyzing an algorithm has come to mean predicting the resources that the algorithm requires. You might consider resources such as memory, communication bandwidth, or energy consumption. Most often, however, you'll want to measure computational time.

Most of this book assumes a generic one-processor, random-access machine (RAM) model of computation as the implementation technology, with the understanding that algorithms are implemented as computer programs. In the RAM model, instructions execute one after another, with no concurrent operations. The RAM model assumes that each instruction takes the same amount of time as any other instruction and that each data access$-$using the value of a variable or storing into a variable$-$takes the same amount of time as any other data access.

#### Analysis of Insertion Sort

*How long does the Insertion-Sort procedure take? How do we analyze insertion sort?*

Even though the running time can depend on many features of the input, we'll focus on the one that has been shown to have the greatest effect, namely the *size of the input*, and describe the running time of a program as a function of the size of its input.

The best notion for **input size** depends on the problem being studied. For many problems, such as sorting or computing discrete Fourier transforms, the most natural measure is the number of items in the input. For many other problems, such as multiplying two integers, the best measure of input size is the total number of bits needed to represent the input in ordinary binary notation.
The **running time** of an algorithm on a particular input is the number of instructions and data accesses executed.

Now, let's analyze the Insertion-Sort procedure. To analyze the Insertion-Sort procedure, let's view it with the time cost of each statement and the number of times each statement is executed. 
For each $i = 2, 3, \ldots, n,$ let $t_i$ denote the number of times the while loop test is executed for that value of $i$. When a for or while loop exits in the usual way$-$because the test in the loop header comes up FALSE$-$the test is executed one time more than the loop body. Because comments are not executable statements, assume that they take no time.
$$\begin{align*}
& for \space i := 2 \space to \space n & c_1 \qquad n \quad \space \space \space \\
& \qquad key := A[i] & c_2 \qquad n - 1 \\
& \qquad j = i - 1 & c_3 \qquad n - 1 \\
& \qquad  while \space j > 0 \space and \space A[j] > key & c_4 \qquad \scriptstyle \sum_{i = 2}^{n} t_i \\  
& \qquad \qquad A[j + 1] := A[j] & \quad c_5 \space \space \space \scriptstyle \sum_{i = 2}^{n} (t_i - 1) \\
& \qquad \qquad j := j - 1 & c_6 \space \space \space \scriptstyle \sum_{i = 2}^{n} (t_i - 1) \\
& \qquad A[j + 1] := key & c_7 \qquad n - 1 \\
\end{align*}$$
The running time of the algorithm is the sum of running times for each statement executed. We denote the running time of an algorithm on an input of size $n$ by $T(n)$. To compute $T(n)$, the running time of Insertion-Sort on an input of $n$ values, we sum the products of the cost and times columns, obtaining $$\begin{align*}
& T(n) = c_1n + c_2(n - 1) + c_3(n - 1) + c_4 \sum_{i = 2}^{n} t_i + c_5 \sum_{i = 2}^{n} (t_i -1) + c_6 \sum_{i = 2}^{n} (t_i -1) + c_7(n - 1). &
\end{align*}$$
Even for inputs of a given size, an algorithm's running time may depend on which input of that size is given. For example, in Insertion-Sort, the **best case** occurs when the array is already sorted. Therefore, we have that $t_i = 1$ for $i = 2, 3, \ldots, n,$ and the best-case running time is given by $$\begin{align*}
& T(n) = c_1n + c_2(n - 1) + c_3(n - 1) + c_4(n - 1) + c_7(n - 1). & \\
& T(n) = (c_1 + c_2 + c_3 + c_4 + + c_7) \, n - (c_2 + c_3 + c_4 + + c_7).&
\end{align*}$$We can express this running time as $an + b$ for constants $a$ and $b$ that depend on the statement costs $c_k$. The running time is thus a **linear function** of $n$.

The **worst case** arises when the array is in reverse sorted order. The procedure must compare each element $A[i]$ with each element in the entire sorted subarray $A[1 : i - 1]$, and so $t_i = i$ for $i = 2, 3, \ldots, n,$. In the worst case, the running time of Insertion-Sort is $$\begin{align*}
& T(n) = c_1n + c_2(n - 1) + c_3(n - 1) + c_4 \left( \frac{n(n - 1)}{2} - 1 \right) +  (c_5  + c_6) \left( \frac{n(n - 1)}{2} \right) + c_7(n - 1). &
\end{align*}$$
We can express this worst-case running time as $an^2 + bn + c$ for constants $a, b,$ and $c$ that again depend on the statement costs $c_k$. The running time is thus a **quadratic function** of $n$.
The worst-case running time of an algorithm gives an upper bound on the running time for any input. If you know it, then you have a guarantee that the algorithm never takes any longer.

#### Order of Growth

Let's now make one simplifying abstraction: it is the **rate of growth**, or **order of growth**, of the running time that really interests us. We therefore consider only the leading term of a formula ($an^2$), since the lower-order terms are relatively insignificant for large values of $n$. We also ignore the leading term's constant coefficient, since constant factors are less significant than the rate of growth in determining computational efficiency for large inputs.

To highlight the order of growth of the running time, we have a special notation that uses the Greek letter $\Theta$ (theta). We write that insertion sort has a worst-case running time of $\Theta (n^2)$. For now, think of ‚ $\Theta$-notation as saying "roughly proportional when $n$ is large", so that $\Theta (n^2)$ means "roughly proportional to $n^2$ when $n$ is large".

## Designing Algorithms

This section examines another design method, known as "**divide-and-conquer**".
#### The Divide-and-Conquer Method

Let's look into the algorithms with recursion. These algorithms typically follow the divide-and-conquer method: they break the problem into several subproblems that are similar to the original problem but smaller in size, solve the subproblems recursively, and then combine these solutions to create a solution to the original problem.

In this method, if the problem is small enough$-$**the base case**$-$you just solve it directly without recursing. Otherwise$-$**the recursive case**$-$you perform three characteristic steps:

* **Divide** the problem into one or more subproblems that are smaller instances of the same problem.
* **Conquer** the subproblems by solving them recursively.
* **Combine** the subproblem solutions to form a solution to the original problem.

The **merge sort** algorithm closely follows the divide-and-conquer method. In each step, it sorts a subarray $A[p : r]$, starting with the entire array $A[1 : n]$ and recursing down to smaller and smaller subarrays. Here is how merge sort operates:

* Divide the subarray $A [p : r]$ to be sorted into two adjacent subarrays, each of half the size. To do so, compute the midpoint $q$ of $A [p : r]$ (taking the average of $p$ and $r$), and divide $A [p : r]$ into subarrays $A [p : q]$ and $A [q + 1 : r]$.
* Conquer by sorting each of the two subarrays $A [p : q]$ and $A [q + 1 : r]$ recursively using merge sort.
* Combine by merging the two sorted subarrays $A [p : q]$ and $A [q + 1 : r]$ back into $A [p : r]$, producing the sorted answer.

The recursion "bottoms out"$-$it reaches the base case$-$when the subarray $A [p : r]$ to be sorted has just $1$ element, that is, when $p$ equals $r$.

* **Algorithm**: The Merge Sort
  **procedure** merge-sort ($A$: real numbers with indices $p$: start and $r$: end)
  if $p \geqslant r$
  $\qquad$$return$
  $q = \lfloor (p + q) / 2 \rfloor$
  merge-sort $(A, p, q)$
  merge-sort $(A, q + 1, r)$
  Merge $(A, p, q, r)$
  
  **Output**: {$a_1, \ldots, a_n$ is in increasing order}

The merge operation is performed by the auxiliary procedure $Merge \, (A, p, q, r)$, where $A$ is an array and $p, q,$ and $r$ are indices into the array such that $p \leqslant q < r$. The procedure assumes that the adjacent subarrays $A [p : q]$ and $A [q + 1 : r]$ were already sorted. It **merges** the two sorted subarrays to form a single sorted subarray that replaces the current subarray $A [p : r]$.
With each basic step taking constant time and the total number of basic steps being between $n/2$ and $n$, we can say that merging takes time roughly proportional to $n$. That is, merging takes $\Theta(n)$ time.

* **procedure** Merge ($A$: real numbers with indices $p$: start, $q$: mid and $r$: end)
  $n_L = q - p + 1$
  $n_R = r - q$
  let $L[0 : n_L - 1]$ and $R[0 : n_R - 1]$ be new arrays
  for $i = 0$ to $n_L - 1$
  $\qquad$$L[i] = A[p + i]$
  for $j = 0$ to $n_R - 1$
  $\qquad$$R[j] = A[q + j + 1]$
  $i = 0$
  $j = 0$
  $k = p$
  
  while $i < n_L$ and $j < n_R$
  $\qquad$if $L[i] \leqslant R[j]$
  $\qquad \qquad$$A[k] = L[i]$
  $\qquad \qquad$$i = i + 1$
  $\qquad$else 
  $\qquad \qquad$$A[k] = R[j]$
  $\qquad \qquad$$j = j + 1$
  $\qquad$$k = k + 1$
  
  while $i < n_L$
  $\qquad$$A[k] = L[i]$
  $\qquad$$i = i + 1$
  $\qquad$$k = k + 1$
  while $j < n_R$
  $\qquad$$A[k] = R[j]$
  $\qquad$$j = j + 1$
  $\qquad$$k = k + 1$
  
  **Output**: $\{ A[p : r] \}$

In detail, the Merge procedure works as follows. It copies the two subarrays $A [p : q]$ and $A [q + 1 : r]$ into temporary arrays $L$ and $R$ ("left" and "right"), and then it merges the values in $L$ and $R$ back into $A [p : r]$. Line $1$ and $2$ compute the lengths $n_L$ and $n_R$ of the subarrays $A [p : q]$ and $A [q + 1 : r]$, respectively. Then line $3$ creates arrays $L [0 : n_L - 1]$ and $R [0 : n_R - 1]$ with respective lengths $n_L$ and $n_R$ . The for loop of lines $4 - 5$ copies the subarray $A [p : q]$ into $L$, and the for loop of lines $6 - 7$ copies the subarray $A [q + 1 : r]$ into $R$.

*Lines $8 - 18$, perform the basic steps.*
The while loop of lines $12 - 18$ repeatedly identifies the smallest value in $L$ and $R$ that has yet to be copied back into $A [p : r]$ and copies it back in. The index $k$ gives the position of $A$ that is being filled in, and the indices $i$ and $j$ give the positions in $L$ and $R$, respectively, of the smallest remaining values. Eventually, either all of $L$ or all of $R$ is copied back into $A [p : r],$ and this loop terminates.

If the loop terminates because all of $R$ has been copied back, that is, because $j$ equals $n_R$, then $i$ is still less than $n_L$, so that some of $L$ has yet to be copied back, and these values are the greatest in both $L$ and $R$. In this case, the while loop of lines $20 - 23$ copies these remaining values of $L$ into the last few positions of $A [p : r]$.
Because $j$ equals $n_R$, the while loop of lines $24 - 27$ iterates $0$ times. If instead the while loop of lines $12 - 18$ terminates because $i$ equals $n_L$, then all of $L$ has already been copied back into $A [p : r]$, and the while loop of lines $24 - 27$ copies the remaining values of $R$ back into the end of $A [p : r]$.

#### Analyzing Divide-and-Conquer Algorithms

When an algorithm contains a recursive call, you can often describe its running time by a **recurrence equation** or **recurrence**, which describes the overall running time on a problem of size $n$ in terms of the running time of the same algorithm on smaller inputs.

As we did for insertion sort, let $T(n)$ be the worst-case running time on a problem of size $n$. If the problem size is small enough, say $n < n_0$ for some constant $n_0 > 0,$ the straightforward solution takes constant time, which we write as $\Theta(1)$.
Suppose that the division of the problem yields a subproblems, each with size $n / b$, that is, $1/b$ the size of the original. For merge sort, both $a$ and $b$ are $2$. It takes $T(n/b)$ time to solve one subproblem of size $n/b$, and so it takes $aT(n/b)$ time to solve all $a$ of them. If it takes $D(n)$ time to divide the problem into subproblems and $C(n)$ time to combine the solutions to the subproblems into the solution to the original problem, we get the recurrence $$\begin{align*}
& T(n) = \begin{cases} \Theta(1) \qquad \qquad \qquad \space \qquad \qquad \text{if} \space n < n_0, \\ D(n) + a T(n / b) + C(n) \qquad \text{otherwise}. \end{cases} &
\end{align*}$$
Sometimes, the $n/b$ size of the divide step isn't an integer. For example, the Merge-Sort procedure divides a problem of size $n$ into subproblems of sizes $\lceil n/2 \rfloor$ and $\lfloor n/2 \rfloor$. Since the difference between $\lceil n/2 \rfloor$ and $\lfloor n/2 \rfloor$ is at most $1$, which for large $n$ is much smaller than the effect of dividing $n$ by $2$, we'll just call them both size $n/2$.
Another convention we'll adopt is to omit a statement of the base cases of the recurrence. The reason is that the base cases are pretty much always $T(n) = \Theta(1)$ if $n < n_0$ for some constant $n_0 > 0$. That's because the running time of an algorithm on an input of constant size is constant.
###### Analysis of Merge-Sort

Let's set up the recurrence for $T(n)$, the worst-case running time of merge sort on $n$ numbers:
* **Divide**: The divide step just computes the middle of the subarray, which takes constant time. Thus, $D(n) = \Theta(1)$.
* **Conquer**: Recursively solving two subproblems, each of size $n/2$, contributes $2T(n/2)$ to the running time.
* **Combine**: Since the Merge procedure on an $n$-element subarray takes $\Theta(n)$ time, we have $C(n) = \Theta(n)$.

Adding $\Theta(n)$ to the $2T (n/2)$ term from the conquer step gives the recurrence for the worst case running time $T(n)$ of merge sort: $$\begin{align*}
& T(n) = 2 T(n / 2) + \Theta(n). &
\end{align*}$$
So, by Master-Theorem, $T(n) = \Theta(n \lg n)$.
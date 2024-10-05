# Amortized Analysis

In an *amortized analysis*, you average the time required to perform a sequence of data-structure operations over all the operations performed. Amortized analysis differs from average-case analysis in that probability is not involved. An amortized analysis guarantees the average performance of each operations in the worst case.
___
### Aggregate analysis
In *aggregate analysis*, you show that for all $n$, a sequence of $n$ operations takes $T(n)$ worst-case time in total. In the worst case, the average cost, or amortized cost per operation is therefor $T(n) /n$.  This amortized cost applies to each operation, even when there are several types of operations in the sequence.
##### Stack operations
Suppose we have a augmented stack and it consists of three operations each of which takes $O(1)$ time:
`PUSH(S, x)` pushes object $x$ onto stack $S$. 
`POP(S)` pops the top of stack $S$ and returns the popped object,
`MULTIPOP(S, k)` operation removes the k top objects of stack $S$, popping the entire stack if the stack contains the fewer than $k$ objects. 
`push` and `pop` runs in $O(1)$ time while `multipop` runs in linear time and has the cost of $\min\{ s,k \}$.

Let's analyze a sequence of $n$ `PUSH`, `POP` , and `MULTIPOP` operations on an initially empty stack. The worst-case cost of a MULTIPOP operation in the sequence in $O(n)$, since the stack size is at most $n$. which makes the sequence of $n$ operations costs $O(n^{2})$ . Although this analysis is correct, the $O(n^{2})$ result, which came from considering the worst-case cost of each operation individually , is not tight.

Aggregate analysis show that any sequence of $n$ `PUSH`, `POP`, and `MULTIPOP`  operation on an initially empty stack has an upper bound of its cost of $O(n^{2})$ . Because an object cannot be popped from the stack unless it was first pushed. 
Therefore, the no of times that `POP` can be called on a nonempty stack, including calls within `MULTIPOP`, is at most the no of `PUSH` operations, which is at most $n$

For any value of $n$, any sequence of $n$ of these operations take a total of $O(n)$ time. Averaging over the $n$ operations gives an average cost per operation of $O(n) / n = O(1)$. 
___
### The Accounting method
In the *accounting method* of amortized analysis, you assign differing charges to different operation, with some operations charged more or less than they actually cost. This amount that you charge an operation is its *amortized cost*. When an operation's amortized cost exceeds its actual cost, you assign the difference to specific object in the data structure as *credit*.

##### Stack operations
To illustrate the accounting method use stack example once more.

| Operation  | Actual Cost      | Amortized Cost |
| ---------- | ---------------- | -------------- |
| `PUSH`     | 1                | 2              |
| `POP`      | 1                | 0              |
| `MULTIPOP` | $\min\{ s, k \}$ | 0              |

where $k$ is the argument supplied to `MULTIPOP` and $s$ is the stack size when it is called.
The amortized cost of `MULTIPOP` is a constant $(0)$ , whereas the actual cost is variable and thus all three amortized cost are constant.

Let $1$ represent each unit of cost. At first the stack is empty. Upon pushing element onto the stack, use $1$ to pay the actual cost of the push, leaving a credit of $1$ . Place that $1$ of credit on top of the element on top of the stack. At any point in time, every element on stack has $1$ of credit on it.

The $1$ stored on the stack serves to prepay the cost of popping the element from the stack. A `POP` operation incurs no charge: pay the actual cost of popping a plate by taking the $1$ of credit off the element. Thus by charging the `PUSH` operation a little more we can consider `POP` operation as free. 

Moreover, the `MULTIPOP` also incurs no charge, since it's just repeated `POP` operations . Thus for any sequence of $n$ PUSH, POP, MULTIPOP , the total amortized cost is an upper bound on the total actual cost. which is $O(n)$.
___
### The potential method
Instead of representing prepaid work as credit stored with specific objects in the data structure, the *potential method* of amortized analysis represents the prepaid word as *potential energy*, which can be released to pay for future operations. 
The potential applies to the data structure as a whole rather than to specific objects within the data structure. 

Starting with an initial data structure $D_{0}$ a sequence of $n$ operations occurs. For each $i=1,2,\dots,n$ let $c_{i}$ be the actual cost of the $i$th operation and $D_{i}$ be the data structure that results after applying the $i$th operation to data structure $D_{i-1}$. 

A *potential function* $\Phi$  maps each data structure $D_{i}$ to a real number $\Phi(D_{i})$ which is the *potential* associated with $D_{i}$ . The amortized cost $\hat{c_{i}}$ of the $i$th operation with respect to potential function $\Phi$ is defined by
$$
\hat{c_{i}} = c_{i} + \Phi (D_{i}) - \Phi(D_{i-1})
$$
The amortized cost of each operation is therefore its actual cost plus potential due to the operation. 
Total amortized cost of $n$ operations is 
$$
\begin{align}
\sum_{i=1}^{n} \hat{c_{i}} &= \sum_{i=1}^{n} (c_{i}+\Phi(D_{i})) - \Phi(D_{i-1}) \\
&= \sum_{i=1}^{n} c_{i} + \Phi(D_{n}) - \Phi(D_{0})
\end{align}
$$
If the potential difference $\Phi(D_{i}) - \Phi(D_{i-1})$ of the $i$th operation is positive then the amortized cost $\hat{c_{i}}$ represents overcharge to the ith operation, and the potential of the data structure increases. 
If the potential difference is negative then the amortized cost represents an undercharge to the $i$th operation and the decrease in the potential pays for a actual cost of the operation.

##### Stack operations
To illustrate the potential method, we return once again to the example of stack operations `PUSH`, `POP`, and `MULTIPOP` . We define the potential function $\Phi$ on a stack to be the number of objects in the stack. The potential of the empty initia stack $D_{0}$ is $\Phi(D_{0}) = 0$ . Since the number of objects in the stack is never negative, the stack $D_{i}$ that stack $D_{i}$ that results after the ith operation has nonnegative potential and thus 
$\Phi(D_{i})\geq 0$
$\quad\qquad=\Phi(D_{0})$

The total amortized cost of $n$ operation with respect to $\Phi$ therefore represents an upper bound on the actual cost. 
If the ith operation on a stack containing $s$ objects is `push` operation, then the potential difference is 
$$
\begin{align}
\Phi(D_{i}) - \Phi(D_{i-1}) & = (s+1) - s \\
& =1
\end{align}
$$
The amortized cost of this `push` operation is
$$
\begin{align}
\hat{c_{i}} &= c_{i} + \Phi(D_{i}) - \Phi(D_{i-1}) \\
&= 1 + 1 \\
&= 2
\end{align}
$$
Suppose that the ith operation onthe stack of $s$ objects is `multipop` which causes $k'= \min\{ s,k \}$ objects to be popped off the stack. The actual cost of the operation is $k'$ and potential difference is 
$\Phi(D_{i})-\Phi(D_{i-1}) = -k'$
Thus, the amortized cost of the MULTIPOP operation is 
$$
\begin{align}
\hat{c_{i}} &= c_{i} + \Phi(D_{i}) - \Phi(D_{i-1}) \\
&= k'-k' \\
&= 0
\end{align}
$$
The amortized cost of each of the operations is $O(1)$ and thus the total amortized cost of a sequence of $n$ operations is $O(n)$. Since $\Phi(D_{i})  \geq \Phi(D_{0})$ , the total amortized cost of $n$ operations is an upper bound on the total actual cost . 
The worst-case cost of $n$ operations is therefore $O(n)$.
___
### The dynamic tables
The dynamic tables is kind of tables whose size can be increased on runtime.
The *load factor* $\alpha(T)$ of a nonempty table $T$ is defined as the number of items stored in the table divided by the size of the table. 

#### Table expansion


___
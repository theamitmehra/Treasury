Our first algorithm, insertion sort, solves the **sorting problem**. 
- **Input** : A sequence of $n$ numbers $\{a_1, a_2, ..., a_n\}$.
- **Output** : A permutation (reordering) $\{a'_1, a'_2, ..., a'_n\}$ of the input sequence such that $a'_1 \le a'_2 \le ... \le a'_n$ .
The number to be sorted are also known as the **keys**. Although the problem is conceptually about sorting a sequence, the input comes in the form of an array with $n$ elements. When we want to sort numbers, it's often because they are the keys associated with other data, which we call **satellite data**. Together a key and satellite data form a **record**.

**Insertion sort** is an efficient algorithm for sorting a small number of elements. insertion sort works the way you might sort a hand of playing cards. Start with an empty left hand and cards in a pile on the table. Pick up the first card in the pile and hold it with your left hand. Then, with you right hand, remove one card at a time from the pile and insert it into the correct position for a card by comparing it with each of the cards already in you left hand, starting at the right and moving left. As soon as you see a card in you left hand whose value is less than or equal to the card you're holding in you right hand, insert the card that all the cards in your right hand just to the right of this card in your left hand. If all the cards in you left hand have greater values then the card in your right hand, then place this card as the leftmost card in your left hand.
All the times, the cards held in your left hand are sorted, and these cards were originally the top cards of the pile on the table.

![[Sorting a hand of cards using insertion sort.png]]
$$
\text{Figure : Sorting a hand of cards using insertion sort}
$$
>[!tldr] $\text{INSERTION-SORT(A, n)}$
>for $i= 2$ to $n$
>$\qquad key = A[i]$  $\qquad \qquad$// insert $A[i]$ into the sorted subarray $A[1:i-1]$
>$j= i-1$
>while $j>0$ and $A[j] > key$
>$\qquad A[j+1] = A[j]$
>$\qquad j = j-1$
>$A[j+1] = key$

#### Loop invariants and the correctness of insertion sort : 
The index $i$ indicates the "current card" being inserted into the hand. At the beginning of each iteration of the **for** loop, which is index by i, the **subarray** (a contiguous portion of array) consisting of elements $A[1: i-1]$ constitutes the currently sorted hand, and the remaining subarray $A[i+1 : n]$ corresponds to the piles of cards still on the table. In facts, elements $A[1: i-1]$ are the elements originally in the positions $1$ through $i-1$ but now in sorted order. we state these properties of $A[1: i-1]$ formally as a **loop invariant**.

Loop invariants help us understand why an algorithm is correct. When you're using a loop invariant , you need to show three things:
- **Initialization** : It is true prior to the first iteration of the loop.
- **Maintenance** : If it is true before and iteration of the loop, it remains true before the next iteration.
- **Termination** : The loop terminates and when it does the invariant $-$ usually along with the reason that the loop terminated $-$ gives us a useful property that helps show that the algorithm is correct.

A loop-invariant proof is a form of mathematical induction, where to prove that a property holds, you prove a base case and an inductive step.
___
### Analyzing algorithms : 
Analyzing an algorithm has come to mean predicting the resources that a algorithm requires. This analysis is crucial for comparing algorithms. 
- **RAM (Random Access Machine) Model** - Used as an abstraction for algorithm analysis. It assumes each simple operation takes exactly one time step, also memory takes one time step.
- **Running Time** - It usually measured as a function of input of the input. It typically focuses on the worst-case scenario.
- **Big O Notation** - Describes the upper bound of the growth.

Let Analyze `INSERTION-SORT` using cost and time.

| INSERTION-SORT (A,n)                                               | COST  | TIME                     |
| ------------------------------------------------------------------ | ----- | ------------------------ |
| $For\space i = 2 \space to \space n$                               | $c_1$ | $n$                      |
| $\qquad key = A[i]$                                                | $c_2$ | $n-1$                    |
| $\qquad \text {// insert A[i] into the sorted subarray A[1: i-1]}$ | $0$   | $n-1$                    |
| $\qquad j = i -1$                                                  | $c_4$ | $n-1$                    |
| $\qquad While \space j > 0 \space and \space A[j] > key$           | $c_5$ | $\sum_{i=2} ^n t_i$      |
| $\qquad \qquad A[j+1] = A[j]$                                      | $c_6$ | $\sum_{i=2} ^n (t_i -1)$ |
| $\qquad \qquad j = j -1$                                           | $c_7$ | $\sum_{i=2} ^n (t_i-1)$  |
| $\qquad A[j+1] = key$                                              | $c_8$ | $n-1$                    |

$$
\begin{matrix}
T(n) = c_1n + c_2 (n-1) + c4(n-1) + c_5 \sum_{i=2}^n t_i + c_6 \sum_{i=2} ^ n (t_i - 1) \\
+ c_7 \sum_{i=2} ^ n (t_i - 1) + c_8 (n - 1).
\end{matrix}
$$
### Designing algorithms
#### The divide-and-conquer method

Many useful algorithms are recursive in structure : to solve a given problem they **recurse** (call themselves) one or more times to handle closely related subproblems. 
These algorithms typically follow the **divide-and-conquer** method: they break the problem into several subproblems that are similar to the original problem but smaller in size, solve the subproblems recursively and then combine these solution to create a solution to the original problem.
In divide and conquer method if the problem is small enough $-$ the **base case** $-$ you just solve it directly without recursing. Otherwise $-$ **the recursive case** $-$ you perform three characteristic steps:

**Divide** the problem into one or more subproblems.
**Conquer** the subproblems by solving them recursively.
**Combine** the subproblem solutions to form a solution to the original problem.
___
The **merge sort** algorithm follow the divide-and-conquer method. In each step it sort a subarray $A[p:r]$ starting with entire array $A[1:n]$ and recursing down to smaller and smaller subarrays.

Here is how merge sort operates :
- **Divide** the subarray $A[p:r]$ to be sorted into two adjacent subarrays, each of half the size. To do so, compute the midpoint $q$ of $A[p:r]$ (taking the average of $p$ and $r$), and divide $A[p:r]$ into subarrays $A[p:q]$ and $A[q+1: r]$
- **Conquer** by sorting each of the two subarrays $A[p:q]$ and $A[q+1: r]$ recursively using merge sort.
- **Combine** by merging the two sorted subarrays $A[p:q]$ and $A[q+1,: r]$ back into $A[p:r]$ , producing the sorted answer.
___

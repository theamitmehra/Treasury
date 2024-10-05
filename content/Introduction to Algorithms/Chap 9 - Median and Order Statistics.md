# Median and Order statistics
The $i$th *order statistics* of a set of n elements is the $i$th smallest element. For example the minimum of a set of element is the first order statistic $(i=1)$ and the maximum is the $n$th order statistic $(i=n)$ . A median is the halfway point of the set.
When $n$ is odd, the median is unique, occurring at $i= (n+1)/2$ . When $n$ is even, there are two medians, the lower median occurring at $i=n/2$ and upper median occurring at $i=n/2 + 1$ . Thus regardless of the parity of $n$ , medians occur at $i = \lfloor (n+1)/2 \rfloor$ and $i = \lceil (n+1)/2 \rceil$.
*Selection problem* is as follows :
**Input** : A set of $n$ distinct numbers and an integer $i$, with $1\le i\le n$.
**Output** : The element $x\in A$ that is larger than exactly $i-1$ other element of $A$.
___
### Minimum and maximum
Pseudocode for finding minimum element

>[!abstract]+ Minimum(A, n) 
>$min = A[1]$  
for $i = 2$ to $n$  
$\qquad$ if $min > A[i]$  
$\qquad \qquad$ $min = A[i]$  
return $min$  

___
### Selection in expected linear time

The general selection problem $-$ finding the $i$th order statistic for any value of i appears more difficult than the simple problem of finding a minimum. Yet surprisingly the asymptotic running time for both problems is the same: $\Theta (n)$. The algorithm $\text{RANDOMIZED-SELECT}$ is modeled after quick sort. But unlike quicksort which recursively processes both sides of the partition, this works only one side of partition. 
$\qquad$ This algorithm uses the procedure $\text{RANDOMIZED-PARTITION}$. Like $\text{RANDOMIZED-QUICKSORT}$ it is a randomized algorithm, since its behavior is determined in part by the output of  a random-number generator. The $\text{RANDOMIZED-SELECT}$ procedure returns the $i$th smallest element of the array $A[p:r]$ where $1\le i\le r-p+1$.

>[!tldr]+ RANDOMIZED-SELECT(A, p, r, i)
>if $p == r$  
>$\qquad$ return $A[p]\qquad \qquad // 1 \le i\le r-p+1\text{ when }p == r\text{means that }i = 1$   
>q = $\text {RANDOMIZED-PARTITION(A,p,r)}$  
>$k = q-p+1$
>if $i == k$
>$\qquad$ return $A[q]$
>else if $i < k$
>$\qquad$ return $\text{RANDOMIZED-SELECT}(A,p,q-1,i)$
>else 
>$\qquad$ return $\text{RANDOMIZED-SELECT}(A,q+1,r,i-k)$

___
> Linear-Time median algorithm : (https://youtu.be/n8cyxDtp9t4?feature=shared)
___

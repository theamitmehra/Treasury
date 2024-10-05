### Description of quicksort
Quicksort like merge sort, applies Divide-and-conquer method.
here is three-step process for sorting a subarray $A[p:r]$:

**Divide** by partitioning (rearranging) the array $A[p:r]$ into two (possibly empty) subarrays $A[p:q-1]$ (the low side) and $A[q+1: r]$ (the high side) such that each element in the low side of the partition is less than or equal to the pivot $A[q]$ , which is, in turn, less than or equal to each element in the high side. Compute the index $q$ of the pivot as part of this partitioning procedure. 

**Conquer** by calling quicksort recursively to sort each of the subarrays $A[p:q-1]$ and $A[q+1: r]$ ,

**Combine** by doing nothing: because the two subarrays are already sorted, no work is needed to combine them. All elements in $A[p:q-1]$ are sorted and less than or equal to $A[q]$, and all elements in $A[q+1:r]$ are sorted and greater than or equal to the pivot $A[q]$. The entire subarray  $A[p:r]$ cannot help but be sorted! 

$\qquad$ The $\text{QUICKSORT}$ procedure implements quicksort. To sort an entire $n$-element array $A[1:n]$, the initial call is $\text{QUICKSORT}(A.1, n)$.

>[!tldr] $\text{QUICKSORT(A, p, r)}$
>if $p < r$  
>$\qquad$// Partition the subarray around the pivot which ends up in $A[q]$  
>$q = \small\text{PARTITION}(A, p, r)$  
>$\small \text{QUICKSORT}(A, p, q-1)\qquad$ //  recursively sort the low side  
>$\small \text{QUICKSORT}(A, q+1, r)\qquad$ //  recursively sort the high side  

Partitioning the array

>[!tldr] $\text{PARTITION}(A, p,r)$
>$x = A[r]\qquad\qquad\qquad\qquad\qquad\space$                           // the pivot  
>$i = p - 1\qquad\qquad\qquad\qquad\qquad$                          // highest index into the low side  
>for $j = p$ to $r -1\qquad\qquad\qquad\space\space$      // process each element other than the pivot  
>$\qquad if A[j] \le x\qquad\qquad\qquad\qquad$        // does this element belong on the low side?  
>$\qquad\qquad i = i+1\qquad\qquad\qquad\qquad\qquad \qquad\space\space$             // index of a new slot in the low side  
>$\qquad\qquad\qquad$ exchange $A[i]$ with $A[j]\qquad\qquad$  // put this element there  
>exchange $A[i+1]$ with $A[r]\qquad\qquad\space\space$  // pivot goes just to the right of the low side  
>return $i + l\qquad\qquad\qquad\qquad\qquad\qquad$// new index of the pivot  

Correctness of Quick Sort :
**Initialization**
**Maintenance**
**Termination**
___
#### Implementation
```cpp
// Quick sort in C++

#include <iostream>
using namespace std;

// function to swap elements
void swap(int *a, int *b) {
  int t = *a;
  *a = *b;
  *b = t;
}

// function to print the array
void printArray(int array[], int size) {
  int i;
  for (i = 0; i < size; i++)
    cout << array[i] << " ";
  cout << endl;
}

// function to rearrange array (find the partition point)
int partition(int array[], int low, int high) {
    
  // select the rightmost element as pivot
  int pivot = array[high];
  
  // pointer for greater element
  int i = (low - 1);

  // traverse each element of the array
  // compare them with the pivot
  for (int j = low; j < high; j++) {
    if (array[j] <= pivot) {
        
      // if element smaller than pivot is found
      // swap it with the greater element pointed by i
      i++;
      
      // swap element at i with element at j
      swap(&array[i], &array[j]);
    }
  }
  
  // swap pivot with the greater element at i
  swap(&array[i + 1], &array[high]);
  
  // return the partition point
  return (i + 1);
}

void quickSort(int array[], int low, int high) {
  if (low < high) {
      
    // find the pivot element such that
    // elements smaller than pivot are on left of pivot
    // elements greater than pivot are on righ of pivot
    int pi = partition(array, low, high);

    // recursive call on the left of pivot
    quickSort(array, low, pi - 1);

    // recursive call on the right of pivot
    quickSort(array, pi + 1, high);
  }
}

// Driver code
int main() {
  int data[] = {8, 7, 6, 1, 0, 9, 2};
  int n = sizeof(data) / sizeof(data[0]);
  
  cout << "Unsorted Array: \n";
  printArray(data, n);
  
  // perform quicksort on data
  quickSort(data, 0, n - 1);
  
  cout << "Sorted array in ascending order: \n";
  printArray(data, n);
}
```
___
#### Performance of quick sort
The running time of quicksort depends on how balanced each partitioning is, which in turn depends on which elements are used as pivots. If the two sides of a partition are about the same size $-$ the partitioning is balanced $-$ then the algorithm runs asymptotically as fast as merge sort. If the partitioning is unbalanced, however, it can run asymptotically as slowly as insertion sort.

##### Worst-case partitioning
The worst-case behaviour for quicksort occurs when the partitioning produces one subproblem with $n-1$ elements and one with 0 elements. This unbalanced partitioning arises in each recursive call and cost us $\Theta (n)$ time .
Recurrence for the running time is 
$$
\begin{align}
T(n) & = T(n-1) + T(0) + \Theta(n) \\
& = T(n-1) + \Theta(n)
\end{align}
$$
The solution to this Recurrence is 
##### Best-case Partitioning
in this case partition produces two subproblem, each of size no more than $n/2$. in this case quick sort runs faster .
Recurrence : 
$$
T(n) = 2T(n/2) + \Theta (n)
$$
This recurrence has solution $T(n) = \Theta (n \text{ lg } n)$
##### Balanced Partitioning

___
#### A Randomized version of Quick sort

>[!tldr] $\text{RANDOMIZED-PARTITION}(A,p,r)$
>$i = \small\text{RANDOM}(p,r)$  
>exchange $A[r]$ with $A[i]$  
>return $\small \text{PARTITION}(A,p,r)$  

>[!tldr] $\text{RANDOMIZED-QUICKSORT}(A,p,r)$
>if $p < r$  
>$\qquad q = \small \text{RANDOMIZED-PARTITION}(A,p,r)$  
>$\qquad \small \text{RANDOMIZED-QUICKSORT}(A, p, q-1)$  
>$\qquad \small \text{RANDOMIZED-QUICKSORT}(A, q+1, r)$  

___
#### Analysis of quick sort
###### Worst-case analysis
We'll use the substitution method to show that running time of quicksort is $O(n^2)$. Let $T(n)$ be the worst-case time for `QUICKSORT` on an input of size n. Because the procedure `PARTITION` produces two subproblems with total size $n-1$ , we obtain the recurrence
$T(n) = \text{max} \{T(q) + T(n-1-a) : 0 \le q \le n-1 \} + \Theta (n)$
We guess that $T(n) \le cn^2$ for some constant $c > 0$. Substituting this guess into recurrence yields.
$$
\begin{align}
T(n) &\le \text{max }\{cq^2 + c(n-1-q)^2 : 0 \le q \le n-1 \} + \Theta(n) \\
&= c \cdot \text{max }\{q^2 + (n-1-1)^2 : 0 \le q \le n -1\} + \Theta (n)
\end{align}
$$
Let's focus out attention on the maximization. For $q = 0, 1, \dots, n-1$ , we have 
$$
\begin{align}
q^2 + (n-1-q)^2 & = q^2 + (n-1)^2 - 2q(n-1) + q^2 \\
& = (n-1)^2 + 2q(q-(n-1)) \\
& \le (n-1)^2
\end{align}
$$

Because $q \le n-1$ implies that $2q(q-(n-1)) < 0$. Thus every term in the maximization is bounded by $(n-1)^2$ 
Continuing with out analysis of $T(n)$ , we obtain
$$
\begin{align}
T(n) & \le c(n-1)^2 + \Theta (n) \\
&\le cn^2 - c(2n-1) + \Theta (n) \\
&\le cn^2
\end{align}
$$
By picking the constant c large enough that the $c(2n-1)$ term dominates the $\Theta(n)$ term. Thus $T(n) = O(n^2)$, We have seen previous that quicksort takes $\Omega (n^2)$ time : when partitioning is maximally unbalanced. Thus the worst case running time of quicksort is $\Theta(n^2)$ . 
___

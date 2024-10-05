# Sorting in Linear Time
All the sorting algorithm we share an interesting property : *the sorted order they determine is based only on comparison between the input elements.*  we call such sorting algorithms **comparison sorts**.
### Lower bounds for sorting
A comparison sort uses only comparison between elements to gain the information about an input sequence $\{a_1, a_2, \dots, a_n\}$. It may not inspect the values of the elements or gain order information about them in any other way.
#### The Decision-tree model
A **decision tree** is a full binary tree that represents the comparison between elements that are performed by a particular sorting algorithm operating on an input of given size.
![[The decision tree.png]]

A decision tree has each internal node annotated by $i:j$ for some $i$ and $j$ in the range $1 \le i, j \le n$ where n is the number of element. Also annotate each leaf by permutation $\pi_1, \pi_2, \dots, \pi_n$ . Indices in the internal nodes and the leaves always refer to the original positions of the array elements at the start of the sorting algorithm. 
The execution of the comparison sorting algorithm corresponds to tracing a simple path from the root of the decision tree down to a leaf. Each internal node indicates a comparison $a_i \le a_j$ . The left subtree then dictates sub-sequent comparisons once we know that $a_i \le a_j$ , and the right subtree dictates subsequent comparisons when $a_i > a_j$ . Arriving at a leaf, the sorting algorithm has established the ordering $a_{\pi(1)} \le a_{\pi(2)} \le \dots a_{\pi(n)}$ Because any correct sorting algorithm must be able to produce each permutation of its input, each of the $n!$ permutations on $n$ elements must appear as at least one of the leaves of the decision tree for a comparison sort to be correct. Furthermore, each of these leaves must be reachable from the root by a downward path corresponding to an actual execution of the comparison sort. (We call such leaves "reachable"). Thus we consider only decision trees in which each permutation appears as a reachable leaf.
### Counting sort
Counting sort assumes that each of the $n$ input elements is an integer in the range $0$ to $k$ , for some integer $k$. It runs in $\Theta (n+k)$ time, so that when $k = O(n)$ counting sort runs in $\Theta (n)$ time.
counting sort first determines, for each input element $x$ the number of element less that or equal to $x$. It then uses this info to place element $x$ directly into its position in the output arrays.
The $\text{COUNTING SORT}$ takes an array $A[1:n]$ , the size $n$ and the limit $k$ on the nonnegative integer values in A as an input and outputs a sorted array $B[1:n]$ and uses an array $C[0:k]$ for temporary working storage.

>[!tldr] $\text{COUNTING-SORT}(A, n, k)$
>let $B[1:n]$ and $C[0:k]$ be new arrays  
>for $i = 0$ to $k$  
>$\qquad$ $C[i] = 0$  
>for $j = 1$ to $n$  
>$\qquad C[A[j]] = C[A[j]] + 1$  
>// $C[i]$ now contains the number of elements equal to $i$  
>for $i = 1$ to $k$  
>$\qquad C[i] = C[i] + C[i-1]$  
>$C[i]$ now contains the number of elements less than or equal to $i$  
>Copy $A$ to $B$, starting from the end of $A$  
>for $j = n$ downto $1$  
>$\qquad B[C[A[j]]] = A[j]$  
>$\qquad C[A[j]] = C[A[j]] - 1$ // to handle duplicate values  
>return $B$  

#### Implementation

```cpp
/* Counting sort */
void countSort(int array[], int size) {
  // The size of count must be at least the (max+1) but
  // we cannot assign declare it as int count(max+1) in C++ as
  // it does not support dynamic memory allocation.
  // So, its size is provided statically.
  int output[10];
  int count[10];
  int max = array[0];

  // Find the largest element of the array
  for (int i = 1; i < size; i++) {
    if (array[i] > max)
      max = array[i];
  }

  // Initialize count array with all zeros.
  for (int i = 0; i <= max; ++i) {
    count[i] = 0;
  }

  // Store the count of each element
  for (int i = 0; i < size; i++) {
    count[array[i]]++;
  }

  // Store the cummulative count of each array
  for (int i = 1; i <= max; i++) {
    count[i] += count[i - 1];
  }

  // Find the index of each element of the original array in count array, and
  // place the elements in output array
  for (int i = size - 1; i >= 0; i--) {
    output[count[array[i]] - 1] = array[i];
    count[array[i]]--;
  }

  // Copy the sorted elements into original array
  for (int i = 0; i < size; i++) {
    array[i] = output[i];
  }
}
```
___
### Radix sort
Radix sort is the algorithm used by the card-sorting machines. 
Radix sorts the input by - counterintuitively sorting on the least significant digit first. The algorithm then combines the cards into a single deck, with the cards in the 0 bin preceding the cards in the 1 bin preceding the cards in the 2 bin and so on. Then it sort the entire deck again on the second-least significant digit and recombines the deck in a like manner. The process continues until the cards have been sorted on all $d$ digit. 

![[Radix sort.png]]
$$\text{Fig : Radix sort on 3-digit numbers}$$
The $Radix sort$ procedure assumes that each element in the array $A[1:n]$ has $d$ digits, where 1 is the lowest-order digit and digit $d$ is the highest-order digit.

>[!tldr] $\text{RADIX-SORT}(A, n, d)$
>for $i = 1$ to $d$  
>$\qquad$ use a stable sort to sort Array $A[1:n]$ on digit $i$  

#### Implementation
```cpp
// Radix Sort in C++ Programming

// Using counting sort to sort the elements in the basis of significant places
void countingSort(int array[], int size, int place) {
  const int max = 10;
  int output[size];
  int count[max];

  for (int i = 0; i < max; ++i)
    count[i] = 0;

  // Calculate count of elements
  for (int i = 0; i < size; i++)
    count[(array[i] / place) % 10]++;

  // Calculate cumulative count
  for (int i = 1; i < max; i++)
    count[i] += count[i - 1];

  // Place the elements in sorted order
  for (int i = size - 1; i >= 0; i--) {
    output[count[(array[i] / place) % 10] - 1] = array[i];
    count[(array[i] / place) % 10]--;
  }

  for (int i = 0; i < size; i++)
    array[i] = output[i];
}

// Main function to implement radix sort
void radixsort(int array[], int size) {
  // Get maximum element
  int max = *max_element(arr, arr + size);
  
  // Apply counting sort to sort elements based on place value.
  for (int place = 1; max / place > 0; place *= 10)
    countingSort(array, size, place);
}
```
___
### Bucket sort
it assumes that the input is drawn from a uniform distribution and has an average-case running time of $O(n)$ . Bucket sort assumes the the input is generated by a random process that distributes elements uniformly and independently over the interval $[0,1)$.
$\space$ Bucket sort divides the interval $[0,1)$ into $n$ equal-sized subintervals or **buckets** and then distributes the $n$ input numbers into the buckets,
To produce the output we simply sort the numbers in the bucket and then go through the buckets in order, list the elements in each.

>[!tldr] $\text{BUCKET-SORT(A,n)}$
>let $B[0:n-1]$ be a new array  
>$\qquad$  
>for $i = 0$ to $n-1$  
>$\qquad$ make $B[i]$ an empy list}  
>for i = 1 to n  
>$\qquad$ insert A[i] into the list $B[\lfloor n \cdot A[i]\rfloor]$  
>for $i = 0$ to $n-1$  
>$\qquad$ sort list B[i] with insertion sort   
>concatenate the $list B[0], B[1], \dots, B[n-1]$  together in order  
>return the concatenated lists  

#### Implementation

```cpp
/* Radix Sort */

// Using counting sort to sort the elements in the basis of significant places
void countingSort(int array[], int size, int place) {
  const int max = 10;
  int output[size];
  int count[max];

  for (int i = 0; i < max; ++i)
    count[i] = 0;

  // Calculate count of elements
  for (int i = 0; i < size; i++)
    count[(array[i] / place) % 10]++;

  // Calculate cumulative count
  for (int i = 1; i < max; i++)
    count[i] += count[i - 1];

  // Place the elements in sorted order
  for (int i = size - 1; i >= 0; i--) {
    output[count[(array[i] / place) % 10] - 1] = array[i];
    count[(array[i] / place) % 10]--;
  }

  for (int i = 0; i < size; i++)
    array[i] = output[i];
}

// Main function to implement radix sort
void radixsort(int array[], int size) {
  // Get maximum element
  int max = getMax(array, size);

  // Apply counting sort to sort elements based on place value.
  for (int place = 1; max / place > 0; place *= 10)
    countingSort(array, size, place);
}
```
___
Sorting Algorithm and Their Time complexity

| Algorithm      | Worst Case running Time  | Average-case running time           |
| -------------- | ------------------------ | ----------------------------------- |
| Insertion sort | $\Theta (n^2)$           | $\Theta (n^2)$                      |
| Merge sort     | $\Theta (n\text{ lg }n)$ | $\Theta (n\text{ lg }n)$            |
| Heap sort      | $\Theta (n\text{ lg }n)$ | ___                                 |
| Quick sort     | $\Theta (n^2)$           | $\Theta (n\text{ lg }n)$ (expected) |
| Counting sort  | $\Theta (k+n)$           | $\Theta (k+n)$                      |
| Radix sort     | $\Theta (d(n+k))$        | $\Theta (d(n+k))$                   |
| Bucket sort    | $\Theta (n^2)$           | $\Theta (n)$ (average-case)         |
### Heaps
The **Heaps** data structure is an array object that we can view as a nearly complete binary tree. each node of the tree corresponds to an element of the array. The tree is completely filled on all levels except possibly the lowest, which is filled from the left up to a point. An array $A[1:n]$ that represents a heap is an object with an attribute A. *heap size* represents how many elements in the heap are stored within array A.
There are two kinds of binary heaps : max-heaps and min-heaps.
in both kinds the values in the nodes satisfy a *heap property*. 

#### Max Heap
In max-heap the max-heap property is that for every node $i$ other than the root, 
$$
A[parent(i)] \ge A[i]
$$
Thus, the largest element in a max-heap is root.
___
#### Min Heap
In min-heaps the min-heap property is that for every node $i$ other than the root 
$$
A[parent(i)] \le A[i]
$$
The smallest element in a min-heap is at the root.
$\qquad$ The heapsort algorithm uses max-heaps. min heaps are used to implement priority queues.
___
### Maintaining the heap property
The procedure `Max-Heapify` maintains the max-heap property. Its inputs are an array $A$ with the heap-size attribute and an index $i$ into the array. When it is called `maxheapify` assumes that the binary trees rooted at left(i) and right(i) are max-heaps but that $A[i]$ might be smaller than its children thus violating the max-heap property . `MAX-HEAPIFY` lets the value at $A[i]$ "float down" in the max-heap so that the subtree rooted at index i obeys the max-heap property.

>[!tldr] $\text{MAX-HEAPIFY}(A, i)$
>$i = \small\text{LEFT}(i)$  
>$r = \small \text{RIGHT}(i)$  
>$\qquad$  
>if $l \le A.heap\mbox{-}size$ and $A[l] > A[i]$  
>$\qquad$ largest = l  
>else $largest = i$  
>$\qquad$  
>if $r \le A.heap\mbox{-}size$ and $A[r] > A[largest]$  
>$\qquad largest = r$   
>if $largest \ne i$  
>$\qquad$ exchange $A[i]$ with $A[largest]$  
>$\small\text{MAX-HEAPIFY}(A, largest)$   

We can describe the running time of `MAX-HEAPIFY` by the recurrence
$$
T(n) \le T(2n/3) + \Theta (1)
$$
The solution to this recurrence, by master theorem is $T(n) = O(\text{lg } n)$ , alternatively we can characterize the running time of `MAX-HEAPIFY` on a node of height $h$ as $O(h)$.
___
#### Building A heap
The procedure `BUILD-MAX-HEAP` converts an array $A[1:n]$ into a max-heap by calling `MAX-HEAPIFY` in a bottom-up manner.

>[!tldr] $\text{BUILD-MAX-HEAP}(A, n)$
>$A.heap\mbox{-}size = n$  
>for $i=[\lfloor n/2 \rfloor]$ downto $l$  
>$\qquad \small\text{MAX-HEAPIFY}(A, i)$  

___
#### The heapsort algorithm
The heapsort algorithm starts by calling the `BUILD-MAX-HEAP` procedure to build a max-heap on the input array $A[1:n]$ Since the maximum element of the array is stored at the root $A[1]$ , `HEAPSORT` can place it into its correct final position by exchanging it with $A[n]$ . If the procedure then  discard node $n$ from the heap $-$ and it can do so by simply decrementing $A.heap-size$ - the children of the root remains max-heaps, but the new root element might violate the max-heap property. To restore the max-heap property, the procedure just calls `MAX-HEAPIFY(A,1)`, which leaves a max-heap in a $A[1:n-1]$ . The `HEAPSORT` procedure then repeats this process for the max-heap of size $n-1$ down to a heap of size 2.

>[!tldr] $\text{HEAPSORT}(A, n)$
>$\small \text{BUILD-MAX-HEAP}(A, n)$  
>for $i = n$ downto $2$  
>$\qquad$exchange $A[1]$ with $A[i]$  
>$\qquad A.heap\mbox{-}size = A.heap\mbox{-}size -1$  
>$\qquad \small\text{MAX-HEAPIFY}(A, 1)$  

The `heapsort` procedure takes $O(n\text{ lg }n)$ time, since the call to `BUILD-MAX-HEAP` takes $O(n)$ time and each of the $n-1$ calls to `MAX-HEAPIFY` takes $O(\text{lg }n)$ time.

#### Implementation
```cpp
// Max-Heap data structure in C++
#include <iostream>
#include <vector>
using namespace std;

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

void heapify(vector<int> &hT, int i) {
    int size = hT.size();
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    if (l < size && hT[l] > hT[largest])
        largest = l;
    if (r < size && hT[r] > hT[largest])
        largest = r;

    if (largest != i) {
        swap(&hT[i], &hT[largest]);
        heapify(hT, largest);
    }
}

void insert(vector<int> &hT, int newNum) {
    hT.push_back(newNum);
    int current = hT.size() - 1;

    // Bubble up
    while (current > 0) {
        int parent = (current - 1) / 2;
        if (hT[current] > hT[parent]) {
            swap(&hT[current], &hT[parent]);
            current = parent;
        } else {
            break;
        }
    }
}

void deleteNode(vector<int> &hT, int num) {
    int size = hT.size();
    int i;
    for (i = 0; i < size; i++) {
        if (num == hT[i])
            break;
    }

    swap(&hT[i], &hT[size - 1]);
    hT.pop_back();
    // Update size after popping
    size = hT.size();  

    // Heapify from the current index to adjust the rest of the heap
    if (i < size) {
        heapify(hT, i);
    }
}

void printArray(const vector<int> &hT) {
    for (int num : hT)
        cout << num << " ";
    cout << "\n";
}

int main() {
    vector<int> heapTree;

    insert(heapTree, 3);
    insert(heapTree, 4);
    insert(heapTree, 9);
    insert(heapTree, 5);
    insert(heapTree, 2);

    cout << "Max-Heap array: ";
    printArray(heapTree);

    deleteNode(heapTree, 4);
    cout << "After deleting an element: ";
    printArray(heapTree);

    return 0;
}
```
___
#### Priority queues
A **priority queue** is a data structure for maintaining a set $S$ of elements, each with an associated value called a key. A max-priority queue supports the following operations: 
- $\text{INSERT} (S, x, k)$ : inserts the element x with key k into the set S, which is equivalent to the operation $S = S \cup \{x\}$
- $\text{MAXIMUM} (S)$  : returns the element of S with the largest key. 
- $\text{EXTRACT-MAX}(S)$ : removes and returns the element of S with the largest key. 
- $\text{INCREASE-KEY} (s,X,K)$ : increases the value of element x’s key to the new value k, which is assumed to be at least as large as x’s current key value.
max-priority queues can be used to schedule jobs on a computer shared among multiple users.
Alternatively, a min-priority queue supports the operations $\text{INSERT, MINIMUM, EXTRACT-MIN, and DECREASE-KEY}$.. A min-priority queue can be used in an even-driven simulator.
___

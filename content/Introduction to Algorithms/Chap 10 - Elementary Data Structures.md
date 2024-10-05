Sets are fundamental to computer science as they are to mathematics. Whereas mathematical sets are unchanging, the sets manipulated by algorithms can grow, shrink, or otherwise change over time. We call such sets **dynamic**. A dynamic set that supports insertion, deletion, and test membership are called **dictionary**.

#### Operation on dynamic sets
Operation on a dynamic set can be grouped into two categories: queries which return some information about the set, and modifying operation, which change the set. 
Here is a list of operations :
- `SEARCH(S,k)` 
- `INSERT(S,x)`
- `DELETE(S, x)`
- `MINIMUM(S)` and `MAXIMUM(S)`
- `SUCCESSOR(S, x)`
- `PREDECESSOR(S, x)`
___
## Elementary Data Structures
#### Arrays 
An array is stored as a contiguous sequence of bytes in memory. If the first element of an array has index $s$ , the array starts at memory address $a$, and each array element occupies $b$ bytes, then the $i$th element occupies byte $a+b(i-s)$  through $a+b(i-s+1)-1$ .
###### Advantages of contiguously allocated arrays include:
- Constant- time access given the index
- Space efficiency
- Memory locality
###### Downside of arrays 
- Fixed size 
#### Matrices
Matrices are two dimensional arrays . The two most common ways to store a matrix are row-major and column-major order. In row-major order , the matrix is store row by row and in column major order the matrix is stored column by column. 

#### Containers: Stacks and queues
stacks and queues are dynamic sets in which the element removed from the set by the delete operation is prespecified. In a stack the element deleted from the set is the one most recently inserted: the stack implements a last-in, first-out or LIFO policy, Similarly, in a queue, the element deleted is always the one that has been in the set for the longest time: the queue implements a first-in, first-out or FIFO policy. 
**Pseudocode** : 

>[!tldr] STACK-EMPTY(S)
>$\text{if }S.top == 0$  
> $\qquad \text{return } \text{TRUE}$  
> $\text{else}$  
> $\qquad \text{return } \text{FALSE}$  

>[!tldr] $\text{PUSH(S, x)}$
>if $S.top == S.size$  
$\qquad$ error $'overflow'$  
else $S.top = S.top + 1$  
$\qquad$ $S[S.top] = x$  

>[!tldr] $\text{POP(S)}$
>if $\text{STACK-EMPTY}(S)$  
$\qquad$ error $\text{underflow}$  
else $S.top = S.top - 1$  
$\qquad$ return $S[S.top + 1]$  

___

Queues 
Pseudocode : 
>[!tldr] $\text{ENQUEUE(Q, x)}$
>If $Q.tail == Q.size$  
>$\qquad Q.tail = 1$  
>else  
>$\qquad Q.tail = Q.tail + 1$  

>[!tldr] $\text{DEQUEUE(Q)}$
>$x = Q[Q.head]$  
>if $Q.head == Q.size$  
>$\qquad Q.head = 1$  
>else   
>$\qquad Q.head = Q.head + 1$  

____
#### Linked Lists 
A linked List is a data structure in which the objects are arranged in linear order. The order in a linked list is determined by a pointer in each object. Since the elements of linked list often contain keys that can be searched for, linked list are sometimes called **search lists**.
```c
typedef struct list{
	item_type item;             /* data item */
	struct list * next;         /* points to successor */
}
```

Types of Linked lists :
- Singly Linked List : 
	Each node in Singly linked list contains one attribute key and only one pointer `next` that points to next node.
- Doubly Linked List : 
	Each node in doubly linked list contains two pointer $-$ `next`, and `prev`. `prev` points to previous node, and next points to next node. 
- Circular Linked List : 
	In Circular linked list the tail node points to head node making linked list circular . It can also be doubly.

>[!tldr] $\text{LIST-SEARCH(L, K)}$
>$x = L.head$  
>while $x \ne NIL$ and $x.key \ne k$  
>$\qquad x = x.next$  
>return $x$  

```C
list* search_list (list *l , item_type x){
	if(l == nullptr){
		return nullptr;
	}

	if(l->item == x){
		return (l);
	}
	else {
		return (seach_list(l->next, x));
	}
}
```

> [!tldr] $\text{LIST-PREPEND(L, x)}$
> $x.next = L.head$  
> $x.prev = NIL$  
> $\space$  
> if $L.head \ne NIL$  
> $\qquad L.head.prev = x$  
> $L.head = x$  

>[!tldr] $\text{LIST-INSERT(x,y)}$
>$x.next = y.next$  
>$x.prev = y$  
>if $y.next != NIL$  
>$\qquad y.next.prev = x$  
>$y.next = x$  

>[!tldr] $\text{LIST-DELETE(L,x)}$
>if $x.prev \ne NIL$  
>else  
>$\qquad L.head = x.next$  
>if $x.next \ne NIL$  
>$\qquad x.next.prev = x.prev$  

> A **sentinel** is a dummy object that allows us to simplify boundary conditions.

___
### Representing rooted trees
we represent each node of a tree by an object. As with linked list, we assume that each node contains a key attribute. The remaining attribute of interest are pointer to other nodes, and they vary according to the type of tree.

#### Binary trees
Each node in binary tree has three attribute $p$, $left$, and $right$ to store pointers to the parent, left child and right child. If $x.p = NIL$ then $x$ is the root. If node $x$ has no left child then $x.left = NIL$ and similarly for the right child. The root of the entire tree $T$ is pointed to by the attribute $T.root$. If $T.root = NIL$ , then the tree is empty.
###### Rooted trees with unbounded branching
We can represent a binary to any class of trees in which the number of each node is at most some constant k. But this scheme does not work for unbounded number of nodes since we do not know how many attribute to allocate in advance. Moreover, if $k$ is the number of children, is bounded by a large constant but most number of children, we may waste a lot of memory.

To solve this problem we use The left-child, right sibling representation which grants us the advantage of using only $O(n)$ space for any $n-$node rooted tree.  Instead of having a pointer to each of its children. each node has two pointers :
1. $x.left-child$ points to the leftmost child of node $x$
2. $x.right-sibling$ points to the sibling of x immediately to its right.
___

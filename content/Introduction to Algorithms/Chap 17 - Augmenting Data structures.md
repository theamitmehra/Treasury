# Augmenting Data structures

### Dynamic order statistics
In chapter 9, we saw how to determine any order statistic in $O(n)$ time from an unordered set. This section show how to modify red-black trees so that we can determine any order statistic for a dynamic set in $O(\lg n)$ time and also compute the rank of an element $-$ its position in the linear order of the set $-$ in $O(\lg n)$ time.

the $i$th order statistics of a set of $n$ elements, where $i\in \{ 1,2,\dots ,n \}$ is simply the element in the set with the $i$th smallest key. 

![[order-statistic tree.png]]

Figure $17.1$ show a data structure that can support fast order-statistic operations.

A *order statistics tree* $T$ is simply a red-black tree with additional information stored in each node. Each node $x$ contains usual red-black tree attributes $x.key, x.color, x.p, x.left,$ and $x.right$ , along with a new attribute, $x.size$. This attribute contains the number of internal nodes (including $x$ itself, but not including any sentinels) in the subtree rooted at x. that is size of subtree.
If we define the sentinel's size to be $0$ then we have the identity.
$x.size = x.left.size + x.right.size +1$

Keys need not be distinct in an order statistic tree. When equal keys are present, the above notion of rank is not well defined. We remove this ambiguity for an order-statistic tree by defining the rank of an element as the position at which it would be printed in an inorder walk of the tree.

#### Retrieving the element with a given rank 
Before we see how to maintain the size information during insertion and deletion, let's see how to implement two order statistic queries that uses this additional information. We begin with an operation that retrieves the element with a given rank. The procedure `OS-SELECT(x,i)` returns a pointer to the node containing the $i$th smallest key in the subtree rooted at x. To find the node with $i$th smallest key in an order-statistic tree $T$, call `OS-SELECT(T.root, i)`. 

>[!tldr] $\text{OS-SELECT}(x, i)$
>1$\qquad r = x.left.size + 1 \qquad\qquad\qquad// \text{rank of } \space x \text{ within the subtree rooted at} \space x$  
>2$\qquad\text{if } \space i == r$  
>3$\qquad\qquad \text{return} \space x$  
>4$\qquad\text{elseif } \space i<r$  
>5$\qquad\qquad\text{return} \space \text{OS-SELECT}(x.left, i)$  
>6$\qquad\text{else return } \space \text{OS-SELECT}(x.right, i-r)$  

Here is how `OS-SELECT(x, i)` works, line 1 computes $r$, the rank of node $x$ within the subtree rooted at $x$. The value of $x.left.size$ is the number of nodes that come before $x$ in an inorder tree walk of subtree rooted at x. Thus $x.left.size+1$ is the rank of x withing the subtree rooted at $x$.
if $i = r$ then node $x$ is the $i$th smallest element, and so line $3$ returns $x$. If $x < r$ then the $ith$ smallest element resides in $x$'s left subtree and therefore, line $5$ recurses on $x.left$. If $i> r$ then the $i$th smallest element resides in $x$'s right subtree. Since the subtree rooted at $x$ contains $r$ element in the subtree rooted at $x$ is the $(i-r)$th smallest element in the subtree rooted at $x.right$. Linear $6$ determines this element recursively.
___
#### Determining the rank of an element
Given a pointer to a node $x$ in an order-statistic tree $T$, the procedure `OS-RANK` returns the position of $x$ in the linear order determined by an inorder tree walk of $T$.

>[!tldr] $\text{OS-RANK}(T, x)$
>1$\qquad r= x.left.size + 1\qquad\qquad\text{ // rank of } \space x \text{ within subtree rooted at }x$  
>2$\qquad y = x$  
>3$\qquad$while $y\neq T.root$  
>4$\qquad\qquad$if $y==y.p.right$  
>5$\qquad\qquad\qquad r = r+ y.p.left.size + 1$  
>6$\qquad\qquad y = y.p$  
>7$\qquad$return $r$  

The `OS-RANK` procedure works as follows. You can think of node $x$'s rank as the number of nodes preceding $x$ in an inorder tree walk, plus 1 for $x$ itself. `OS-RANK` maintains the following loop invariant:

We use this loop invariant to show that `OS-RANK` works correctly as follows :
- **Initialization**: 
	Prior to the first iteration, line 1 sets r to be the rank of the $x.key$ within the subtree rooted at $x$. 
- **Maintenance**:
	At the end of each iteration of the while loop line $6$ sets $y=y.p$ Thus , we must show that if $r$ is the rank of $x.key$ in the subtree rooted at $y$ at the start of the loop body, then $r$ is the rank of $x.key$ in the subtree at $y.p$ at the end if the loop body. In each iteration of the while loop, consider the subtree rooted at $y.p$. The value of $r$ already includes the number of nodes in the subtree rooted at node $y$ that precede $x$ in an inorder walk, and so the procedure must add the nodes in the subtree rooted at $y$'s siblings that precede $x$ in inorder walk, Plus $1$ for $y.p$ if it, too precedes $x$. If $y$ is a left child then neither $y.p$ nor any node in $y.p$'s right subtree precedes $x$ and so `OS-RANK` leaves $r$ alone. Otherwise, $y$ is the right child and all the nodes in $y.p$'s left subtree precede $x$, as does $y.p$ itself. In this case, line $5$ adds, $y.p.left.size  +1$ to the current value of $r$.
- **Termination**: 
	Because each iteration of the loop moves $y$ toward the root and loop terminates when $y=T.root$ the loop eventually terminates. Moreover the subtree rooted at $y$ is the entire tree. Thus the value of $r$ is the rank of $x.key$ in the entire tree.

The running time of `OS-RANK` is at worst proportional to the height of the tree : $O(\lg n)$ on an $n$-node order-statistic tree.
___
#### Maintaining subtree sizes 
Given the $size$ attributes in each node, `OS-SELECT` `OS-RANK` can quickly compute order-statistic information. But if the basic modifying operation on red-black tree can not efficiently maintain the $size$ attribute, our will will have been for naught.

Let's see how to maintain the subtree sizes for both insertion and deletion without affecting the asymptotic running time of either operation.

Insertion into a red-black tree consists of two phases. The first phase goes down the tree from the root, inserting the new node as a child of an existing node. The second phase goes up the tree, changing colors and performing rotations to maintain the red-black properties.

To maintain the subtree sizes in the first phase, simply increment $x.size$ for each node $x$ on the simple path traversed from the root down toward the leaves. The new node added gets a $size$ of $1$. Since there are $O(\lg n)$ nodes on the traversed path, the additional cost of maintaining the size attributes is $O(\lg n)$. 
In the second phase, the only structural changes to the underlying red-black tree are caused by rotations, of which there are at most two. Moreover, a rotation is a local operation: only two nodes have their $size$ attributes invalidated. The link around which the rotation is performed is incident on these two nodes.

> 13$\qquad y.size = x.size$  
> 14$\qquad x.size = x.left.size+x.right.size + 1$  

Since inserting into a red-black requires at most two rotations, updating the $size$ attributes in the second phase costs only $O(1)$ additional time. Thus, the total time for insertion into an $n$-node order statistic tree is $O(\lg n)$ which is asymptotically the same as for an ordinary red-black tree.

Deletion from a red-black tree also consists of two phases: the first operates on the underlying search tree, and the second causes at most three rotations and otherwise performs no structural changes. The first phase removes one node $z$ from the tree and could move at most two other nodes within the tree. To update the subtree sizes, simply traverse a simple path from the lowest node that moves (starting from its original position within the tree) up to the root, decrementing the size attribute of each node on the path. Since this path has length $O(\lg n)$ in an n-node red black tree, the additional time spent maintaining size attributes in the first phase is$O(\lg n)$. For the $O(1)$ rotations in the second phase of deletion, handle them in the same manner as for insertion. Thus, both insertion and deletion, including maintaining the size attributes, take $O(\lg n)$ time for an $n$-node order-statistic tree
____
### How to augment a data structure
The process of augmenting a basic structure to support additional functionality occurs quite frequently in algorithm design. This section examines the steps involved in such augmentation. It includes theorem that allows you to augment red-black trees easily in many cases.

We can break out the process of augmenting a data structure into four steps :
1. Choose an underlying data structure.
2. Determine additional information to maintain in the underlying data structure.
3. Verify that we can maintain the additional information for the basic modifying operations on the underlying data structure.
4. Develop new operations.

##### Augmenting red-black trees
When red-black trees underlie an augmented data structure, we can prove that insertion and deletion can always efficiently maintain certain kinds of additional insertion. The proof of the following theorem is similar to the argument that we can maintain $size$ attribute for order-statistic trees.

___
### Interval trees
This section shows how to augment red-black trees to support operations on dynamic set of intervals.

Intervals are convenient for representing events that each occupy a continuous period of time. 
A simple way to represent an interval $[t_{1},t_{2}]$ is as an object $i$ with attributes $i.low ={1}$   (the **low endpoint**) and $i.high=t_{2}$ (the **high endpoint**). We can that intervals $i$ and $i'$ **overlap** if $i\cap i'\neq \emptyset$ , that is , if $i.low\leq i'.high$ and $i'low \leq i.high$.

![[interval trichotomy.png]]

Above figure show, any two intervals $i$ and $i'$ satisfy the interval trichotomy, if exactly one of the following three properties holds.
1. $i$ and $i'$ overlap
2. $i$ is to the  left of $i'$
3. $i$ is to the right of $i'$

An **interval tree** is a red-black tree that maintains a dynamic set of elements, with each element $x$ containing an interval $x.int$. Interval trees support the following operations:

`INTERVAL-INSERT(T,x)` adds the element $x$, whose $int$ attribute is assumed to contain an interval, to the interval tree $T$.
`INTERVAL-DELETE(T,x)` removes the element $x$ from the interval tree $T$.
`INTERVAL-SEARCH(T,i)` returns a pointer to an element $x$ in the interval tree $T$ such that $x.int$ overlaps interval $i$, or a pointer to the sentinel $T.nil$ if now such element belongs to the set.

The four step method given below will guide our design of an interval tree and the operations that run on it.
###### Step 1: Underlying data structure
A red-black tree serves as the underlying data structure, Each node $x$ contains an interval $x.int$ . The key  of $x$ is the low endpoint, $x.int.low$ of the interval. Thus an inorder tree walk of the data structure lists the intervals in sorted order by now endpoints.
###### Step 2: Additional information
In addition to the intervals themselves, each node $x$ contains a value $x.max$ which is the maximum value of any interval endpoint stored in the subtree rooted at $x$.
###### Step3: Maintaining the information
We must verify that insertion and deletion take $O(\lg n)$ time on an interval tree of $n$ nodes. It is simple enough to determine $x.max$ in $O(1)$ time, given interval $x.int$ and the max values of nodes $x$'s children:
$$
x.max = max\{ x.int.high, x.left.max, x.right.max \}.
$$
###### Step 4: Developing new operations
The only new operation is `INTERVAL-SEARCH(T, i)` which finds a node in the tree $T$ whose interval overlaps interval $i$. If there is no intervals in the tree that overlaps $i$ , the procedure returns a pointer to the sentinel $T.nil$.

>[!tldr] $\text{INTERVAL-SEARCH}(T,i)$
>1 $\qquad x= T.root$  
>2 $\qquad$while $x\neq T.nil$ and $i$ does not overlap $x.int$  
>3 $\qquad\qquad$if $x.left\neq T.nil$ and $x.left.max \geq i.low$  
>4 $\qquad\qquad\qquad x=x.left$ $\qquad\qquad\space\text{//overlap in the left subtree or no overlap in right subtree}$  
>5 $\qquad\qquad$else $x=x.right$ $\qquad\qquad\text{// no overlap in left subtree}$  
>6 $\qquad$return $x$  

The search for an interval that overlaps $i$ starts at the root of the tree and proceeds downward. It terminates when either it finds an overlapping interval or it reaches the sentinel $T.nil$. Since each iteration of the basic loop takes $O(1)$ and since the height of an $n$-node red-black tree is $O(\lg n)$, the `INTERVAL-SEARCH` procedure takes $O(\lg n)$ time.

Before we see why `INTERVAL-SEARCH` is correct, Let's examine how it works on the interval tree in this figure given below 

![[An interval tree.png|500]]

Let's look for an interval the overlaps the interval $i=22,25$ . We begin with $x$ as the root, which contains $[16,21]$ and does not overlap $i$. Since $x.left.max =23$ is greater than $i.low=22$, the loop continues with $x$ as the left child of the root $-$ the node containing $[8,9]$ , which also does not overlap $i$. This time, $x.left.max=10$ is less than $i.low=22$ and so the loop continues with the right child of $x$ as the new $x$. Because the interval overlaps $i$ the procedure return this node.


To see why `INTERVAL-SEARCH` is correct we must understand why it suffices to examine a single path from the root. The basic idea is that any node $x$, if $x.int$ does not overlap $i$, the search always proceeds in the sage direction: the search will definitely find an overlapping interval if the tree contains one. 
The following theorem states this property more precisely

**Theorem**
An execution of `INTERVAL-SEARCH(T,i)` either returns a node whose interval overlaps $i$, or it return $T.nil$ and the tree $T$ contains no node whose interval overlaps $i$.

- For problems and exercise solution visit [[PS-17]]
___
# Binary Search Trees
A binary search tree is a rooted binary tree data structure with the key of each internal node being greater than all the keys in respective node's left subtree and less than the ones in its right subtree. 
It allows binary search for fast lookup, insertion and deletion of nodes with time complexity of $O(\log n)$.
In addition to a $key$ and satellite data each node object contains attributes left, right, and p that points to the nodes corresponding to its left child and its right child and its parent, respectively.

![[Binary Search Trees.png]]

![[Binary Search Trees II.png]]

$$
\begin{flalign}
&\text{Fig : Binary Search Trees} \\
&\text{(a) bst with 6 nodes and height of 2, } \\
&\text{(b) A less efficient bst with height of 4 with same keys}
\end{flalign}
$$
**Binary-search-tree property**: 
Let $x$ be a node in a binary search tree. If $y$ is a node in the left subtree of $x$, then $y.key \le x.key$. If y is a node in the right subtree of $x$, then $y.key \ge x.key$.


Because of the binary-search-tree property, you can print out all the keys in a binary search tree in sorted order by a simple recursive algorithm, called an `inorder` tree walk, given by the procedure I NORDER-TREE-WALK. This algorithm is so named because it prints the key of the root of a subtree between printing the values in its left subtree and printing those in its right subtree. (Similarly, a `preorder` tree walk prints the root before the values in either subtree, and a `postorder` tree walk prints the root after the values in its subtrees.)

>[!tldr] $\text{INORDER-TREE-WALK}$
>if $x \ne \text{NIL}$  
>$\qquad \small \text{INORDER-TREE-WALK}(x.left)$  
>$\qquad$ print $x.key$  
>$\qquad \small \text{INORDER-TREE-WALK}(x.right)$   

It takes $\Theta (n)$ time to walk an $n$-node binary search tree.

### Querying a binary search tree
BST supports `MINIMUM`, `MAXIMUM`, `SUCCESSOR`, and `PREDECESSOR` as well as `SEARCH`. 

#### Searching
To search for a node with given key in bst, call the `TREE-SEARCH` procedure. Given a pointer to $x$ to the root of a subtree and a key $k$ `TREE-SEARCH(x, k)` returns a pointer to a node with key $k$ if one exists in the subtree; otherwise it returns NIL. 

>[!tldr] $\text{TREE-SEARCH}(x, k)$
>if $x == \text{NIL}$ or $k == x.key$  
>$\qquad$ return $x$  
>if $k < x.key$  
>$\qquad$ return $\small \text{TREE-SEARCH}(x.left, k)$  
>else  
>$\qquad$ return $\small\text{TREE-SEARCH}(x.right, k)$

>[!tldr] $\text{ITERATIVE-TREE-SEARCH}(x, k)$
>while $x \ne \text{NIL}$ and $k \ne x.key$  
>$\qquad$ if $k < x.key$  
>$\qquad\qquad$ x = x.left  
>$\qquad$ else $x = x.right$  
>return $x$  

The `TREE-SEARCH` procedure begins its search at the root and traces a simple path downward in the tree. For each node x it encounters, it compares the key $k$ with $x.key$. If the two keys are equal, the search terminates. If k is smaller than $x.key$, the search continues in the left subtree of $x$, since the binary-search-tree property implies that $k$ cannot reside in the right subtree. Symmetrically, if $k$ is larger than $x.key$, the search continues in the right subtree. The nodes encountered during the recursion form a simple path downward from the root of the tree, and thus the running time of TREE-SEARCH is $O(h)$, where $h$ is the height of the tree.
___
#### Minimum and Maximum
>[!tldr] $\text{TREE-MINIMUM}(x)$
>while $x.left \ne \text{NIL}$  
>$\qquad$ $x = x.left$  
>return $x$  

>[!tldr] $\text{TREE-MAXIMUM}(x)$
>while $x.right \ne \text{NIL}$  
>$\qquad x = x.right$  
>return $x$  

Both of these methods take $O(h)$ time.
#### Successor and predecessor

>[!tldr] $\text{TREE-SUCCESSOR}(x)$
>if $x.right \ne \text{NIL}$  
>$\qquad$ return $\text{TREE-MINIMUM}(x.right) \qquad\qquad$ // leftmost node in the right subtree  
>else // find the lowest ancestor of $x$ whose left child is an ancestor of $x$   
>$\qquad y= x.p$  
>$\qquad$ while $y \ne \text{NIL}$ and $x == y.right$  
>$\qquad\qquad x = y$  
>$\qquad\qquad y = y.p$  
>$\qquad$ return $y$  

#### Insertion and Deletion

The `TREE-INSERT` procedure inserts a new node into a binary search tree. The procedure takes a binary search tree $T$ and a node $z$ for which $z.key$ has already filled in , $z.left = \text{NIL}$, and $z.right = \text{NIL}$.

>[!tldr] $\text{TREE-INSERT}(T, z)$
>$x = T.root \qquad\qquad\space\space\space\space$ // node being compared with $z$  
>$y = \text{NIL}\qquad\qquad\qquad\space\space$ // $y$ will be parent of $z$  
>while $x \ne \text{NIL}\qquad\qquad$ // descend until reaching a leaf   
>$\qquad y = x$  
>$\qquad$ if $z.key < x.key$  
>$\qquad\qquad x = x.left$  
>$\qquad$ else $x = x.right$  
>$z.p = y \qquad\qquad\qquad\qquad \qquad$ // found the location - insert $z$ with parent $y$  
>if $y == \text{NIL}$  
>$\qquad T.root = z\qquad\qquad\qquad\space\space$ // tree $T$ was empty  
>elseif $z.key < y.key$  
>$\qquad y.left = z$  
>else $y.right = z$  
>

#### Deletion
To delete a node we have to consider three cases : 
- if $z$ has no children, then simply remove it by modifying its parent to replace $z$ with `NIL` as its child
- If $z$ has just one child then elevate that child to take z's position in the tree by modifying $z$'s parent to replace $z$ by $z$'s child.
- If $z$ has two children, find $z$'s successor $y$ which must belong to $z$'s right subtree and move $y$ to take $z$ position in the tree,  The rest of $z$'s left subtree becomes $y$'s new left subtree. Because y is z's successor, it cannot have a left child, and y’s original right child moves into y’s original position, with the rest of y’s original right subtree following automatically.

As part of the process of deleting a node, subtrees need to move around within the binary search tree. The subroutine `TRANSPLANT` replaces one subtree as a child of its parent with another subtree. 

>[!tldr] $\text{TRANSPLANT}(T, u, v)$
>if $u.p == \text{NIL}$  
>$\qquad$ $T.root = v$  
>elseif $u == u.p.left$  
>$\qquad u.p.left = v$  
>else $u.p.right = v$  
>if $v \ne \text{NIL}$  
>$\qquad v.p = u.p$  

>[!tldr] $\text{TREE-DELETE}(T, z)$
>if $z.left == \text{NIL}$  
>$\qquad \text{TRANSPLANT}(T, z, z.right)$ $\qquad \text{// replace }z \text{ by its right child}$  
>elseif $z.right == \text{NIL}$  
>$\qquad \text{TRANSPLANT}(T, z, z.left)$ $\qquad \text{ // replace }z \text{ by its left child}$  
>else $y = \text{TREE-MINIMUM}(z.right) \qquad$ // y is z's successor  
>$\qquad$ if $y \ne z.right \qquad\qquad\qquad\qquad\qquad\space\space$ // is y father down the tree ?  
>$\qquad\qquad \text{TRANSPLANT}(T, y, y.right) \qquad$ // replace y by its right child  
>$\qquad\qquad y.right = z.right \qquad\qquad\qquad\qquad$  // z's right child becomes  
>$\qquad\qquad y.right.p = y \qquad\qquad\qquad\qquad \space\space$ // y's right child  
>$\qquad \text{TRANSPLANT}(T, z, y)\qquad\qquad\qquad \space\space$ // replace z by its successor y  
>$\qquad y.left = z.left\qquad\qquad\qquad\space\space\space$ // and give z's left child to y  
>$\qquad y.left.p = y\qquad\qquad\qquad\qquad$  // which had no left child  

___
#### Radix trees (Tries)
Given two strings $a=a_{0}a_{1}\dots a_{p}$ and $b = b_{1}b_{1}\dots b_{q}$, where each of $a_{i}$ and $b_{j}$ belongs to some ordered set of characters, we say that string $a$ is lexicographically less than string $b$ if either
1. there exists an integer j, where $0\le j\le min\{p,q\}$, such that $a_{i} = b_{i}$ for all $i=0,1,\dots j-1$ and $a_{j}<b_{j}$ or
2. $p<q$ and $a_{i} = b_{i}$ for all $i = 0,1, \dots, p$.

![[Radix tree (tries).png]]
$$
Figure : \text{A radix tree storing the bit string 1011, 10, 011, and 0}
$$
For example, if a and b are bit strings, then 10100<10110 by rule 1 (letting j D 3) and 10100<101000 by rule 2. 
___

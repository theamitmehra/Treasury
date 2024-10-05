# Basic Structures : Sets, Functions, Sequences, Sums, and Matrices
## Sets
A *set* is an unordered collection of distinct objects, called *elements* or *members* of the set. 
A set is said to *contain* its elements. We write a $\in$ A to denote that a is an element of the set A. The notation a $\not \in$ A denotes that a is not an element of the set A.

There are several ways to describe a set. One way is to list all the members of a set, when
this is possible. We use a notation where all members of the set are listed between braces. For example, the notation {a, b, c, d} represents the set with the four elements a, b, c, and d. This way of describing a set is known as the **roster method**.

Another way to describe a set is to use **set builder** notation. We characterize all those
elements in the set by stating the property or properties they must have to be members. The general form of this notation is {x ∣ x has property P} and is read "the set of all x such that x has property P."

These sets, each denoted using a boldface letter, play an important role in discrete mathematics:
**$\mathbb{N}$**  $=$ {0, 1, 2, 3, $\ldots$}, the set of all **natural numbers**
**$\mathbb{Z}$**  $=$ {$\ldots$ , −2, −1, 0, 1, 2, $\ldots$}, the set of all **integers**
**$\mathbb{Z}$**$^+$ $=$ {1, 2, 3, $\ldots$}, the set of all **positive integers**
**$\mathbb{Q}$** $=$ {p/q ∣ p $\in$ **Z**, q $\in$ **Z**, and q $\ne$ 0}, the set of all **rational numbers** 
**$\mathbb{R}$**  $=$ the set of all **real numbers**
**$\mathbb{R}$$^{+}$** $=$ the set of all **positive real numbers**
**$\mathbb{C}$** $=$ the set of all **complex numbers**.

Among the sets studied in calculus are intervals, sets of all the real numbers between two numbers a and b, with or without a and b. If a and b are real numbers with a $\le$ b, 
we denote these intervals by
**Closed Interval** : \[a, b] $=$ {x | a $\le$ x $\le$ b}
**Open Interval** :    (a, b) $=$ {x | a $<$ x $<$ b}.

Two sets are equal if and only if they have the same elements. Therefore, if A and B are sets,
then A and B are equal if and only if $\forall$x(x $\in$ A $\leftrightarrow$ x $\in$ B). We write A $=$ B if A and B are equal
sets.

**THE EMPTY SET**:
There is a special set that has no elements. This set is called the empty set, or null set, and is denoted by $\emptyset$. The empty set can also be denoted by { } (that is, we represent the empty set with a pair of braces that encloses all the elements in this set).
A set with one element is called a **singleton set**.

#### Subsets
The set A is a subset of B, and B is a superset of A, if and only if every element of A is also an element of B. We use the notation A $\subseteq$ B to indicate that A is a subset of the set B. 
If, instead, we want to stress that B is a superset of A, we use the equivalent notation B $\supseteq$ A. (So, A $\subseteq$ B and B $\supseteq$ A are equivalent statements.)

We see that A $\subseteq$ B if and only if the quantification **$\forall$x(x $\in$ A $\rightarrow$ x $\in$ B)** is true. Note that to show that A is not a subset of B we need only find one element x $\in$ A with x $\not \in$ B. Such an x is a counterexample to the claim that x $\in$ A implies x $\in$ B.

 * **Theorem** :
   For every set S, (i ) $\emptyset$ $\subseteq$ S  and (ii ) S $\subseteq$ S.

When we wish to emphasize that a set A is a subset of a set B but that A $\ne$ B, we write A $\subset$ B and say that A is a **proper subset** of B. For A $\subset$ B to be true, it must be the case that A $\subseteq$ B and there must exist an element x of B that is not an element of A. That is, A is a proper subset of B if and only if **$\forall$x(x $\in$ A $\rightarrow$ x $\in$ B) $\land$ $\exists$x(x $\in$ B $\land$ x $\not \in$ A)** is true.

#### Cardinality
Let S be a set. If there are exactly n distinct elements in S where n is a non-negative integer, we say that S is a *finite set* and that n is the **cardinality** of S. The cardinality of S is  denoted by |S|.
Given a set S, the *power set* of S is the set of all subsets of the set S. The *power set* of S is denoted by $\mathcal {P}$(S).
If a set has n elements, then its power set has 2$^n$ elements.

#### Cartesian Product
The ordered n-tuple (a$_1$, a$_2$, $\ldots$, a$_n$) is the ordered collection that has a$_1$ as its first element, a$_2$ as its second element, $\ldots$ , and a$_n$ as its nth element.
In particular, ordered 2-tuples are called **ordered pairs**.

Let A and B be sets.
The Cartesian product of A and B, denoted by A $\times$ B, is the set of all ordered pairs (a, b), where a $\in$ A and b $\in$ B. 
Hence, **A $\times$ B $=$ {(a, b) ∣ a $\in$ A $\land$ b $\in$ B}.**
## Set Operations

#### Union
Let A and B be sets. The *union* of the sets A and B, denoted by A $\cup$ B, is the set that contains those elements that are either in A or in B, or in both.
An element x belongs to the union of the sets A and B if and only if x belongs to A or x belongs to B. This tells us that **A $\cup$ B $=$ {x ∣ x $\in$ A $\lor$ x $\in$ B}.**
#### Intersection
Let A and B be sets. The *intersection* of the sets A and B, denoted by A $\cap$ B, is the set containing those elements in both A and B. 
An element x belongs to the intersection of the sets A and B if and only if x belongs to A and x belongs to B. This tells us that **A $\cap$ B $=$ {x ∣ x $\in$ A $\land$ x $\in$ B}.**

Two sets are called **disjoint** if their *intersection* is the empty set.

* |A $\cup$ B| $=$ |A| + |B| − |A $\cap$ B|
  
  The generalization of this result to unions of an arbitrary number of sets is called the **principle of inclusion–exclusion**. The principle of inclusion–exclusion is an important technique used in enumeration.
#### Difference
Let A and B be sets. The difference of A and B, denoted by *A − B*, is the set containing those
elements that are in A but not in B. The difference of A and B is also called the *complement* of B with respect to A.
An element x belongs to the difference of A and B if and only if x $\in$ A and x $\not \in$ B. This tells us that **A − B $=$ {x ∣ x $\in$ A $\land$ x $\not \in$ B}.**

#### Complement
Let U be the universal set. The complement of the set A, denoted by $\bar {A}$, is the complement of A with respect to U. Therefore, the complement of the set A is U − A.
An element belongs to $\bar {A}$ if and only if x $\not \in$ A. This tells us that **$\bar {A}$ $=$ {x $\in$ U ∣ x $\not \in$ A}**.

#### Set Identities
| Identity                                                                                                             | Name                |
| -------------------------------------------------------------------------------------------------------------------- | ------------------- |
| A $\cap$ U $=$ A<br>A $\cup$ $\emptyset$ $=$ A                                                                           | Identity Laws       |
| A $\cup$ U $=$ U<br>A $\cap$ $\emptyset$ $=$ $\emptyset$                                                                 | Domination laws     |
| A $\cup$ A $=$ A<br>A $\cap$ A $=$ A                                                                                     | Idempotent laws     |
| $\overline{(\bar{A})}$ $=$ A                                                                                           | Complementation law |
| A $\cup$ B $=$ B $\cup$ A<br>A $\cap$ B $=$ B $\cap$ A                                                                   | Commutative laws    |
| A $\cup$ (B $\cup$ C) $=$ (A $\cup$ B) $\cup$ C<br>A $\cap$ (B $\cap$ C) $=$ (A $\cap$ B) $\cap$ C                       | Associative laws    |
| A $\cup$ (B $\cap$ C) $=$ (A $\cup$ B) $\cap$ (A $\cup$ C)<br>A $\cap$ (B $\cup$ C) $=$ (A $\cap$ B) $\cup$ (A $\cap$ C) | Distributive laws   |
| $\overline {(A \cap B)}$ $=$ $\bar {A}$ $\cup$ $\bar {B}$<br>$\overline {(A \cup B)}$ $=$ $\bar {A}$ $\cap$ $\bar {B}$   | De Morgan’s laws    |
| A $\cup$ (A $\cap$ B) $=$ A<br>A $\cap$ (A $\cup$ B) $=$ A                                                               | Absorption laws     |
| A $\cup$ $\bar {A}$ $=$ U<br>A $\cap$ $\bar {A}$ $=$ $\emptyset$                                                         | Complement laws     |

The union of a collection of sets is the set that contains those elements that are members at least one set in the collection. We use the notation **A$_1$ $\cup$ A$_2$ $\cup$ $\ldots$ $\cup$ A$_n$ $=$ $\bigcup$$^n_{i=1}$ A$_i$** to denote the union of the sets A$_1$, A$_1$, $\ldots$, A$_n$.

The intersection of a collection of sets is the set that contains those elements that are members of all the sets in the collection. We use the notation **A$_1$ $\cap$ A$_2$ $\cap$ $\ldots$ $\cap$ A$_n$ $=$ $\bigcap$$^n_{i=1}$ A$_i$** to denote the intersection of the sets A$_1$, A$_2$, $\ldots$, A$_n$.

#### Multisets
Sometimes the number of times that an element occurs in an unordered collection matters. A **multiset** (short for multiple-membership set) is an unordered collection of elements where an element can occur as a member more than once. We can use the same notation for a multiset as we do for a set, but each element is listed the number of times it occurs. So, the multiset denoted by {a, a, a, b, b} is the multiset that contains the element a thrice and the element b twice. When we use this notation, it must be clear that we are working with multisets and not ordinary sets. We can avoid this ambiguity by using an alternate notation for multisets. The notation {m$_1$ ⋅ a$_1$, m$_2$ ⋅ a$_n$, $\ldots$, m$_r$ ⋅ a$_r$} denotes the multiset with element a$_1$ occurring m$_1$ times, element a$_2$ occurring m$_2$ times, and so on.
The numbers m$_i$, i $=$ 1, 2, $\ldots$ , r, are called the **multiplicities** of the elements a$_i$, i $=$ 1, 2, $\ldots$ , r.
(Elements not in a multiset are assigned 0 as their multiplicity in this set.)
The cardinality of a multiset is defined to be the sum of the multiplicities of its elements. **The word multiset was introduced by Nicolaas Govert de Bruijn in the 1970s, but the concept dates back to the 12th century work of the Indian mathematician Bhaskaracharya.**

Let P and Q be multisets. The **union** of the multisets P and Q is the multiset in which the
multiplicity of an element is the maximum of its multiplicities in P and Q. 
The **intersection** of P and Q is the multiset in which the multiplicity of an element is the minimum of its multiplicities in P and Q. 
The **difference** of P and Q is the multiset in which the multiplicity of an element is
the multiplicity of the element in P less its multiplicity in Q unless this difference is negative,
in which case the multiplicity is 0. 
The **sum** of P and Q is the multiset in which the multiplicity of an element is the sum of multiplicities in P and Q. 
The **union**, **intersection**, and **difference** of P and Q are denoted by **P $\cup$ Q, P $\cap$ Q,** and **P − Q**, respectively . The sum of P and Q is denoted by **P + Q**.

## Functions

Let A and B be nonempty sets. A function $\mathcal{f}$ from A to B is an assignment of exactly one element of B to each element of A. We write $\mathcal{f}$(a) $=$ b if b is the unique element of B assigned
by the function $\mathcal{f}$ to the element a of A. If $\mathcal{f}$ is a function from A to B, we write $\mathcal{f}$ : A $\rightarrow$ B.

A function $\mathcal{f}$ : A $\rightarrow$ B can also be defined in terms of a relation from A to B. 
A relation from A to B that contains one, and only one, ordered pair (a, b) for every element
a $\in$ A, defines a function $\mathcal{f}$ from A to B. This function is defined by the assignment $\mathcal{f}$(a) $=$ b, where (a, b) is the unique ordered pair in the relation that has a as its first element.

If $\mathcal{f}$ is a function from A to B, we say that A is the domain of $\mathcal{f}$ and B is the codomain of $\mathcal{f}$.
If $\mathcal{f}$(a) $=$ b, we say that b is the image of a and a is a preimage of b. The range, or image, of
$\mathcal{f}$ is the set of all images of elements of A. Also, if $\mathcal{f}$ is a function from A to B, we say that $\mathcal{f}$ maps A to B.

Let $\mathcal{f}$$_1$ and $\mathcal{f}$$_2$ be functions from A to R. Then $\mathcal{f}$$_1$ + $\mathcal{f}$$_2$ and $\mathcal{f}$$_1$$\mathcal{f}$$_2$ are also functions from A to R
defined for all x $\in$ A by :
* ($\mathcal{f}$$_1$ + $\mathcal{f}$$_2$)(x) $=$ $\mathcal{f}$$_1$(x) + $\mathcal{f}$$_2$(x),
* ($\mathcal{f}$$_1$$\mathcal{f}$$_2$)(x) $=$ $\mathcal{f}$$_1$(x)$\mathcal{f}$$_2$(x).

Let $\mathcal{f}$ be a function from A to B and let S be a subset of A. The image of S under the function
$\mathcal{f}$ is the subset of B that consists of the images of the elements of S. We denote the image of S by $\mathcal{f}$(S), so **$\mathcal{f}$(S) $=$ {t ∣ $\exists$s $\in$ S (t $=$ $\mathcal{f}$(s))}**.
We also use the shorthand {$\mathcal{f}$(s) ∣ s $\in$ S} to denote this set.

#### One-to-One and Onto Functions
Some functions never assign the same value to two different domain elements. These functions are said to be **one-to-one**.
A function $\mathcal{f}$ is said to be one-to-one, or an injection, if and only if $\mathcal{f}$(a) $=$ $\mathcal{f}$(b) implies that
a $=$ b for all a and b in the domain of $\mathcal{f}$. A function is said to be injective if it is one-to-one.

Note that a function $\mathcal{f}$ is *one-to-one* if and only if $\mathcal{f}$(a) $\ne$ $\mathcal{f}$(b) whenever a $\ne$ b. This way of
expressing that $\mathcal{f}$ is one-to-one is obtained by taking the contrapositive of the implication in the definition. We can express that $\mathcal{f}$ is one-to-one using quantifiers as 
**$\forall$a$\forall$b($\mathcal{f}$(a) $=$ $\mathcal{f}$(b) $\rightarrow$ a $=$ b)** or equivalently **$\forall$a$\forall$b(a $\ne$ b $\rightarrow$ $\mathcal{f}$(a) $\ne$ $\mathcal{f}$(b))**, 
where the universe of discourse is the domain of the function.

A function $\mathcal{f}$ whose domain and codomain are subsets of the set of real numbers is called
**increasing if $\mathcal{f}$(x) $\le$ $\mathcal{f}$(y)**, and **strictly increasing if $\mathcal{f}$(x) $<$ $\mathcal{f}$(y)**, whenever x $<$ y and x and y
are in the domain of $\mathcal{f}$. Similarly, $\mathcal{f}$ is called **decreasing if $\mathcal{f}$(x) $\ge$ $\mathcal{f}$(y)**, and **strictly decreasing if $\mathcal{f}$(x) $>$ $\mathcal{f}$(y)**, whenever x $<$ y and x and y are in the domain of $\mathcal{f}$.

A function $\mathcal{f}$ is ->

* **increasing if $\forall$x$\forall$y(x $<$ y $\rightarrow$ $\mathcal{f}$(x) $\le$ $\mathcal{f}$(y))**, 
* **strictly increasing if $\forall$x$\forall$y(x $<$ y $\rightarrow$ $\mathcal{f}$(x) $<$ $\mathcal{f}$(y))**, 
* **decreasing if $\forall$x$\forall$y(x $<$ y $\rightarrow$ $\mathcal{f}$(x) $\ge$ $\mathcal{f}$(y))**, and 
* **strictly decreasing if $\forall$x$\forall$y(x $<$ y $\rightarrow$ $\mathcal{f}$(x) $>$ $\mathcal{f}$(y))**, 

where the universe of discourse is the domain of $\mathcal{f}$.

A function $\mathcal{f}$ from A to B is called onto, or a *surjection*, if and only if for every element
b $\in$ B there is an element a $\in$ A with $\mathcal{f}$(a) $=$ b. A function $\mathcal{f}$ is called *surjective* if it is onto.
A function $\mathcal{f}$ is onto if **$\forall$y$\exists$x($\mathcal{f}$(x) $=$ y)**, where the domain for x is the domain of the function and the domain for y is the codomain of the function.

The function $\mathcal{f}$ is a one-to-one correspondence, or a bijection, if it is both one-to-one and
onto. We also say that such a function is bijective.

Suppose that $\mathcal{f}$ : A $\rightarrow$ B :
* *To show that $\mathcal{f}$ is injective* 
  Show that if $\mathcal{f}$(x) $=$ $\mathcal{f}$(y) for arbitrary x, y $\in$ A, then x $=$ y.
* *To show that $\mathcal{f}$ is not injective* 
  Find particular elements x, y $\in$ A such that x $\ne$ y and $\mathcal{f}$(x) $=$ $\mathcal{f}$(y).
* *To show that $\mathcal{f}$ is surjective* 
  Consider an arbitrary element y $\in$ B and find an element x $\in$ A such that $\mathcal{f}$(x) $=$ y.
* *To show that $\mathcal{f}$ is not surjective*
  Find a particular y $\in$ B such that $\mathcal{f}$(x) $\ne$ y for all x $\in$ A.

#### Inverse Functions and Compositions of Functions
Let $\mathcal{f}$ be a one-to-one correspondence from the set A to the set B. The inverse function of $\mathcal{f}$ is the function that assigns to an element b belonging to B the unique element a in A such that $\mathcal{f}$(a) $=$ b. The inverse function of $\mathcal{f}$ is denoted by $\mathcal{f}$$^{−1}$. Hence, $\mathcal{f}$$^{-1}$(b) $=$ a when $\mathcal{f}$(a) $=$ b.

If a function $\mathcal{f}$ is not a one-to-one correspondence, we cannot define an inverse function of
$\mathcal{f}$. When $\mathcal{f}$ is not a one-to-one correspondence, either it is not one-to-one or it is not onto. If $\mathcal{f}$ is not one-to-one, some element b in the codomain is the image of more than one element in the domain. If $\mathcal{f}$ is not onto, for some element b in the codomain, no element a in the domain exists for which $\mathcal{f}$(a) $=$ b. 
Consequently, if $\mathcal{f}$ is not a one-to-one correspondence, we cannot assign to each element b in the codomain a unique element a in the domain such that $\mathcal{f}$(a) $=$ b (because for some b there is either more than one such a or no such a).
A one-to-one correspondence is called **invertible** because we can define an inverse of this
function. A function is **not invertible** if it is not a one-to-one correspondence, because the
inverse of such a function does not exist.

Let g be a function from the set A to the set B and let f be a function from the set B to the set C. The composition of the functions $\mathcal{f}$ and $\mathcal{g}$, denoted for all a $\in$ A by $\mathcal{f}$ ◦ $\mathcal{g}$, is the function
from A to C defined by ($\mathcal{f}$ ◦ $\mathcal{g}$)(a) $=$ $\mathcal{f}$($\mathcal{g}$(a)).

#### The Graph of Functions
We can associate a set of pairs in A $\times$ B to each function from A to B. This set of pairs is called the **graph** of the function and is often displayed pictorially to aid in understanding the behavior of the function.
Let $\mathcal{f}$ be a function from the set A to the set B. The graph of the function $\mathcal{f}$ is the set of ordered pairs **{(a, b) ∣ a $\in$ A and $\mathcal{f}$(a) $=$ b}**.

#### Important Functions
The **floor function** assigns to the real number x the largest integer that is less than or equal to x. The value of the floor function at x is denoted by $\lfloor$x$\rfloor$. 
The **ceiling function** assigns to the real number x the smallest integer that is greater than or equal to x. The value of the ceiling function at x is denoted by $\lceil$x$\rceil$.

* $\lfloor$x$\rfloor$ $=$ n if and only if n $\le$ x $<$ n + 1
* $\lceil$x$\rceil$ $=$ n if and only if n − 1 $<$ x $\le$ n
* $\lfloor$x$\rfloor$ $=$ n if and only if x − 1 $<$ n $\le$ x
* $\lceil$x$\rceil$ $=$ n if and only if x $\le$ n $<$ x + 1
* **x − 1 $<$ $\lfloor$x$\rfloor$ $\le$ x $\le$ $\lceil$x$\rceil$ $<$ x + 1**
* $\lfloor$−x$\rfloor$ $=$ −$\lceil$x$\rceil$
* $\lceil$−x$\rceil$ $=$ −$\lfloor$x$\rfloor$
* $\lfloor$x + n$\rfloor$ $=$ $\lfloor$x$\rfloor$ + n
* $\lceil$x + n$\rceil$ $=$ $\lceil$x$\rceil$ + n
## Sequences and Summations
#### Sequences
A sequence is a discrete structure used to represent an ordered list. The terms of a sequence can be specified by providing a formula for each term of the sequence.
A sequence is a function from a subset of the set of **Z** to a set S. We use the notation a$_n$ to denote the image of the integer n. We call an a term of the sequence.
* A **geometric progression** is a sequence of the form a, ar, ar$^2$, $\ldots$, ar$^n$, $\ldots$
  where the initial term a and the common ratio r are real numbers.
* An **arithmetic progression** is a sequence of the form a, a + d, a + 2d, $\ldots$, a + nd, $\ldots$
  where the initial term a and the common difference d are real numbers.
#### Recurrence Relations
A recurrence relation for the sequence {a$_n$} is an equation that expresses an in terms of
one or more of the previous terms of the sequence, namely, a$_0$, a$_1$, $\ldots$, a$_{n-1}$, for all integers n
with n $\ge$ n$_0$, where n$_0$ is a non-negative integer. 
A sequence is called a solution of a recurrence relation if its terms satisfy the recurrence relation. (A recurrence relation is said to recursively define a sequence.)
The initial conditions for a recursively defined sequence specify the terms that precede the
first term where the recurrence relation takes effect.

#### Summations
A large uppercase Greek letter sigma, $\sum$, is used to denote summation.

* $\sum$$^n_{i=m}$ a$_{i}$ $=$ a$_{m}$ + a$_{m+1}$ + $\ldots$ + a$_{n}$.

The variable i is called **index of summation**. The index of summation runs through all integers starting with its lower limit m and ending with its upper limit n.

#### Cardinality of Sets
The sets A and B have the same cardinality if and only if there is a one-to-one correspondence from A to B. When A and B have the same cardinality, we write |A| $=$ |B|.
If there is a one-to-one function from A to B, the cardinality of A is less than or the same as the cardinality of B and we write |A| $\le$ |B|. Moreover, when |A| $\le$ |B| and A and B have different cardinality, we say that the cardinality of A is less than the cardinality of B and we
write |A| $<$ |B|.

A set that is either finite or has the same cardinality as the set of positive integers is called
countable. A set that is not countable is called uncountable. 
When an infinite set S is countable, we denote the cardinality of S by $\aleph_0$ (where $\aleph$ is aleph, the first letter of the Hebrew alphabet). 
We write |S| $=$ $\aleph_0$ and say that S has cardinality "aleph null."

* **SCHRÖDER-BERNSTEIN THEOREM** :
  If A and B are sets with |A| $\le$ |B| and |B| $\le$ |A|, then |A| $=$ |B|.
  In other words, if there are one-to-one functions f from A to B and g from B to A, then there is a one-to-one correspondence between A and B.
  
#### **THE CONTINUUM HYPOTHESIS**
It can be shown that the power set of **Z$^{+}$** and the set of real numbers **R** have the same cardinality. In other words, we know that |$\mathcal {P}$(Z+)| $=$ |R| $=$ c, where c denotes the cardinality of the set of real numbers. An important theorem of Cantor states that the cardinality of a set is always less than the cardinality of its power set. Hence, |Z+| $<$ |$\mathcal {P}$(Z+)|. 
We can rewrite this as $\aleph_1$ $<$ 2$^{\aleph_0}$,  using the notation 2$^{|S|}$ to denote the cardinality of the power set of the set S. 
Also, note that the relationship |$\mathcal {P}$(Z+)| $=$ |R| can be expressed as 2$^{\aleph_0}$ $=$ $\mathfrak{c}$. 
This leads us to the continuum hypothesis, which asserts that there is no cardinal number X between $\aleph_1$ and $\mathfrak{c}$.
The **continuum hypothesis** states that there is no set A such that $\aleph_1$, the cardinality of the set of positive integers, is less than |A| and |A| is less than $\mathfrak{c}$, the cardinality of the set of real numbers. It can be shown that the smallest infinite cardinal numbers form an infinite sequence  *$\aleph_0$* $<$ *$\aleph_1$* $<$ *$\aleph_2$* $<$ $\ldots$ . If we assume that the continuum hypothesis is true, it would follow that $\mathfrak{c}$ $=$ $\aleph_1$, so that 2$^{\aleph_0}$ $=$ $\aleph_1$.

## Matrices
A matrix is a rectangular array of numbers. A matrix with m rows and n columns is called an
m $\times$ n matrix. The plural of matrix is matrices. A matrix with the same number of rows as columns is called square. Two matrices are equal if they have the same number of rows and the same number of columns and the corresponding entries in every position are equal.

#### Matrix Arithmetic
Let A $=$ \[a$_{ij}$] and B $=$ \[b$_{ij}$] be m $\times$ n matrices.
The sum of A and B, denoted by A + B, is the m $\times$ n matrix that has a$_{ij}$ + b$_{ij}$ as its (i, j)-th element. 
In other words, **A + B $=$ \[a$_{ij}$ + b$_{ij}$]**.

Let A be an m $\times$ k matrix and B be a k $\times$ n matrix. 
The product of A and B, denoted by AB, is the m $\times$ n matrix with its (i, j)-th entry equal to the sum of the products of the corresponding elements from the i-th row of A and the j-th column of B. 
In other words, **if AB $=$ \[c$_{ij}$], then c$_{ij}$ $=$ a$_{i1}$b$_{1j}$ + a$_{i2}$b$_{2j}$ + $\ldots$ + a$_{ik}$b$_{kj}$.**
#### Transposes and Powers of Matrices

The identity matrix of order n is the n $\times$ n matrix I$_n$ $=$ \[δ$_{ij}$], (*the Kronecker delta*)
where δ$_{ij}$ $=$ 1 if i $=$ j and δ$_{ij}$ $=$ 0 if i $\ne$ j. 
Hence,
*  $\begin{bmatrix} 1 & 0 & {\ldots} & 0\\ 0 & 1 & {\ldots} & 0\\ . & . &  & .\\ . & . &  & .\\0 & 0 & {\ldots} & 1\end{bmatrix}$

Multiplying a matrix by an appropriately sized identity matrix does not change this matrix. 
In other words, when A is an m $\times$ n matrix, we have **AI$_n$ $=$ I$_m$A $=$ A**.
Powers of square matrices can be defined because matrix multiplication is associative. When A is an n $\times$ n matrix, we have **A$^0$ $=$ I$_n$,  A$^r$ $=$ AAA $\ldots$ A**. (*r times*)

Let A $=$ \[a$_{ij}$] be an m $\times$ n matrix. The transpose of A, denoted by A$^t$, is the n $\times$ m matrix
obtained by interchanging the rows and columns of A. 
In other words, **if A$^t$ $=$ \[b$_{ij}$], then b$_{ij}$ $=$ a$_{ji}$** for i $=$ 1, 2, $\ldots$ , n and j $=$ 1, 2, $\ldots$ , m.

A square matrix A is called symmetric if A $=$ A$^t$ . 
Thus, **A $=$ \[a$_{ij}$] is symmetric if a$_{ij}$ $=$ a$_{ji}$** for all i and j with 1 $\le$ i $\le$ n and 1 $\le$ j $\le$ n.
#### Zero-One Matrices

Let A $=$ \[a$_{ij}$] and B $=$ \[b$_{ij}$] be m $\times$ n zero–one matrices. 
Then the **join** of A and B is the zero–one matrix with (i, j)-th entry a$_{ij}$ $\lor$ b$_{ij}$. 
The join of A and B is denoted by **A $\lor$ B**. 
The **meet** of A and B is the zero–one matrix with (i, j)th entry a$_{ij}$ $\land$ b$_{ij}$. 
The meet of A and B is denoted by **A $\land$ B**.

Let A $=$ \[a$_{ij}$] be an m $\times$ k zero–one matrix and B $=$ \[b$_{ij}$] be a k $\times$ n zero–one matrix.
Then the Boolean product of A and B, denoted by **A ⊙ B**, is the m $\times$ n matrix with (i, j)-th entry **c$_{ij}$ where c$_{ij}$ $=$ (a$_{i1}$ $\land$ b$_{1j}$) $\lor$ (a$_{i2}$ $\land$ b$_{2j}$) $\lor$ $\ldots$ $\lor$ (a$_{ik}$ $\land$ b$_{kj}$)**.

Let A be a square zero–one matrix and let r be a positive integer. The r-th Boolean power of A is the Boolean product of r factors of A. The r-th Boolean product of A is denoted by A$^{[r]}$.
Hence, **A$^{[r]}$ $=$ A ⊙ A ⊙ A ⊙ $\ldots$ ⊙ A**. (*r times*). We also define **A$^{[0]}$ $=$ I$_n$**.
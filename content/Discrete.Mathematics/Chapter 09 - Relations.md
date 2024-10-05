# Relations

Relationships between elements of more than two sets arise in many contexts. These relationships can be represented by $n$-ary relations, which are collections of $n$-tuples. Such relations are the basis of the relational data model, the most common way to store information in computer databases.

## Relations and Their Properties

The most direct way to express a relationship between elements of two sets is to use ordered pairs made up of two related elements. For this reason, sets of ordered pairs are called *binary relations*.

* **Definition**:
  Let $A$ and $B$ be sets. A **binary relation** from $A$ to $B$ is a subset of $A \times B$.

In other words, a binary relation from $A$ to $B$ is a set $R$ of ordered pairs, where the first element of each ordered pair comes from $A$ and the second element comes from $B$. We use the notation $a \mathrel{R} b$ to denote that $(a, b) \in R$ and $a \not \mathrel{R} b$ to denote that $(a, b) \notin R$.

* **Definition**:
  A relation on a set $A$ is a relation from $A$ to $A$.

#### Functions as Relations

If $R$ is a relation from $A$ to $B$ such that every element in $A$ is the first element of exactly one ordered pair of $R,$ then a function can be defined with $R$ as its graph. A relation can be used to express a one-to-many relationship between the elements of the sets $A$ and $B$, where an element of $A$ may be related to more than one element of $B$.

A function represents a relation where exactly one element of $B$ is related to each element
of $A$. Relations are a generalization of graphs of functions; they can be used to express a much wider class of relationships between sets.

#### Properties of Relations

In some relations an element is always related to itself. For instance, let $R$ be the relation on the set of all people consisting of pairs $(x, y)$ where $x$ and $y$ have the same mother and the same father. Then $x \mathrel{R} x$ for every person $x$.

* **Definition**:
  A relation $R$ on a set $A$ is called **reflexive** if $(a, a) \in R$ for every element $a \in A$.

Using quantifiers we see that the relation $R$ on the set $A$ is reflexive if $\forall a ((a, a) \in R),$ where the universe of discourse is the set of all elements in $A$.

* **Definition**:
  A relation $R$ on a set $A$ is called **symmetric** if $(b, a) \in R$ whenever $(a, b) \in R,$ for all $a, b \in A.$ A relation $R$ on a set $A$ such that for all $a, b \in A,$ if $(a, b) \in R$ and $(b, a) \in R,$ then $a = b$ is called **antisymmetric**.

Using quantifiers, we see that the relation $R$ on the set $A$ is symmetric if $\forall a \forall b \, ((a, b) \in R \rightarrow (b, a) \in R)$. Similarly, the relation $R$ on the set $A$ is antisymmetric if
$\forall a \forall b \, ((a, b) \in R \land (b, a) \in R \rightarrow a = b)$.

* **Definition**:
  A relation $R$ on a set $A$ is called **transitive** if whenever $(a, b) \in R$ and $(b, c) \in R,$ then $(a, c) \in R,$ for all $a, b, c \in A$.

Using quantifiers we see that the relation $R$ on a set $A$ is transitive if we have $\forall a \forall b \forall c \, (((a, b) \in R ∧ (b, c) \in R) \rightarrow (a, c) \in R)$.

#### Combining Relations

Because relations from $A$ to $B$ are subsets of $A \times B,$ two relations from $A$ to $B$ can be combined in any way two sets can be combined.

* **Definition**:
  Let $R$ be a relation from a set $A$ to a set $B$ and $S$ a relation from $B$ to a set $C$. The composite of $R$ and $S$ is the relation consisting of ordered pairs $(a, c),$ where $a \in A, c \in C,$ and for which there exists an element $b \in B$ such that $(a, b) \in R$ and $(b, c) \in S$. We denote the composite of $R$ and $S$ by $S \circ R$.

The powers of a relation $R$ can be recursively defined from the definition of a composite of two relations.

* **Definition**:
  Let $R$ be a relation on the set $A$. The powers $R^n, \, n = 1, 2, 3, \ldots,$ are defined recursively by $R^1 = R$  and $R^{n + 1} = R^n \circ R$.

* **Theorem**:
  The relation $R$ on a set $A$ is transitive if and only if $R^n \subseteq R$ for $n = 1, 2, 3, \ldots$.

## $n$-ary Relations and Their Applications

We will study relationships among elements from more than two sets in this section. These relationships are called **$n$-ary relations**.

* **Definition**:
  Let $A_1, A_2, \ldots, A_n$ be sets. An $n$-ary relation on these sets is a subset of $A_1 \times A_2 \times \ldots \times A_n$. The sets $A_1, A_2, \ldots, A_n$ are called the **domains** of the relation, and $n$ is called its **degree**.

#### Databases and Relations

The time required to manipulate information in a database depends on how this information is stored. Because of the importance of these operations, various methods for representing databases have been developed. We will discuss one of these methods, called the relational data model, based on the concept of a relation.

A database consists of **records**, which are $n$-tuples, made up of **fields**. The fields are the entries of the $n$-tuples. Relations used to represent databases are also called **tables**.

A domain of an $n$-ary relation is called a **primary key** when the value of the $n$-tuple from this domain determines the $n$-tuple. That is, a domain is a primary key when no two $n$-tuples in the relation have the same value from this domain.

Records are often added to or deleted from databases. Because of this, the property that a domain is a primary key is time-dependent. Consequently, a primary key should be chosen that remains one whenever the database is changed. The current collection of n-tuples in a relation is called the **extension** of the relation. The more permanent part of a database, including the name and attributes of the database, is called its **intension**.  When selecting a primary key, the goal should be to select a key that can serve as a primary key for all possible extensions of the database.

Combinations of domains can also uniquely identify n-tuples in an $n$-ary relation. When the values of a set of domains determine an $n$-tuple in a relation, the Cartesian product of these domains is called a **composite key**.

#### Operations on $n$-ary Relations

There are a variety of operations on n-ary relations that can be used to form new $n$-ary relations. Applied together, these operations can answer queries on databases that ask for all $n$-tuples that satisfy certain conditions.

* **Definition**:
  Let $R$ be an $n$-ary relation and $C$ a condition that elements in $R$ may satisfy. Then the selection operator $s_C$ maps the $n$-ary relation $R$ to the $n$-ary relation of all $n$-tuples from $R$ that satisfy the condition $C$.

Projections are used to form new $n$-ary relations by deleting the same fields in every record of the relation.

* **Definition**:
  The **projection** $P_{i_1, i_2, \ldots, i_m}$ where $i_1 < i_2 < \ldots < i_m$, maps the $n$-tuple ($a_1, a_2, \ldots, a_n$) to the  $m$-tuple ($a_{i_1}, a_{i_2}, \ldots, a_{i_m}$), where $m \leqslant n$.

* **Definition**:
  Let $R$ be a relation of degree $m$ and $S$ a relation of degree $n$.
  The **join** $J_p (R, S),$ where $p \leqslant m$ and $p \leqslant n,$ is a relation of degree $m + n - p$ that consists of all $(m + n - p)$-tuples $(a_1, a_2, \ldots, a_{m - p}, c_1, c_2, \ldots, c_p, b_1, b_2, \ldots, b_{n - p}),$  where the $m$-tuple $(a_1, a_2, \ldots, a_{m - p}, c_1, c_2, \ldots, c_p)$ belongs to $R$ and the $n$-tuple $(c_1, c_2, \ldots, c_p, b_1, b_2, \ldots, b_{n - p})$ belongs to $S$.

## Representing Relations

In this section, all relations we study will be binary relations.

#### Representing Relations Using Matrices

A relation between finite sets can be represented using a zero–one matrix. Suppose that $R$ is a relation from $A = \{a_1, \ldots, a_m\}$ to $B = \{b_1, \ldots, b_n\}$. The relation $R$ can be represented by the matrix $M_R = [m_{ij}],$ where $$\begin{align*}
& m_{ij} = \begin{cases} 1 \qquad \text{if} (a_i, b_j) \in R, \\0 \qquad \text{if} (a_i, b_j) \notin R. \end{cases}&
\end{align*}$$
Recalling the definition of the transpose of a matrix, we see that $R$ is symmetric if and only if $$\begin{align*}
& M_R = (M_R)^t,&
\end{align*}$$that is, if $M_R$ is a symmetric matrix.

#### Representing Relations Using Digraphs

There is another important way of representing a relation using a pictorial representation. Each element of the set is represented by a point, and each ordered pair is represented using an arc with its direction indicated by an arrow.

* **Definition**:
  A **directed graph**, or **digraph**, consists of a set $V$ of **vertices** (or **nodes**) together with a set $E$ of ordered pairs of elements of $V$ called **edges** (or **arcs**). The vertex $a$ is called the **initial vertex** of the edge $(a, b),$ and the vertex $b$ is called the **terminal vertex** of this edge.

An edge of the form $(a, a)$ is represented using an arc from the vertex a back to itself. Such an edge is called a **loop**.

## Closures of Relations

A computer network has data centers in Boston, Chicago, Denver, Detroit, New York, and San Diego. There are direct, one-way telephone lines from Boston to Chicago, from Boston to Detroit, from Chicago to Detroit, from Detroit to Denver, and from New York to San Diego. 

Let $R$ be the relation containing $(a, b)$ if there is a telephone line from the data center in $a$ to that in $b$. How can we determine if there is some (possibly indirect) link composed of one or more telephone lines from one center to another? Because not all links are direct, such as the link from Boston to Denver that goes through Detroit, $R$ cannot be used directly to answer this.
In the language of relations, $R$ is not transitive, so it does not contain all the pairs that can be linked. As we will show in this section, we can find all pairs of data centers that have a link by constructing a transitive relation $S$ containing $R$ such that $S$ is a subset of every transitive relation containing $R$. Here, $S$ is the smallest transitive relation that contains $R$. This relation is called the **transitive closure** of $R$.

#### Different Types of Closures

If $R$ is a relation on a set $A,$ it may or may not have some property $P,$ such as reflexivity, symmetry, or transitivity. When $R$ does not enjoy property $P,$ we would like to find the smallest relation $S$ on $A$ with property $P$ that contains $R$.

* **Definition**:
  If $R$ is a relation on a set $A,$ then the **closure** of $R$ with respect to $P,$ if it exists, is the relation $S$ on $A$ with property $P$ that contains $R$ and is a subset of every subset of $A \times A$ containing $R$ with property $P$.

#### Paths in Directed Graphs

We will see that representing relations by directed graphs helps in the construction of transitive closures. A path in a directed graph is obtained by traversing along edges (in the same direction as indicated by the arrow on the edge).

* **Definition**:
  A path from $a$ to $b$ in the directed graph $G$ is a sequence of edges $(x_0, x_1), (x_1, x_2), (x_2, x_3), \ldots, (x_{n - 1}, x_n)$ in $G,$ where $n$ is a nonnegative integer, and $x_0 = a$ and $x_n = b,$ that is, a sequence of edges where the terminal vertex of an edge is the same as the initial vertex in the next edge in the path. 
  This path is denoted by $x_0, x_1, x_2, \ldots, x_{n - 1}, x_n$ and has length $n$. We view the empty set of edges as a path of length zero from $a$ to $a$. A path of length $n \geqslant 1$ that begins and ends at the same vertex is called a **circuit** or **cycle**.

A path in a directed graph can pass through a vertex more than once. Moreover, an edge in a directed graph can occur more than once in a path.

* **Theorem**:
  Let $R$ be a relation on a set $A$. There is a path of length $n,$ where $n$ is a positive integer, from $a$ to $b$ if and only if $(a, b) \in R^n$.

#### Transitive Closures

We now show that finding the transitive closure of a relation is equivalent to determining which pairs of vertices in the associated directed graph are connected by a path.

* **Definition**:
  Let $R$ be a relation on a set $A$. The **connectivity relation** $R^\ast$ consists of the pairs $(a, b)$ such that there is a path of length at least one from $a$ to $b$ in $R$.
  
Because $R^n$ consists of the pairs $(a, b)$ such that there is a path of length $n$ from $a$ to $b,$ it follows that $R^\ast$ is the union of all the sets $R^n$. In other words, $$\begin{align*}
& R^{\ast} = \bigcup_{n = 1}^{\infty} R^n. &
\end{align*}$$The connectivity relation is useful in many models.

* **Theorem**:
  The transitive closure of a relation $R$ equals the connectivity relation $R^\ast$.

Now that we know that the transitive closure equals the connectivity relation, we turn our attention to the problem of computing this relation. We do not need to examine arbitrarily long paths to determine whether there is a path between two vertices in a finite directed graph.

* **Lemma**:
  Let $A$ be a set with $n$ elements, and let $R$ be a relation on $A$. If there is a path of length at least one in $R$ from $a$ to $b,$ then there is such a path with length not exceeding $n$. Moreover, when $a \ne b,$ if there is a path of length at least one in $R$ from $a$ to $b,$ then there is such a path with length not exceeding $n - 1$.

* **Theorem**:
  Let $M_R$ be the zero–one matrix of the relation $R$ on a set with $n$ elements. Then the zero–one matrix of the transitive closure $R^\ast$ is $$\begin{align*}
  & M_{R^\ast} = M_R \lor M^{[2]}_R  \lor M^{[3]}_R \lor \ldots \lor M^{[n]}_R.
 \end{align*}$$
 Now let's look at the naive algorithm for computing the transitive closures

* **Algorithm**: A Procedure for Computing the Transitive Closure.
  **procedure** $transitive \, closure$ ($M_R$ : zero–one $n \times n$ matrix)
  $A := M_R$
  $B := A$
  for $i := 2$ to $n$
  $\qquad$$A := A \odot M_R$
  $\qquad$$B := B \lor A$
  return $B$ $\{B$ is the zero–one matrix for $R^\ast\}$

The next section describes a more efficient algorithm for finding transitive closures.

#### Warshall's Algorithm

Warshall's algorithm is an efficient method for computing the transitive closure of a relation. Algorithm above can find the transitive closure of a relation on a set with $n$ elements using $2n^3 (n - 1)$ bit operations. However, the transitive closure can be found by Warshall's algorithm using only $2n^3$ bit operations.

Suppose that $R$ is a relation on a set with $n$ elements. Let $v_1, v_2, \ldots, v_n$ be an arbitrary listing of these $n$ elements. The concept of the **interior vertices** of a path is used in Warshall's algorithm. If $a, x_1, x_2, \ldots, x_{m - 1}, b$ is a path, its interior vertices are $x_1, x_2, \ldots, x_{m - 1},$ that is, all the vertices of the path that occur somewhere other than as the first and last vertices in the path.

* **Lemma**:
  Let $W_k = [w^{[k]}_{ij}]$ be the zero–one matrix that has a $1$ in its $(i, j)$th position if and only if there is a path from $v_i$ to $v_j$ with interior vertices from the set $\{v_1, v_2, \ldots, v_n\}$. Then $$\begin{align*}
  & w^{[k]}_{ij} = w^{[k - 1]}_{ij} \lor \left( w^{[k - 1]}_{ik} \land w^{[k - 1]}_{kj} \right). &
  \end{align*}$$whenever $i, j,$ and $k$ are positive integers not exceeding $n$.

* **Algorithm**: Warshall Algorithm.
  **procedure** $Warshall$ ($M_R : n \times n$ zero–one matrix) 
  $W := M_R$
  for $k := 1$ to $n$
  $\quad$for $i := 1$ to $n$
  $\qquad$for $j := 1$ to $n$
  $\qquad$$w_{ij} := w_{ij} \lor (w_{ik} \land w_{kj})$
  return $W \, \{W = [w_{ij}]$ is $M_{R^\ast}\}$

## Equivalence Relations

In this section we will study relations with a particular combination of properties that allows them to be used to relate objects that are similar in some way.

* **Definition**:
  A relation on a set A is called an **equivalence relation** if it is reflexive, symmetric, and transitive.

* **Definition**:
  Two elements $a$ and $b$ that are related by an equivalence relation are called **equivalent**. The notation $a \sim b$ is often used to denote that $a$ and $b$ are equivalent elements with respect to a particular equivalence relation.

#### Equivalence Classes

Let $A$ be the set of all students in your school who graduated from high school. Consider the relation $R$ on $A$ that consists of all pairs $(x, y),$ where $x$ and $y$ graduated from the same high school. Given a student $x,$ we can form the set of all students equivalent to $x$ with respect to $R$. This set consists of all students who graduated from the same high school as $x$ did. This subset of $A$ is called an *equivalence class* of the relation.

* **Definition**:
  Let $R$ be an equivalence relation on a set $A$. The set of all elements that are related to an element a of $A$ is called the **equivalence class** of $a$. The equivalence class of $a$ with respect to $R$ is denoted by $[a]_R$. When only one relation is under consideration, we can delete the subscript $R$ and write $[a]$ for this equivalence class.

In other words, if $R$ is an equivalence relation on a set $A,$ the equivalence class of the element $a$ is $[a]_R = \{s \mid (a, s) \in R\}$. If $b \in [a]_R,$ then b is called a **representative** of this equivalence class.

#### Equivalence Classes and Partitions

Let $R$ be a relation on the set $A$. Theorem below shows that the equivalence classes of two elements of $A$ are either identical or disjoint.

* **Theorem**:
  Let $R$ be an equivalence relation on a set $A$. These statements for elements $a$ and $b$ of $A$ are equivalent:
  * $a \mathrel{R} b$.
  * $[a] = [b]$.
  * $[a] \cap [b] \ne \phi$.

* **Theorem**:
  Let $R$ be an equivalence relation on a set $S$. Then the equivalence classes of $R$ form a **partition** of $S$. Conversely, given a partition $\{A_i \mid i \in I\}$ of the set $S,$ there is an equivalence relation $R$ that has the sets $A_i, \, i \in I,$ as its equivalence classes.

## Partial Orderings

We often use relations to order some or all of the elements of sets. For instance, we order words using the relation containing pairs of words $(x, y),$ where $x$ comes before $y$ in the dictionary. When we add all of the pairs of the form $(x, x)$ to these relations, we obtain a relation that is reflexive, antisymmetric, and transitive. These are properties that characterize relations used to order the elements of sets.

* **Definition**:
  A relation $R$ on a set $S$ is called a **partial ordering** or **partial order** if it is reflexive, antisymmetric, and transitive. A set $S$ together with a partial ordering $R$ is called a **partially ordered set**, or **poset,** and is denoted by $(S, R)$. Members of $S$ are called **elements** of the poset.

In different posets different symbols such as $\leqslant, \subseteq,$ and $\mid,$ are used for a partial ordering. However, we need a symbol that we can use when we discuss the ordering relation in an arbitrary poset.
Customarily, the notation $a \preccurlyeq b$ is used to denote that $(a, b) \in R$ in an arbitrary poset $(S, R)$. This notation is used because the less than or equal to relation on the set of real numbers is the most familiar example of a partial ordering and the symbol $\preccurlyeq$ is similar to the $\leqslant$ symbol.

The notation $a \prec b$ denotes that $a \preccurlyeq b,$ but $a \ne b$. Also, we say "$a$ is less than $b$" or "$b$ is greater than $a$" if $a \prec b$. When $a$ and $b$ are elements of the poset $(S, \preccurlyeq),$ it is not necessary that either $a \preccurlyeq b$ or $b \preccurlyeq a$.

* **Definition**:
  The elements $a$ and $b$ of a poset $(S, \preccurlyeq)$ are called **comparable** if either $a \preccurlyeq b$ or $b \preccurlyeq a$. When $a$ and $b$ are elements of $S$ such that neither $a \preccurlyeq b$ nor $b \preccurlyeq a,$ $a$ and $b$ are called **incomparable**.

The adjective "partial" is used to describe partial orderings because pairs of elements may be incomparable. When every two elements in the set are comparable, the relation is called a **total ordering**.

* **Definition**:
  If $(S, \preccurlyeq)$ is a poset and every two elements of $S$ are comparable, $S$ is called a **totally ordered** or **linearly ordered** set, and $\preccurlyeq$ is called a **total order** or a **linear order**. A totally ordered set is also called a **chain**.

* **Definition**:
  $(S, \preccurlyeq)$ is a **well-ordered set** if it is a poset such that $\preccurlyeq$ is a total ordering and every nonempty subset of $S$ has a least element.

Here is the important theorem that we should prove.

* **Theorem**: The Principle of Well-Ordered Induction
  Suppose that $S$ is a well-ordered set. Then $P(x)$ is true for all $x \in S,$ if
  *Inductive Step*:
  For every $y \in S,$ if $P(x)$ is true for all $x \in S$ with $x \prec y,$ then $P(y)$ is true.
  
  **Proof**:
  Suppose it is not the case that $P(x)$ is true for all $x \in S$. Then there is an element $y \in S$ such that $P(y)$ is false. Consequently, the set $A = \{x \in S \mid P(x)$ is false$\}$ is nonempty. Because $S$ is well-ordered, $A$ has a least element $a$. By the choice of $a$ as a least element of $A,$ we know that $P(x)$ is true for all $x \in S$ with $x \prec a$. This implies by the inductive step $P(a)$ is true. This contradiction shows that $P(x)$ must be true for all $x \in S$.

#### Maximal and Minimal Elements

In general, we can represent a finite poset $(S, \preccurlyeq)$ using this procedure:

* Start with the directed graph for this relation. Because a partial ordering is reflexive, a loop $(a, a)$ is present at every vertex $a$. Remove these loops.
* Next, remove all edges that must be in the partial ordering because of the presence of other edges and transitivity. That is, remove all edges $(x, y)$ for which there is an element $z \in S$ such that $x \prec z$ and $z \prec x$.
* Finally, arrange each edge so that its initial vertex is below its terminal vertex. Remove all the arrows on the directed edges, because all edges point "upward" toward their terminal vertex.

These steps are well defined, and only a finite number of steps need to be carried out for a finite poset. The resulting diagram is called the **Hasse diagram** of $(S, \preccurlyeq)$.

Let $(S, \preccurlyeq)$ be a poset. We say that an element $y \in S$ **covers** an element $x \in S$ if $x \prec y$ and there is no element $z \in S$ such that $x \prec z \prec y$. The set of pairs $(x, y)$ such that $y$ covers $x$ is called the **covering relation** of $(S, \preccurlyeq)$. 

From the description of the Hasse diagram of a poset, we see that the edges in the Hasse diagram of $(S, \preccurlyeq)$ are upwardly pointing edges corresponding to the pairs in the covering relation of $(S, \preccurlyeq)$. Furthermore, we can recover a poset from its covering relation, because it is the reflexive transitive closure of its covering relation. This tells us that we can construct a partial ordering from its Hasse diagram.

Elements of posets that have certain extremal properties are important for many applications. An element of a poset is called **maximal** if it is not less than any element of the poset. That is, $a$ is maximal (**greatest element**) in the poset $(S, \preccurlyeq)$ if there is no $b \in S$ such that $a \prec b$. Similarly, an element of a poset is called **minimal** if it is not greater than any element of the poset. That is, $a$ is minimal (**least element**) if there is no element $b \in S$ such that $b \prec a$.

Maximal and minimal elements are easy to spot using a Hasse diagram. They are the "top" and "bottom" elements in the diagram.

Sometimes it is possible to find an element that is greater than or equal to all the elements in a subset $A$ of a poset $(S, \preccurlyeq)$. If $u$ is an element of $S$ such that $a \preccurlyeq u$ for all elements $a \in A,$ then $u$ is called an **upper bound** of $A$. Likewise, there may be an element less than or equal to all the elements in $A$. If $l$ is an element of $S$ such that $l \preccurlyeq a$ for all elements $a \in A,$ then $l$ is
called a **lower bound** of $A$.

The element $x$ is called the **least upper bound** of the subset $A$ if $x$ is an upper bound that is less than every other upper bound of $A$. That is, $x$ is the least upper bound of $A$ if $a \preccurlyeq x$ whenever $a \in A,$ and $x \preccurlyeq z$ whenever $z$ is an upper bound of $A$. Similarly, the element $y$ is called the **greatest lower bound** of $A$ if $y$ is a lower bound of $A$ and $z \preccurlyeq y$ whenever $z$ is a lower bound of $A$. The greatest lower bound and least upper bound of a subset $A$ are denoted by $glb(A)$ and $lub(A),$ respectively.

#### Lattices

A partially ordered set in which every pair of elements has both a least upper bound and a greatest lower bound is called a **lattice**. Lattices have many special properties. Furthermore, lattices are used in many different applications such as models of information flow and play an important role in Boolean algebra.

**Topological Sorting**:
Suppose that a project is made up of 20 different tasks. Some tasks can be completed only after others have been finished. How can an order be found for these tasks? To model this problem we set up a partial order on the set of tasks so that $a \prec b$ if and only if $a$ and $b$ are tasks where $b$ cannot be started until $a$ has been completed. To produce a schedule for the project, we need to produce an order for all $20$ tasks that is compatible with this partial order.

We begin with a definition. A total ordering $\preccurlyeq$ is said to be compatible with the partial ordering $R$ if a $\preccurlyeq b$ whenever $a \mathrel{R} b$. Constructing a compatible total ordering from a partial ordering is called **topological sorting**.

* **Lemma**:
  Every finite nonempty poset $(S, \preccurlyeq)$ has at least one minimal element.

We will use this lemma to form an algorithm for this task.

* **Algorithm**: Topological Sorting.
  **procedure** $topological \space sort$ ($(S, \preccurlyeq)$: finite poset)
  $k := 1$
  while $S \ne \phi$
  $\quad$$a_k := a$ minimal element of $S \, \{$such an element exists by Lemma$\}$
  $\quad$$S := S - {a_k}$
  $\quad$$k := k + 1$
  return $a_1, a_2, \ldots, a_n \, \{a_1 , a_2, \ldots, a_n$ is a compatible total ordering of $S\}$


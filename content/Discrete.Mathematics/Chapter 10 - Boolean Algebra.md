# Boolean Algebra

Claude Shannon showed how the basic rules of logic, first given by George Boole in 1854 in his "*The Laws of Thought*", could be used to design circuits. These rules form the basis for Boolean algebra. In this chapter we develop the basic properties of Boolean algebra.

## Boolean Functions

Boolean algebra provides the operations and the rules for working with the set $\{0, 1\}$. Electronic switches can be studied using this set and the rules of Boolean algebra. The three operations in Boolean algebra that we will use most are the Boolean sum, the Boolean product, and complementation. 
The complement of an element, denoted with a bar, is defined by $\overline{0} = 1$ and $\overline{1} = 0$. The Boolean sum, denoted by $+$ or by $OR,$ has the same values as standard logical 'or' ($\lor$) function if we treat $1$ as True and $0$ as False. Similar results can be obtained for the Boolean product ($\cdot$) which is identical to logical 'and' ($\land$).

#### Boolean Expressions and Boolean Functions

Let $B = \{0, 1\}$. Then $B^n = \{(x_1, x_2, \ldots, x_n) \mid x_i \in B$ for $1 \leqslant i \leqslant n\}$ is the set of all possible $n$-tuples of $0$s and $1$s. The variable $x$ is called a **Boolean variable** if it assumes values only from $B,$ that is, if its only possible values are $0$ and $1$. A function from $B^n$ to $B$ is called a Boolean function of **degree** $n$.

Boolean functions can be represented using expressions made up from variables and Boolean operations. The Boolean expressions in the variables $x_1, x_2, \ldots, x_n$ are defined recursively as $0, 1, x_1, x2, \ldots, x_n$ are Boolean expressions; if $E_1$ and $E_2$ are Boolean expressions, then $\overline{E_1}, \, (E_1 E2_),$ and $(E_1 + E_2)$ are Boolean expressions.

Boolean functions $F$ and $G$ of $n$ variables are equal if and only if $F(b_1, b_2, \ldots, b_n) = G(b_1, b_2, \ldots, b_n)$ whenever $b_1, b_2, \ldots, b_n$ belong to $B$. Two different Boolean expressions that represent the same function are called **equivalent**. For instance, the Boolean expressions $xy, xy + 0,$ and $xy \cdot 1$ are equivalent.

The **complement** of the Boolean function $F$ is the function $\overline{F},$ where $F(x_1, \ldots, x_n) = \overline{F(x_1, \ldots, x_n)}$. Let $F$ and $G$ be Boolean functions of degree $n$. The Boolean sum $F + G$ and the Boolean product $FG$ are defined by $$\begin{align*}
& (F + G)(x_1, \ldots, x_n) = F(x_1, \ldots, x_n) + G(x_1, \ldots, x_n),& \\
& (FG)(x_1, \ldots, x_n) = F(x_1, \ldots, x_n)G(x_1, \ldots, x_n).&
\end{align*}$$

* **Definition**:
  A **Boolean algebra** is a set $B$ with two binary operations $\lor$ and $\land,$ elements $0$ and $1,$ and a unary operation $\space \bar{} \space$ such that these properties hold for all $x, y,$ and $z$ in $B$:
  
  * Identity laws
    $x \lor 0 = x$
    $x \land 1 = x$
  
  * Complement laws
    $x \lor \overline{x} = 1$
    $x \land \overline{x} = 0$
    
  * Associative laws
    $(x \lor y) \lor z = x \lor (y \lor z)$
    $(x \land y) \land z = x \land (y \land z)$
    
  * Commutative laws
    $x \lor y = y \lor x$
    $x \land y = y \land x$
    
  * Distributive laws
    $x \lor (y \land z) = (x \lor y) \land (x \lor z)$
    $x \land (y \lor z) = (x \land y) \lor (x \land z)$

## Representing Boolean Functions

Two important problems of Boolean algebra will be studied in this section. The first problem is: Given the values of a Boolean function, how can a Boolean expression that represents this function be found? The second problem is: Is there a smaller set of operators that can be used to represent all Boolean functions?

#### Sum-of-Products Expansions

* **Definition**:
  A **literal** is a Boolean variable or its complement. A **minterm** of the Boolean variables $x_1, x_2, \ldots, x_n$ is a Boolean product $y_1 y_2 \ldots y_n,$ where $y_i = x_i$ or $y_i = \overline{x_i}$. Hence, a minterm is a product of $n$ literals, with one literal for each variable.

By taking Boolean sums of distinct minterms we can build up a Boolean expression with a specified set of values. In particular, a Boolean sum of minterms has the value $1$ when exactly one of the minterms in the sum has the value $1$. It has the value $0$ for all other combinations of values of the variables. 
Consequently, given a Boolean function, a Boolean sum of minterms can be formed that has the value 1 when this Boolean function has the value $1,$ and has the value $0$ when the function has the value $0$. The minterms in this Boolean sum correspond to those combinations of values for which the function has the value $1$. The sum of minterms that represents the function is called the **sum-of-products expansion** or the **disjunctive normal form** of the Boolean function.

It is also possible to find a Boolean expression that represents a Boolean function by taking a Boolean product of Boolean sums. The resulting expansion is called the **conjunctive normal form** or **product-of-sums expansion** of the function. These expansions can be found from sum-of-products expansions by taking duals.

# Dynamic Programming

The idea behind dynamic programming is to store the solution to each subproblem rather than recomputing it.

### Rod cutting
Serling Enterprises buys long steel rods and cuts them into shorter rods, which it then sells. Each cut is free. The management of Serling Enterprises wants to know the best way to cut up the rods.  

Serling Enterprises has a table giving, for $i=1,2,\dots,$, the price $p_i$ in dollars that they charge for a rod of length $i$ inches. The length of each rod in inches is always an integer. 

| length $i$  | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  |
| ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| price $p_i$ | 1   | 5   | 8   | 9   | 10  | 17  | 17  | 20  | 24  | 30  |
Given a rod of length $n$ inches and a table of prices $p_{i}$ for $i=1,2,\dots,n$, determine the maximum revenue $r_n$ obtainable by cutting up the rod and selling the pieces.

If an optimal solution cuts the rod into k pieces, for some $1\leq k \leq n$ , then an optimal decomposition
$$
n = i_{1}+i_{2}+\dots+i_{k}
$$
we can express the revenue $r_{n}$ for $n\geq 1$ in terms of optimal revenues from shorter rods:
$$
r_{n} = \max \{ p_{n}, r_{1}+ r_{nn-1}, r_{2} + r_{n-2}, \dots, r_{n-1} +r_{1}  \}
$$
where $p_{n}$ corresponds to making no cuts at all and selling the rod of length $n$ as is. 
The other $n-1$ arguments to max correspond to the maximum revenue obtained by making an initial cut of the rod into two pieces of size $i$ and $n -i$, for each $\{ i=1, 2,  \dots ,  n-1 \}$, and then optimally cutting up those pieces further, obtaining revenues $r_i$ and $r_{n-i}$$ from those two pieces. Since you don’t know ahead of time which value of i optimizes revenue, you have to consider all possible values for i $and$ pick the one that maximizes revenue. You also have the option of picking no $i$ at all if the greatest revenue comes from selling the rod uncut.
we obtain the following simpler version of equation . 
$$
r_{n} =\max \{ p_{i}+r_{n-i} : 1\leq i\leq n \}
$$

>[!tldr] $\text{CUT-ROD}$
>if $n == 0$  
>$\qquad$ return $0$  
>$q = -\infty$  
>for $i = 1$ to $n$  
>$\qquad q = \max\{ q,p[i]+ \text{CUT-ROD}(p, n-i) \}$  
>return $q$  

If you code up CUT-ROD in your favorite programming language and run it on your computer, you’ll find that once the input size becomes moderately large, your program takes a long time to run. For $n = 40$, your program may take several minutes and possibly more than an hour. For large values of n, you’ll also discover that each time you increase n by 1, your program’s running time approximately doubles. Why is **CUT-ROD** so inefficient? The problem is that **CUT-ROD** calls itself recursively over and over again with the same parameter values, which means that it solves the same subproblems repeatedly.

The running time of **ROD-CUT** is $T(n) = 2^{n}$.

Using dp for optimal rod cutting :
We can use dp to convert `CUT-ROD` into an efficient algorithm.

The dynamic-programming method works as follows. Instead of solving the same subproblems repeatedly, as in the naive recursion solution, arrange for each subproblem to be solved only once. There’s actually an obvious way to do so: the first time you solve a subproblem, save its solution. If you need to refer to this subproblem’s solution again later, just look it up, rather than recomputing it.

Saving subproblem solutions comes with a cost: the additional memory needed to store solutions. Dynamic programming thus serves as an example of a **time -memory trade-off**.

There are two ways to implement a dynamic -programming approach. 
The first is **top-down** with **memoization**.  In this approach, you write the procedure recursively in a natural manner, but modified to save the result of each subproblem (usually in an array or hash table). The procedure now ûrst checks to see whether it has previously solved this subproblem. If so, it returns the saved value, saving further computation at this level. If not, the procedure computes the value in the usual manner but also saves it.

 >[!tldr] $\text{MEMOIZED-CUT-ROD}(p, n)$
>let $r[0:n]$ be a new array  $\qquad\qquad$ // will remember solution values in r  
>for $i=0$ to $n$  
>$\qquad r[i] = -\infty$  
>return $\text{MEMOIZED-CUT-ROD-AUX}(p,n,r)$  

>[!tldr] $\text{MEMOIZED-CUT-ROD-AUX}(p,n,r)$
>if $r[n] \geq 0$ $\qquad\qquad\qquad\qquad\qquad\quad$ // already have a solution for length n?  
>$\qquad$return $r[n]$  
>if $n==0$   
>$\qquad q=0$  
>else $q=-\infty$  
>$\qquad$for $i=1$ to $n$ $\qquad\qquad\qquad\qquad$ // i is the position of the first cut  
>$\qquad\qquad q = \max\{ q,p[i]+\text{MEMOIZED-CUT-ROD-AUX}(p,n-i,r) \}$  
>$r[n]=q$ $\qquad\qquad\qquad\qquad\qquad\qquad$              // remembers the solution value for length n  
>return $q$  

The second approach is the **bottom-up method** or also known as **tabulation**. This approach typically depends on some natural notion of the "size" of a subproblem, such that solving any particular subproblem depends only on solving "smaller" subproblems. Solve the subproblems in size order, smallest first , storing the solution to each subproblem when it is first solved. In this way, when solving a particular subproblem, there are already saved solutions for all of the smaller subproblems its solution depends upon. You need to solve each subproblem only once, and when you first see it, you have already solved all of its prerequisite subproblems.

>[!tldr] $\text{BOTTOM-UP-CUT-ROD}$
>let $r[0:n]$ be a new array $\qquad\qquad\qquad$ // will remember solution values in r  
>$r[0] = 0$  
>for $j = 1$ to $0$ $\qquad\qquad\qquad\qquad\qquad\quad$ // for increasing rod   length $j$  
>$\qquad q= -\infty$  
>$\qquad$ for $i=1$ to $j$ $\qquad\qquad\qquad\qquad\quad$ // i is the position of the first cut  
>$\qquad\qquad q= \max\{ q,p[i]+r[j-i] \}$  
>$\qquad r[j]=q$ $\qquad\qquad\qquad\qquad\qquad\qquad$ // remember the solution value for length $j$  
>return $r[n]$  

The running time of `BOTTOM-UP-CUT-ROD` is $\Theta(n^{2})$.
### Matrix-chain multiplication
Given a sequence (chain) $\langle A_{1},A_{2},\dots, A_{n}\rangle$ of $n$ matrices to be multiplied, where the matrices aren’t necessarily square, the goal is to compute the product 
$$
A_{1}A_{2}A_{3}\dots A_{n}
$$
Matrix multiplication is associative, and so all parenthesizations yield the same product. A product of matrices if **fully parenthesized** if it is either a single matrix or the product of two fully parenthesized matrix products, surrounded by parentheses. 
A chain of matrices can be parenthesize in five distinct ways -

$$
\begin{align}
(A_{1}(A_{2}(A_{3}A_{4}))) \\
(A_{1}((A_{1}A_{3})A_{4})) \\
((A_{1}A_{2})(A_{3}A_{4})) \\
((A_{1}(A_{2}A_{3})) A_{4}) \\
(((A_{1}A_{1})A_{3})A_{4})
\end{align}
$$
parenthesization can have dramatic impact on the cost of evaluating the product. 
To illustrate the different costs incurred by different parenthesizations of a matrix product, consider a chain $\left< A_{1}, A_{2},A_{3} \right>$ of three matrices. Suppose the dimensions of the matrices are $10\times 100 \times, 100 \times 5$ and $5\times 50$. 
Multiplying according to the parenthesization $((A_{1}A_{1}) A_{3})$ performs $10 \cdot 100 \cdot 5 = 5000$ scalar multiplication for $A_{1}A_{2}$ plus another $10 \cdot 5 \cdot 50 = 2500$ for for multiplying with $A_{3}$, for a total of $7500$ scalar multiplications. 

Whereas multiplying according to the alternative parenthesization $(A_{1}(A_{2}A_{3}))$ takes $50000$ scalar multiplications. Thus computing the product according to the first parenthesization is 10 times faster.

>[!tldr] $\text{RECTANGULAR-MATRIX-MULTIPLY}(A,B,C,p,q,r)$
>for $i=1$ to $p$  
>$\qquad$for $j=1$ to $r$  
>$\qquad\qquad$for $k=1$ to $q$  
>$\qquad\qquad\qquad c_{ij}=c_{ij}+a_{ik}\cdot b_{kj}$  

##### Counting the number of parenthesizations
Denote the number of alternative parenthesizations of a sequence of $n$ matrices by $P(n)$. When $n=1$ , the seq consists of just one matrix, and therefore only one way to parenthesize the matrix product. when $n\geq{2}$, a fully parenthesized matrix product is the product of two fully parenthesized matrix subproducts , and split between the two subproducts may occu between kth and $(k+1)$st matrices for any $k=1,2,\dots, n-1$ Thus we obtain the recurrence 
$$
P(n) = \begin{cases}
1 & if \space n=1 \\
\sum_{k=1}^{n-1}P(k)(P(n-k)) & if\space n\geq 2
\end{cases}
$$
The solution to this recurrence is $\Omega(2^{n})$. Hence it is an exponential algorithm.

##### Applying dynamic programming
**Step 1 : The structure of an optimal parenthesization**
In this first step of dp, you find the optimal substructure and then use it to construct an optimal solution to the problem from optimal solution to subproblems. 

Let $A_{i:j}$ denote the matrix the results from evaluting the product $A_{i}A_{i+1}.. A_{j}$ if the problem is nontrivial, that is $i<j$ , then to parenthesize the product the product must split between $A_{k}$ and $A_{k+1}$, and then multiply them together to produce the final product $A_{i:j}$.
The cost of parenthesizing this way is the cost of computing the matrix $A_{i:k}$ plus the cost of computing $A_{k+1:j}$, plus the cost of multiplying them together.

**Step 2 : A recursive solution**

$$
m[i,j] = \begin{cases}
0 & \text{if } i = j \\
\min \{ m[i,k]+ ,[k-1, j]+p_{i-1} p_{k}p_{j}: i\leq k < j \} & \text{i < j}\\
\end{cases}
$$

**Step 3 : Computing the optimal costs**
At this point, we can write a recursive algorithm based on recurrence to compute the  minimum cost $m[1, n]$ for multiplying $A_{1} \cdot A_{2} \cdot A_{n}$ but the recursive algorithm takes exponential time. 
Instead of computing solution to recurrence recursively, we shall compute the optimal cost by using tabular, bottom-up approach.

>[!tldr] $\text{MATRIX-CHAIN-ORDER}(p, n)$
>let $m[1:n], 1:n$ and $s[1:n-1, 2:n]$ be new tables  
>for $i=1$ to $n$  
>$\qquad m[i,i]=0$  
>for $l=2$ to $n$  
>$\qquad$for $i=1$ to $n-l+1$  
>$\qquad\qquad j=i+l-1$  
>$\qquad\qquad m[i,j]=\infty$  
>$\qquad\qquad$for $k=i$ to $j-1$  
>$\qquad\qquad\qquad q = m[i,k]+m[k+1, j]+p_{i-1}p_{k}p_{j}$  
>$\qquad\qquad\qquad$if $q<m[i,j]$  
>$\qquad\qquad\qquad\qquad m[i,j]=q$  
>$\qquad\qquad\qquad\qquad s[i,j]=k$  
>return $m$ and $s$  

The running time of `MATRIX-CHAIN-ORDER` is $O(n^{3})$ . It also requires $\Theta(n^{2})$ space to store the m and s tables. Thus, it is much more effcient than the exponential time method of enumerating all possible parenthesizations and each each one.

**Step 4 Constructing an optimal solution**

>[!tldr] $\text{PRINT-OPTIMAL-PARENS}(s, i, j)$
>if $i ==j$  
>$\qquad print(\text{"A"}_{i})$  
>else $print\text{"("}$  
>$\qquad\text{PRINT-OPTIMAL-PARENS}(s,i, s[i,j])$  
>$\qquad\text{PRINT-OPTIMAL-PARENS}(s, s[i,j]+1, j)$  
### Elements of dynamic programming
There are two ingredients that an optimization problem must have in order for dynamic programming to apply.
##### 1. Optimal substructure
The first step in solving an optimization problem by dynamic programming is to characterize the structure of an optimal solution. When a problem exhibits optimal substructure that, that gives you a good clue that dp might apply. Dynamic programming builds an optimal an optimal solution to the problem from optimal solutions to subproblems. 
##### 2. Overlapping subproblems
The second ingredient that an optimization problem must have for dp to appy is that the space for subproblems must be "small". When a recursive algo revisits the same problem repeatedly, we say that the optimization problem has overlapping subproblems. Dp typically take advantage of overlapping subproblem by solving each subproblem once and then storing the solution in a table where it can be looked up when needed.
### Longest common subsequence
Given a sequence $X= \langle x_{1},x_{2},\dots x_{n} \rangle$, another sequence $Z= \langle z_{1},z_{2},\dots, z_{k}\rangle$ is a *subsequence* of $X$ if there exists a strictly increasing sequence $\langle i_{1}, i_{2}, \dots i_{k}\rangle$ of indices of $X$ such that for all $j=1,2,\dots,k,$ we have $x_{ij}=z_{j}$ .

Given two sequence $X$ and $Y$ , we say that a sequence $Z$ is a *common subsequence* of $X$ and $Y$ is $X$ is subsequence of both $X$ and $Y$.

In the *longest-common-subsequence problem* , the input is two sequences $X=\langle x_{1},x_{2},\dots, x_{m}\rangle$ and $Y = \langle y_{1},y_{2},\dots, y_{n} \rangle$ , and the goal is to find a maximum-length common subsequence of $X$ and $Y$.

###### Step 1: Characterizing a longest common subsequence
###### Step 2: A recursive solution
###### Step 3: Computing the length of an LCS

>[!tldr] $\text{LCS-LENGTH}(X, Y,m, n)$
>let $b[1:m, 1:n]$ and $c[0:m, 0:n]$ be new tables  
>for $i=1$ to $m$  
>$\qquad c[i,0]=0$  
>for $j=0$ to $n$  
>$\qquad c[0,j]= 0$  
>for $i=1$ to $m$  
>$\qquad$ for $j=1$ to $n$  
>$\qquad\qquad$if $x_{i} ==y_{i}$  
>$\qquad\qquad\qquad c[i,j]= c[i-1, j-1]+1$  
>$\qquad\qquad\qquad b[i,j]=\text{`` }{\nwarrow}\text{"}$  
>$\qquad\qquad$elseif $c[i-1,j] \geq c[i,j-1]$  
>$\qquad\qquad\qquad c[i,j]= c[i-1,j]$  
>$\qquad\qquad\qquad b[i,j]=\text{``}\uparrow\text{"}$  
>$\qquad\qquad$else $c[i,j]=c[i,j-1]$  
>$\qquad\qquad\qquad b[i,j]=\text{``}\leftarrow\text{"}$  
>return $c$ and $b$  

>[!tldr] $\text{PRNIT-LCS}(b,X, i,j)$
>if $i==0$ or $j==0$  
>$\qquad$return   
>if $b[i,j]==\text{``}\nwarrow\text{"}$  
>$\qquad\text{PRINT-LCS}(b,X,i-1, j-1)$  
>$\qquad$print $x_{i}$  
>elseif $b[i,j]==\text{``}\uparrow\text{"}$  
>$\qquad\text{PRINT-LCS}(b,X,i-1, j)$  
>else $\text{PRINT-LCS}(b,X,i,j-1)$  

###### Step 4: Constructing an LCS

### Optimal binary search trees


___
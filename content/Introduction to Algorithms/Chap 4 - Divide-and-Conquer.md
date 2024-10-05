## Divide-and-Conquer
A divide and conquer algorithm breaks down a large problem into smaller subproblems, which themselves may b broken down into even smaller subproblems, and so forth. The recursion **bottoms out** when it reaches a base case and subproblem is small enough to solve directly without further recursing.
___
### Recurrences
A recurrence is an equation that describes a function in terms of its value on the other, typically smaller, arguments. Recurrences go hand in hand with DAC method because they give us a natural way to characterize the running times of recursive algorithms mathematically.
The general form of a recurrence is an equation or inequality that describes a function over the integers or reals using the function itself. It contains two or more cases, depending on the argument. If a case involves the recursive invocation of the function on different inputs it is a **recursive case**. If a case does not involve a recursive invocation it is a **base case**. The recurrence is **well defined** if there is at least one function that satisfies it and **ill defined** otherwise.
___
#### Algorithmic recurrences
A recurrence $T(n)$ is algorithmic if for every sufficiently large threshold constant $n_0 > 0$ the following two properties hold:
1. For all $n<n_0$, we have $T(n) = \Theta (1)$.
2. For all $n \ge n_0$ every path of recursion terminates in a defined base case withing a finite number of recursive invocations.
___
#### Conventions for recurrences

>[!tip]
>whenever a recurrence is stated without an explicit base case, we assume that the recurrence is algorithmic.
#### Solving recurrences 
This chapter offers  four methods for solving recurrences :
- **Substitution Method**: This method involves making an educated guess about the form of the solution and then using mathematical induction to prove that the guess is correct. This technique is particularly useful for finding upper and lower bounds on the running time of an algorithm.
- **Recursion-Tree Method**: This method visualizes the recurrence as a tree, where each node represents a subproblem. The cost at each level of the tree is summed up to find the total cost of the algorithm. Even if not used to formally solve the recurrence, the recursion-tree method helps in intuitively understanding the structure of the recurrence.
- **Master Method**: This method provides a shortcut for solving recurrences of the form $T(n) = aT(n/b) + f(n)$. It categorizes the function $f(n)$ and determines the running time of the recurrence based on three cases. The master method is particularly useful for DAC algorithms with regular subproblem sizes and costs.
- **Akra-Bazzi Method**: This is a more general method for solving DAC recurrences that may not fit into the cases covered by the master method. It involves more advanced mathematical tools, such as calculus, and can handle more complex recurrences

Brute Force approach For solving Recurrence :

```C++
void test(int n){        // ----->  T(n)
	if(n > 0){           // ----->  c_1
		printf("%d", n); // ----->  c_2
		test(n-1);       // ----->  T(n-1)
	}
}
```
So the recurrence will be :
$T(n) = T(n-1) + c_1 + c_2$
We can also write it like this 
$$
T(n) = \begin{cases} 1 & \text{if }x = 0 \\
T(n-1) + C & \text{if } x > 0\end{cases}
$$
Solution :
$$
\begin{align}
& T(n) = T(n-1) + C \\
& T(n) = [ T(n-2) + C ] + C & \{T(n-1) = T(n-2 ) + C\} \\ 
& T(n) = T(n-2) + 2C \\
& T(n) = [T(n-3) + C] + 2C & \{T(n-2) = T(n-3) + C\} \\
& T(n) = T(n-3) + 3C \\
& \vdots & \\
& T(n) = T(n-k) + k * C \\
& T(n) = T(n-n) + n * C\\
& T(n) = T(0) + n * C \\
& T(n) = 1 + n * C & \{T(0) = 1\} \\
& T(n) = n
 \end{align}
$$
So the time complexity for this recurrence will be $O(n)$ 
___
#### Multiplying square matrices 
Le $A = (a_{ik})$ and $B = (b_{jk})$ be square $n \times n$ matrices. the product $C = A\cdot B$ is also an $n\times n$ matrix, where for $i,j = 1,2,3, \dots , n$ the $(i,j)$ entry of $C$ is given by
$$
C_{ij} = \sum_{k=1}^n {a_{ik} \cdot b_{kj}}
$$

Dense Matrices :$\rightarrow$ A matrix where most of entries are not 0.
Sparse Matrices :$\rightarrow$  A matrix where most of the entries are 0.

>[!tldr] $\text{MATRIX-MULTIPLY(A, B, C, n)}$
>for $i=1$ to $n$ $\qquad\qquad\qquad\qquad\qquad\space \space\space$// compute entries in each of n rows  
>$\qquad$ for $j=1$ to $n$ $\qquad\qquad\qquad\qquad$ // compute n entries in row i  
>$\qquad\qquad$ for $k = 1$ to $n$  
>$\qquad\qquad\qquad c_{ij} = c_{ij} +a_{ik} \cdot b_{kj}$ $\qquad\space$ // add in another term of equation  
#### A simple divide-and-conquer algorithm
for $n>1$, the divide step partitions the $n\times n$ matrices into four $n/2 \times n/2$ submatrices.
As with `Matrix-Multiply` we'll actually compute $C = C+ A\cdot B$ but to simplify the math behind it let's assume that C has been initialized to zero matrix, so that we are indeed computing $C = A\cdot B$
$$
\begin{matrix}
A = (\begin{matrix} A_{11} && A_{12} \\
A_{21} && A_{22} \end{matrix}), 

\qquad B = (\begin{matrix} B_{11} && B_{12} \\
B_{21} && B_{22} \end{matrix}) 

\qquad C = (\begin{matrix} C_{11} && C_{12} \\
C_{21} && C_{22} \end{matrix})
\end{matrix}
$$
then we can write the matrix product as 
$$
\begin{align*} 
(\begin{matrix} C_{11} && C_{12} \\
C_{21} && C_{22} \end{matrix})

 & = (\begin{matrix} A_{11} && A_{12} \\
A_{21} && A_{22} \end{matrix}) 

(\begin{matrix} B_{11} && B_{12} \\
B_{21} && B_{22} \end{matrix}) \\

& = (\begin{matrix} A_{11} \cdot B_{11} + A_{12} \cdot B_{21}  && A_{11} \cdot B_{12} + A_{12} \cdot B_{22} \\ A_{21} \cdot B_{22} + A_{22} \cdot B_{21}  && A_{21} \cdot B_{12} + A_{22} \cdot B_{22} \end{matrix})
\end{align*}
$$
Which corresponds to the equations
$C_{11} = A_{11}\cdot B_{11} + A_{12} \cdot B_{21} ,$
$C_{12} = A_{11}\cdot B_{12} + A_{12} \cdot B_{22} ,$
$C_{21} = A_{21}\cdot B_{11} + A_{22} \cdot B_{21} ,$
$C_{22} = A_{21}\cdot B_{12} + A_{22} \cdot B_{22} .$

>[!tldr] $\text{MATRIX-MULTIPLY-RECURSIVE(A, B, C, n)}$
>if $n == 1$ $\qquad\qquad$  
>// Base case.  
>$\qquad c_{11} = c_{11} + a_{11} \cdot b_{11}$  
>$\qquad$return  
>// Divide.  
>partition $A, B$ and $C$ into $n/2 \times n/2$ submatrices   
>$\qquad\qquad A_{11}\space, A_{12}\space, A_{21},\space A_{22};\space B_{11}\space,B_{12}\space,B_{21},\space B_{22};$    
>$\qquad\qquad \text{and}\space C_{11}\space,C_{12}\space, C_{21}\space,C_{22}; \space$ repectively  
>// Conquer.  
>$\text{MATRIX-MULTIPLY-RECURSIVE}(A_{11}, B_{11},C_{11}, n/2)$  
>$\text{MATRIX-MULTIPLY-RECURSIVE} A_{11}, B_{12},C_{12}, n/2)$  
>$\text{MATRIX-MULTIPLY-RECURSIVE}(A_{21}, B_{11},C_{21}, n/2)$  
>$\text{MATRIX-MULTIPLY-RECURSIVE}(A_{21}, B_{12},C_{22}, n/2)$  
>$\text{MATRIX-MULTIPLY-RECURSIVE}(A_{12}, B_{21},C_{11}, n/2)$  
>$\text{MATRIX-MULTIPLY-RECURSIVE}(A_{12}, B_{22},C_{12}, n/2)$  
>$\text{MATRIX-MULTIPLY-RECURSIVE}(A_{22}, B_{21},C_{21}, n/2)$  
>$\text{MATRIX-MULTIPLY-RECURSIVE}(A_{22}, B_{22},C_{22}, n/2)$  

#### Strassen's algorithm for matrix multiplication 
You might find it hard to imagine that any matrix multiplication algorithm could take less than $\Theta (n^3)$ time, since the natural definition of matrix multiplication requires $n^3$ scaler multiplications. In 1969 `V. Straseen` Published a remarkable recursive algorithm for multiplying $n \times n$ matrices which runs in $\Theta (n^{\text{lg} 7} )$ time. Since lg 7 = 2.8073549... , Strassen's algorithm runs in $O(n^{2.81})$ time. which is asymptotically better than $\Theta (n^3)$ .
The key to Strassen's method is to use the divide and conquer idea from the `MATRIX-MULTIPLY-RECURSIVE` procedure, but make the recursion tree less bushy.
Instead of performing eight recursive multiplications of $n/2 \times n/2$ matrices, Strassen's algorithm performs only seven.
Strassen's algorithm uses the divide and conquer method to compute $C = C + A \cdot B$ where $A, B$ and $C$ are all $n\times n$ matrices and n is an exact power of 2. Strassen's algorithm computes the four submatrices, $C_{11}, C_{12}, C_{21}, C_{22}$ of $C$ from equations. 
Let's see how it works:
1. If n = 1, the matrices each contain a single element. Perform a single scalar multiplication and a single scalar addition, of `MATRIX-MULTIPLY RECURSIVE`, taking $O(1)$ time, and return. Otherwise, partition the input matrices A and B and output matrix C into  $n/2 \times n/2$ submatrices, . This step takes $O(1)$ time by index calculation, just as in `MATRIX-MULTIPLY-RECURSIVE`. 
2. Create $n/2 \times n/2$ matrices $S_1,S_2, \dots, S_{10}$, each of which is the sum or difference of two submatrices from step 1. Create and zero the entries of seven  $n/2 \times n/2$ matrices $p_1, p_2, \dots, p_7$ to hold seven  $n/2 \times n/2$ matrices products. All 17 matrices can be created, and the $P_i$ initialized, in $O(n^2)$  time. 
3. Using the submatrices from step 1 and the matrices $S_1,S_2, \dots, S_{10}$ created in step 2, recursively compute each of the seven matrix products $p_1, p_2, \dots, p_7$ taking $7T (n/2)$ time. 
4. Update the four submatrices C11; C12; C21; C22 of the result matrix C by adding or subtracting various $P_i$ matrices, which takes $\Theta(n^2)$ time.
When $n>1$ step 1,2,and 4 take total of $\Theta (n^2)$ and step 3 requires seven multiplication of  $n/2 \times n/2$ matrices matrices. Hence we obtain the following recurrence for the running time of Strassen's algorithms:
$$
T(n) = 7 T(n/2) + \Theta (n^2)
$$
Compared to `MATRIX-MULTIPLY-RECURSIVE` , we have traded off one recursive submatrix multiplication for a constant number of submatrix additions.

Now let's delve into the details . step 2 creates the following 10 matrices:
$S_1 = B_{12} - B_{22}$ 
$S_2 = A_{11} + A_{12}$ 
$S_3 = A_{21 }+ A_{22}$ 
$S_4 = B_{21 }- B_{11}$ 
$S_5 = A_{11} + A_{22}$  
$S_6 = B_{11}+ B_{22}$ 
$S_7 = A_{12 }- A_{22}$ 
$S_8 = B_{21} + B_{22 }$ 
$S_9 = A_{11 }- A_{21}$  
$S_{10} = B_{11} + B_{12}$ 

This step adds or subtracts  $n/2 \times n/2$ matrices 10 times, taking $\Theta (n^2)$ time.

Step 3 recursively multiplies  $n/2 \times n/2$ matrices 7 times to  compute the follow  $n/2 \times n/2$ matrices matrices. each of which is the sum or difference of product of $A$ and $B$ submatrices:

$P_1 = A_{11} \cdot S1 (= A_{11} \cdot B_{12} - A_{11} \cdot B_{22})$ 
$P_2 = S2 \cdot B_{22} (= A_{11} \cdot B_{22} + A_{12} \cdot B_{22})$ 
$P_3 = S3 \cdot B_{11} (= A_{21} \cdot B_{11} + A_{22} \cdot B_{11})$ 
$P_4 = A22 \cdot S4 (= A_{22} \cdot B_{21} - A_{22} \cdot B_{11})$ 
$P_5 = S5 \cdot S6 (= A11 \cdot B_{11} + A_{11} \cdot B_{22} + A_{22} \cdot B_{11} + A_{22} \cdot B_{22})$ 
$P_6 = S7 \cdot S8 (= A_{12} \cdot B_{21} + A_{12} \cdot B_{22} - A_{22} \cdot B_{21} - A_{22} \cdot B_{22})$ 
$P_7 = S9 \cdot S10 (= A_{11} \cdot B_{11} + A_{11} \cdot B_{12} - A21 \cdot B_{11} - A_{21} \cdot B_{12}) :$

The only multiplication that the algorithm performs are those in the middle column of these equations. The right-hand column just shows what these products equal in terms of the original submatrices created in step 1. but the terms are never explicitly calculated by the algorithm.

We adds to and subtracts from the four $n/2 \times n/2$ submatrices of the products $C$ the various $P_i$ matrices created in step 3. 
$C_{11} = C_{11} + P_5 + P_4 - P_2 + P_6$
$C_{12} = C_{12} + P_1 + P_2$
$C_{21} = C_{21} + P_3 + P_4$
$C_{22} = C_{22} + P_5+ P_1 - P_3 + P_7$

Time complexity analysis : 
$$
T(n) = 7T\left( \frac{n}{2}  \right) + O(n^2)
$$
Solving this recurrence gives us 
$$
T(n) = O(n^{\log_{2}(7)}) \approx O(n^{2.81})
$$
This is asymptotically faster than the standard $O(n^{3})$ algorithm.
___
#### Substitution Method
Substitution method comprises two steps :
1. Guess the form of the solution symbolic constants .
2. Use mathematical induction to show that the solution works and find the constants.
To apply the inductive hypothesis, you substitute the guessed solution for the function on smaller values $-$ hence the name "substitution method".
We can use substitution method to establish either an upper bound or lower bound on a recurrence. 

Example : Determine a tight asymptotic lower bound for following recurrence :
$$
T(n) = 4T(n/2)+ n^2
$$
Solution : Let us guess that $T(n) = n^2 \text{lg }(n)$ Then our induction hypothesis is that there exists a $c$ and an $n_0$ such that 
$$
T(n) \ge cn^2 \text{ lg }(n) \space \forall n > n_0 \text{ and } c>0
$$
Now , for the inductive step, assume the hypothesis is true for $m<n$ . Then
$$
T(m) \ge cm^2 \text{ lg } (m)
$$
So, 
$$
\begin{align}
T(n) & = 4T(\frac n 2) + n^2 \\
& \ge 4c{\frac {n^2} 4} \text{ lg } \frac n 2 + n^2 \\
& = cn^2 \text{ lg }(n) -cn^2 \text{ lg }(2) + n^2 \\
& = cn^2\text{ lg }(n) + (1-c)n^2.
\end{align}
$$
If we now pick as $c<1$, then 
$$
T(n) = \Omega (cn^2\text{ lg }(n))
$$

___
#### Recursion Tree
In a recursion tree , each node represents the cost of a single subproblem somewhere in the set of recursive function invocations. we typically sum the cost within each level of tree to obtain the per-level-costs and then sum all the per-level costs to determine the total cost of all the levels of the recursion.

![[Screenshot 2024-09-09 010626.png]]
$$
\text{Figure : Recursion tree of recurrence }T(n) = 3T(n/4) + cn^2. 
$$
#### Master Method
The master method provides a "cookbook" method for solving algorithmic recurrences of the form . 
$T(n) = aT(n/b) + f(n)$
where $a>0$ and $b>1$ are constants. we call $f(n)$ a **driving function** and recurrence of this general form a **master recurrence**. 
**The master theorem** depends upon the following theorem.
Let $a>0$ and $b>1$ be constants, and let $f(n)$ be a driving function that is defined and nonnegative on all sufficiently large reals.  Define the recurrence $T(n)$ on $n\in \mathbb{N}$ by 
$T(n) = aT(n/b) + f(n)$
where $aT(n/b)$ actually means $a'T(\lfloor n/b \rfloor) + a'' T(\lceil n/b\rceil)$ for some constants $a'\ge 0$ and $a'' \ge 0$ satisfying $a= a' + a''$ . Then the asymptotic behavior of $T(n)$ cam ne characterized as follows:
1. If there exists a constant $\epsilon > 0$ such that $f(n)= O(n^{log_b a-\epsilon})$ then $T(n) = \Theta (n^{log_b a})$ .
2. If there exists a const $k\ge 0$ such that $f(n)=\Theta(n^{log_b a} lg^k n)$ , then $T(n)= \Theta(n^{log_b a} lg^{k+1} n)$
3. If there exists a constant $\epsilon > 0$ such that $f(n) = \omega (n^{log_b a + \epsilon})$, and if $f(n)$ additionally satisfies the **regularity condition** $af(n/b) \le c f(n)$ for some constant $c<1$ and all sufficiently large $n$ , then $T(n)= \Theta (f(n))$. 

The function $n^{log_b a}$ is called the watershed function.
#### Akra-bazzi method 
The Akra-Bazzi method is a powerful technique used to solve divide-and-conquer recurrences, especially those that don't fit neatly into the Master Theorem. It's particularly useful when dealing with non-homogeneous recurrences, where the recursion isn't strictly proportional at each level.
Akra-Bazzi recurrences take the form:

$$
T(n) = f(n) + \sum_{i=1}^k a_i T(b_i n + h_i(n))
$$
where \( k \) is a positive integer; all the constants $( a_1, a_2, \dots, a_k \in \mathbb{R} )$ are strictly positive; all the constants $( b_1, b_2, \dots, b_k \in \mathbb{R})$ are strictly greater than 0; and the driving function $f(n)$  is defined on sufficiently large nonnegative reals and is itself non-negative.
Next, we find \( p \) such that:
$$
\sum_{i=1}^k a_i b_i^p = 1
$$
Then,
$$
T(n) \in \Theta \left( n^p \left( 1 + \int_1^n \frac{f(u)}{u^{p+1}} du \right) \right)
$$
###### Advantages:
- Handles more complex recurrences than the Master Theorem.
- Useful for real-world problems where inputs might not split evenly.
___

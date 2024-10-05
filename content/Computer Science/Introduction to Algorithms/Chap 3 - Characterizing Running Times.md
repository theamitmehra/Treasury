The order of growth of the running time of an algorithm gives a simple way to characterize the algorithm's efficiency and also allows us to compare it with alternative algorithms. 
**Asymptotic** efficiency of an algorithm is concerned with how the running time of an algorithm increases with the size of the input in the limit, as the size of the input increases without bound.

Type of Asymptotic Efficiency :
#### $O$-notation (Worst Case)
This notation characterizes an *upper bound* on the asymptotic behavior of a function. In other words it says that a function grows no faster than a certain rate based on the highest-order term.
Consider the function $7n^3 + 100 ^n2 - 20n + 6$. Its highest-order term is $7n^3$ and so we say this function's rate of growth is $n^3$ . We can write it as $O(n^3)$ 
#### $\ohm$ - notation (Best Case)
This notation characterizes a *lower bound* one the behavior of a function. In other words it says that a function grows at least as fast as a certain rate, based $-$ as in $O$ notation $-$ on the highest-order term. 
Because the highest-order term in the function $7n^3 + 100n^2 - 20n + 6$ grows at least as fast as $n^3$, this function is $\ohm(n^3)$. This function is also $\ohm (n^2)$ and $\ohm (n)$. More generally, it is $\ohm (n^c)$ for any constant $c\le 3$ .
#### $\Theta$ - Notation (Average Case)
This notation characterizes a *tight bound* on the asymptotic behaviour of a function. It says that a function grows precisely at a certain rate, based $-$ once again $-$ on the highest-order term.
if you can show that a function is both $O(f(n))$ and $\ohm (f(n))$ for some function f(n) then you have shown that a function is $\Theta(f(n))$.
For example since the function $7n^3 + 100n^2 - 20n + 6$ is both $O(n^3)$ and $\ohm(n^3)$, It is also $\Theta (n^3)$.
___
### Asymptotic notation : formal definitions
- $O$ - notation : 
$$
	\begin{matrix}
f(n) = O(g(n)) & if\, \lim_{ n \to \infty } |\frac{f(n)}{g(n)}| < \infty
\end{matrix}
$$
- $\ohm$ - Notation :
$$
\begin{matrix}
f(n) = \Omega (g(n)) & if \space \lim_{ n \to \infty } \frac{f(n)}{g(n)} > 0
\end{matrix}
$$
- $\Theta$ Notation : 
$$
\begin{matrix}
f(b) = \Theta (g(n)) & if \space 0 < \lim_{ n \to \infty }  \frac{f(n)}{g(n)} \leq \lim_{ n \to \infty } \frac{f(n)}{g(n)} < \infty
\end{matrix}
$$

___
### Standard notations and common functions

#### Monotonicity
A function $f(n)$ is **monotonically increasing** if $m \le n$ implies $f(m) \le f(n)$. similarly, it is **monotonically decreasing** if $m \le n$ implies $f(m) \ge f(n)$. 

A function $f(n)$ is **strictly increasing** if $m < n$ implies $f(m) < f(n)$ and **strictly decreasing** if $m<n$ implies $f(m) > f(n)$.
___
#### Floor and ceilings
For any real number x, we denote the greatest integer less than or equal to x by $\lfloor{x} \rfloor$
and the least integer greater than or equal to x by $\lceil x \rceil$. The floor function is monotonically increasing , as is the ceiling function.
Floor and ceiling obey the following properties. For any integer $n$ we have $\lfloor n \rfloor = n = \lceil n \rceil$
For all real x we have
$x - 1 < \lfloor x \rfloor \le x \le \lceil x \rceil < x + 1$
We also have
$-\lfloor x \rfloor = \lceil -x \rceil$
or equivalently
$-\lceil x\rceil = \lfloor -x \rfloor$
For any integer n and real number x we have
$\lfloor n + x \rfloor = n + \lfloor x \rfloor$
$\lceil n + x \rceil= n + \lceil x \rceil$
___
#### Modular arithmetic
For any integer a and any positive integer n, the value $a\space mod \space n$ is the **remainder** (residue) of the quotient $a/n$:
$a \space mod \space n = a - n \lfloor a/n \rfloor$ 
it follows that 
$a \le a\space mod\space n < n$,
even when $a$ is negative.
___
#### Polynomials
Given a nonnegative integer $d$, a **polynomial in n of degree d** is a function $p(n)$ of the form 
$$
p(n) = sum_{i=0} ^d {a_in^i}
$$
where the constants $a_0, a_1, \dots, a_d$ are the **coefficients** of the polynomial and $a_d \ne 0$.A polynomial is asymptotically positive if and only if $a_d > 0$ .For an asymptotically positive polynomial $p(n)$  of degree $d$, we have $p(n)= \Theta (n^d)$. For any real constant $a \ge 0$, the function $n^a$ is monotonically increasing, and for any real constant $a \le 0$, the function $n^a$ is monotonically decreasing. We say that a function $f(n)$ is **polynomially bounded** if $f(n) = O(n^k)$ for some constant $k$.
___
#### Exponentials
For all real $a > 0$, $m$ and $n$ we have the following identities :
$a^0 =1$
$a^1 = a$
$a^{-1} = 1/a$
$(a^m)^n  = a^{mn}$
$(a^m)^n = (a^n)^m$
$a^m a^n = a ^{m+n}$
For all $n$ and $a\ge 1$ the function $a^n$ is monotonically increasing in $n$. 
___
#### Logarithms
$\log_{a} n = x$ is equivalent to $a^x = n$. 
We use the following notations:
$\text {lg}\space n = \text{log}_2 \space n \qquad \text{(binary logarithm)},$
$\text{ln}\space n = \text{log}_e n \qquad \text {(natural logarithm)}$
$\text{lg} ^k \space n = (\text{lg}\space n )^k \qquad \text{(exponentiation)}$
$\text{lg}\space \text{lg} \space n = \text{lg} (\text{lg} n) \qquad \text{(composition)}$
___
#### Factorials
The notation $n!$ is defined for integers $n\ge 0$ as 
$$
n! = \begin{cases}
1 & \text{if }n = 0 \\
n {\cdot} (n-1)! & \text{if }n > 0 \\
\end{cases}
$$
Thus, $n!$ = $1 \cdot 1\cdot 3 \dots n$.
A weak upper bound on the factorial function is $n! \le n^m$, since each of the n terms in the factorial product is at most $n$ .
Stirling's Approximation : 

$$
n! = \sqrt {2\pi n} \cdot (\frac n e)^n (1+ \Theta (\frac 1 n))
$$
Where $e$ is the base of the natural logarithm, gives us a tighter upper bound , and a lower bound as well. 
___
#### Function iteration
We use the notation $f^{(i)}$ to denote the function $f(n)$ iteratively applied $i$ times to an initial value of $n$. Formally, let $f(n)$ be a function over the reals. For non-negative integers i, we recursively define
$$
f^{(i)} (n) = 

\begin{cases} 
n & if \space i = 0 \\
f (f^{(i-1) (n)}) & if \space i > 0 \\
\end{cases}

$$
For example , if $f(n) = 2n$ , then $f^{(i) } = 2^i n$.
#### The iterated logarithm function
We use the notation $lg * n$ (read ''log star of n'') to denote the iterated logarithm defined as follow, let $lg^{(i)}n$ be a defined above with $f(n) = lg \space n$ . because the logarithm of a nonpositive number is undefined, $lg^ {(i)} n$ is defined only if $lg^{(i-1)} n > 0$

Be sure to distinguish $lg^{(i)} n$ (the logarithm function applied i times in succession, starting with argument n) from $lg^i n$  (the logarithm of n raised to the $ith$ power). Then we define the iterated logarithm function as 
$$
lg * n = min\{i \ge 0 : lg ^{(i)} n \le 1\}.
$$
The iterated logarithm is a very slowly growing function: 
$lg * 2 = 1$
$lg * 4 = 2$
$lg * 16 = 3$
$lg * 65536 = 4$
$lg * (2^{65536}) = 5$

Since the number of atoms in the observable universe is estimated to be about $10^{80}$ , which is much less than $2^{65536} = 10^{{65536}/lg 10} \approx 10^{19,728}$, we rarely encounter an input size n for which $lg*n > 5$.
#### Fibonacci numbers
we define the **Fibonacci numbers** $F_i$ , for $i \le 0$, as follows:
$$
F_i = \begin{cases} 0 & \text{if } i = 0, \\
1 & \text{if } i = i, \\
F_{i-1} + F_{i-2} & \text{if } i\ge 2 \\
\end{cases}
$$
Thus, after the first two, each Fibonacci number is the sum of the two previous ones, yielding the sequence
$0,1,1,2,3,5,8,13,21,34,55, \dots, \dots$
Fibonacci numbers are related to the **golden ration** $\phi$ and its conjugate $\hat{\phi}$, which are the two roots of the equation
$x^2 = x + 1$
golden ration  
$$
\phi = \frac{1 + \sqrt{5}} {2}
$$
and its conjugate, by 
$$
\hat{\phi} = \frac {1 - \sqrt {5}}{2}
$$
Specifically we have 
$$
F_i = \frac {\phi^i - \hat{\phi^i}}{\sqrt{5}}
$$
Which can be proved by induction since $|\hat{\phi}| < 1$, we have 
$$
\begin{matrix}
\frac {|\hat{\phi^i}|}{\sqrt{5}} < \frac {1} {\sqrt{5}} \\
\space \space \space < \frac {1} {2}
\end{matrix}
$$
which implies that 
$$
F_i = \lfloor{{\frac {\phi^i} {\sqrt{5}}} + {\frac 1 2}}\rfloor
$$
Which is to say that $i^{th}$  Fibonacci number is equal to $\phi ^i / \sqrt 5$ rounded to the nearest integer. Thus Fibonacci numbers grow exponentially.
___
# Number Theory and Cryptography

The part of mathematics devoted to the study of the set of integers and their properties is known as **number theory**.
## Divisibility and Modular Arithmetic
Division of an integer by a positive integer produces a quotient and a remainder.
#### Division

* **Definition** :
  If $a$ and $b$ are integers with $a \ne 0$, we say that $a$ divides $b$ if there is an integer $c$ such that $b = ac$ (or equivalently, if $b/a$ is an integer). When $a$ divides $b$ we say that $a$ is a factor or divisor of $b$, and that $b$ is a multiple of $a$. The notation $a \mid b$ denotes that $a$ divides $b$. We write $a \not\mid b$ when $a$ does not divide $b$.
* **Theorem** :
  Let $a, b,$ and $c$ be integers, where $a \ne 0$. Then
  (I) if $a \mid b$ and $a \mid c$, then $a \mid (b + c)$;
  (II) if $a \mid b$, then $a \mid bc$ for all integers $c$;
  (III) if $a \mid b$ and $b \mid c$, then $a \mid c$.
#### The Division Algorithm

* **THE DIVISION ALGORITHM** :
  Let $a$ be an integer and $d$ a positive integer. Then there are unique integers $q$ and $r$, with $0 \leq r < d,$ such that $a = dq + r$.

In the equality given in the division algorithm, $d$ is called the **divisor**, $a$ is called the **dividend**, $q$ is called the **quotient**, and $r$ is called the **remainder**. 
This notation is used to express the quotient and remainder:
* $q = a$ **div** $d, \qquad r = a$ **mod** $d$.

#### Modular Arithmetic
* **Definition** :
  If $a$ and $b$ are integers and $m$ is a positive integer, then $a$ is congruent to $b$ modulo $m$ if $m$ divides $a - b$. 
  We use the notation $a \equiv b$ (mod $m$) to indicate that $a$ is congruent to $b$ modulo m. We say that $a \equiv b$ (mod $m$) is a **congruence** and that $m$ is its **modulus** (plural **moduli**). If $a$ and $b$ are not congruent modulo $m$, we write $a \not\equiv b$ (mod $m$).
* **Theorem** :
  Let $a$ and $b$ be integers, and let $m$ be a positive integer. Then $a \equiv b$ (mod $m$) if and only if
  $a$ **mod** $m = b$ **mod** $m$.

The great German mathematician **Karl F. Gauss** developed the concept of congruences at the end of the eighteenth century. The notion of congruences has played an important role in the development of number theory.
* **Theorem** :
  Let $m$ be a positive integer. The integers $a$ and $b$ are congruent modulo $m$ if and only if there is an integer $k$ such that $a = b + k m$.

The set of all integers congruent to an integer $a$ modulo $m$ is called the **congruence class** of $a$ modulo $m$. Furthermore, we will show that there are $m$ pairwise disjoint equivalence classes modulo $m$ and that the union of these equivalence classes is the set of integers.
* **Theorem** :
  Let $m$ be a positive integer. If $a \equiv b$ (mod $m$) and $c \equiv d$ (mod $m$), 
  then $a + c \equiv b + d$ (mod $m$) and  $ac \equiv bd$ (mod $m$).
* **Corollary** :
  Let $m$ be a positive integer and let $a$ and $b$ be integers. Then $$\begin{align*}
  & (a + b) \space \text{mod} \space m = ((a \space \text{mod} \space m) + (b \space \text{mod} \space m)) \space \text{mod} \space m & and \\ 
  & ab \space \text{mod} \space m = ((a \space \text{mod} \space m)(b \space \text{mod} \space m)) \space \text{mod} \space m. &
  \end{align*}$$
#### Arithmetic Modulo $m$
We can define arithmetic operations on $Z_m$, the set of non-negative integers less than $m$, that is, the set $\{0, 1, \ldots, m - 1\}$. In particular, we define addition of these integers, denoted by $+_m$ by $$\begin{align*}
& a +_m b = (a + b) \space \text{mod} \space m, &
\end{align*}$$where the addition on the right-hand side of this equation is the ordinary addition of integers, and we define multiplication of these integers, denoted by ${\cdot}_m$ by$$\begin{align*}
& a \space {\cdot}_m \space b = (a \cdot b) \space \text{mod} \space m, &
\end{align*}$$where the multiplication on the right-hand side of this equation is the ordinary multiplication of integers. The operations $+_m$ and $\cdot_m$ are called **addition and multiplication modulo m** and when we use these operations, we are said to be doing **arithmetic modulo m**.

## Integer Representations and Algorithms
#### Representations of Integers
In everyday life we use decimal notation to express integers. In decimal notation, an integer $n$ is written as a sum of the form $a_k 10^k + a_{k-1} 10^{k-1} + \ldots + a_1 10 + a_0,$ where $a_j$ is an integer with $0 \leq a_j \leq 9$ for $j = 0, 1, \ldots, k$.
* **Theorem (Base $b$ expansion of $n$)** :
  Let $b$ be an integer greater than 1. Then if $n$ is a positive integer, it can be expressed uniquely in the form $$\begin{align*}
   & n = a_k b^k + a_{k-1} b^{k-1} + \ldots + a_1 b + a0, &
   \end{align*}$$where $k$ is a non-negative integer, $a_0 , a_1 , \ldots, a_k$ are non-negative integers less than $b$, and $a_k \ne 0$.

###### Base Conversion
First, divide $n$ by $b$ to obtain a quotient and remainder, that is, 
$n = bq_0 + a_0, \qquad 0 \leq a_0 < b$.
The remainder, $a_0$, is the rightmost digit in the base $b$ expansion of $n$. Next, divide $q_0$ by $b$ to obtain $q_0 = bq_1 + a_1, \qquad 0 \leq a_1 < b$.
We see that $a_1$ is the second digit from the right in the base $b$ expansion of $n$.
Continue this process, successively dividing the quotients by $b$, obtaining additional base $b$ digits as the remainders. This process terminates when we obtain a quotient equal to zero. It produces the base $b$ digits of $n$ from the right to the left.
* **Algorithm** : Constructing Base $b$ Expansions
  **procedure** base $b$ expansion($n,b$: positive integers with $b > 1$)
  $q := n$
  $k := 0$
  while $q \ne 0$
  $\qquad a_k := q$ mod $b$
  $\qquad q := q$ div $b$
  $\qquad k := k + 1$
  return ($a_{k - 1}, \ldots, a_1, a_0$) {${(a_{k - 1} \ldots a_1 a_0)}_b$ is the expansion of $n$}

#### Algorithms for Integer Operations
The algorithms for performing operations with integers using their binary expansions are extremely important in computer arithmetic.
###### Addition Algorithm
* **Algorithm** : Addition of Integers.
  **procedure** add($a, b$ : positive integers)
  {$a$ and $b$ are ${(a_{n-1}a_{n-2} \ldots a_1 a_0)}_2$ and ${(b_{n-1}b_{n-2} \ldots b_1 b_0)}_2,$ respectively}
  $c := 0$
  for $j := 0$ to $n - 1$
  $\qquad d := \lfloor(a_j + b_j + c)∕2 \rfloor$
  $\qquad s_j := a_j + b_j + c - 2d$
  $\qquad c := d$
  $s_n := c$
  return $(s_0, s_1, \ldots, s_n)$ {the binary expansion of the sum is $(s_n s_{n-1} \ldots s_0)_2$}

###### Multiplication Algorithm
* **Algorithm** : Multiplication of Integers.
  **procedure** multiply($a, b$ : positive integers)
  {$a$ and $b$ are ${(a_{n-1}a_{n-2} \ldots a_1 a_0)}_2$ and ${(b_{n-1}b_{n-2} \ldots b_1 b_0)}_2,$ respectively}
  for $j := 0$ to $n - 1$
  $\qquad$if $b_j = 1$ then $c_j := a$ shifted $j$ places
  $\qquad$else $c_j := 0$
  $\{c_0, c_1, \ldots, c_{n - 1}$ are partial products$\}$
  $p := 0$
  for $j := 0$ to $n - 1$
  $\qquad p := add(p, c_j)$
  return $p$ {$p$ is the value of $ab$}

##### Algorithm for $div$ and $mod$
* **Algorithm** : Computing div and mod.
  **procedure** division algorithm($a$ : integer, $d$ : positive integer)
  $q := 0$
  $r := |a|$
  while $r \geq d$
  $\qquad r := r - d$
  $\qquad q := q + 1$
  if $a < 0$ and $r > 0$ then
  $\qquad r := d - r$
  $\qquad q := -(q + 1)$
  return $(q, r)$ {$q = a \space div \space d$ is the quotient, $r = a \space mod \space d$ is the remainder}

#### Modular Exponentiation
In cryptography it is important to be able to find $b^n$ mod $m$ efficiently without using an excessive amount of memory, where $b, n,$ and $m$ are large integers. 
It is impractical to first compute $b^n$ and then find its remainder when divided by $m$, because $b^n$ can be a huge number and we will need a huge amount of computer memory to store such numbers.
To motivate the fast modular exponentiation algorithm, we illustrate its basic idea. We will explain how to use the binary expansion of $n$, say $n = {(a_{k-1} \ldots a_1 a_0)}_2,$ to compute $b^n$.
First, note that $$\begin{align*}
& b^n = b^{a_{k-1} \cdot 2^{k-1}+ \ldots + a_1 \cdot 2 + a_0} = b^{a_{k-1} \cdot 2^{k-1}} \ldots b^{a_1 \cdot 2} \cdot b^{a_0}. &
\end{align*}$$This shows that to compute $b^n$, 
we need only compute the values of $b, b^2, (b^2)^2 = b^4, (b^4)^2 = b^8, \ldots, b^{2^k}$. Once we have these values, we multiply the terms $b^{2^j}$ in this list, where $a_j = 1$. This gives us $b^n$.

* **Algorithm** : Fast Modular Exponentiation.
  **procedure** modular exponentiation($b$: integer, $n = {(a_{k−1} a_{k−2} \ldots a_1a_0)}_2,$ $m$: positive integers)
  $x := 1$
  $power := b$ mod $m$
  for $i := 0$ to $k - 1$
  $\qquad$if $a_i = 1$ then $x := (x \cdot power)$ mod $m$
  $\qquad power := (power ⋅ power)$ mod $m$
  return $x$ {$x$ equals $b^n$ mod $m$}

## Primes and Greatest Common Divisors
Primes have become essential in modern cryptographic systems, and we will develop some of their properties important in cryptography. For example, finding large primes is essential in modern cryptography.
The length of time required to factor large integers into their prime factors is the basis for the strength of some important modern cryptographic systems.
#### Primes
* **Definition** :
  An integer $p$ greater than $1$ is called **prime** if the only positive factors of $p$ are $1$ and $p$.
  A positive integer that is greater than 1 and is not prime is called **composite**.

An integer $n$ is composite if and only if there exists an integer $a$ such that $a \mid n$ and $1 < a < n$.

* **Theorem** : *The Fundamental Theorem Of Arithmetic*
  Every integer greater than 1 can be written uniquely as a prime or as the product of two or more primes, where the prime factors are written in order of non-decreasing size.
* **Theorem** :
  If $n$ is a composite integer, then $n$ has a prime divisor less than or equal to $\sqrt{n}$.

Because there are infinitely many primes, given any positive integer there are primes greater
than this integer. For almost all the last 300 years, the largest prime known has been an integer of the special form $2^p - 1,$ where $p$ is also prime.
Such primes are called **Mersenne primes**. The reason that the largest known prime has usually been a Mersenne prime is that there is an extremely efficient test, known as the Lucas-Lehmer test, for determining whether $2^p - 1$ is prime.

* **Theorem** : *The Prime Number Theorem*
  The ratio of $\pi(x),$ the number of primes not exceeding $x$, and $x / \ln x$ approaches $1$ as $x$ grows without bound. (Here $\ln x$ is the natural logarithm of $x$.)
#### Greatest Common Divisors and Least Common Multiples
* **Definition** :
  Let $a$ and $b$ be integers, not both zero. The largest integer $d$ such that $d \mid a$ and $d \mid b$ is called the **greatest common divisor** of $a$ and $b$. The greatest common divisor of $a$ and $b$ is denoted by gcd$(a, b)$.
* **Definition** :
  The integers $a$ and $b$ are **relatively prime** if their greatest common divisor is $1$.
* **Definition** :
  The integers $a_1, a_2, \ldots, a_n$ are **pairwise relatively prime** if gcd$(a_i, a_j) = 1$ whenever
  $1 \leq i < j \leq n$.

Another way to find the greatest common divisor of two positive integers is to use the prime factorizations of these integers. Suppose that the prime factorizations of the positive integers $a$ and $b$ are $$\begin{align*}
& a = p_1^{a_1}p_2^{a_2} \ldots p_n^{a_n}, \qquad b = p_1^{b_1}p_2^{b_2} \ldots p_n^{b_n}, &
\end{align*}$$where each exponent is a non-negative integer, and where all primes occurring in the prime factorization of either $a$ or $b$ are included in both factorizations, with zero exponents if necessary. Then gcd$(a, b)$ is given by $$\begin{align*}
& \text{gcd} (a, b) = p_1^{min(a_1, b_1)}p_2^{min(a_2, b_2)} \ldots p_n^{min(a_n, b_n)}, &
\end{align*}$$where $min(x, y)$ represents the minimum of the two numbers $x$ and $y$.

* **Definition** :
  The **least common multiple** of the positive integers $a$ and $b$ is the smallest positive integer that is divisible by both $a$ and $b$. The least common multiple of $a$ and $b$ is denoted by lcm$(a, b)$.
* **Theorem** :
  Let $a$ and $b$ be positive integers. Then $ab = \text{gcd}(a, b) \cdot \text{lcm}(a, b)$.

The greatest common divisor of two integers $a$ and $b$ can be expressed in the form $sa + tb,$
where $s$ and $t$ are integers.
In other words, gcd$(a, b)$ can be expressed as a **linear combination** with integer coefficients of $a$ and $b$.

* **Bézout's Theorem :
  If $a$ and $b$ are positive integers, then there exist integers $s$ and $t$ such that
  gcd$(a, b) = sa + tb$.
* **Definition** :
  If $a$ and $b$ are positive integers, then integers $s$ and $t$ such that gcd$(a, b) = sa + tb$ are called **Bézout Coefficients** of $a$ and $b$. Also, the equation gcd$(a, b) = sa + tb$ is called **Bézout's Identity**.
* **Theorem** :
  Let $m$ be a positive integer and let $a, b,$ and $c$ be integers. If $ac \equiv bc$ (mod $m$) and
  gcd$(c, m) = 1,$ then $a \equiv b$ (mod $m$).

## Solving Congruences
#### Linear Congruences
A congruence of the form $ax \equiv b$ (mod $m$), where $m$ is a positive integer, $a$ and $b$ are integers, and $x$ is a variable, is called a **linear congruence**.

* **Theorem** :
  If $a$ and $m$ are relatively prime integers and $m > 1,$ then an inverse of $a$ modulo $m$ exists. Furthermore, this inverse is unique modulo $m$.
  (That is, there is a unique positive integer $\bar{a}$ less than $m$ that is an inverse of $a$ modulo $m$ and every other inverse of $a$ modulo m is congruent to $\bar{a}$ modulo $m$.)

* **Theorem** : *The Chinese Remainder Theorem*
  Let $m_1, m_2, \ldots, m_n$ be pairwise relatively prime positive integers greater than one and
  $a_1, a_2, \ldots, a_n$ arbitrary integers. Then the system $$\begin{align*}
  & x \equiv a_1 (\text{mod} \space m_1), & \\
  & x \equiv a_2 (\text{mod} \space m_2), & \\
  & \quad . & \\
  & \quad . & \\
  & \quad . & \\
  & x \equiv a_n (\text{mod} \space m_n) & \\
\end{align*}$$has a unique solution modulo $m = m_1 m_2 \ldots m_n$. (There is a solution $x$ with $0 \leq x < m,$ and all other solutions are congruent modulo $m$ to this solution.)
#### Fermat's Little Theorem
* **Theorem** : Fermat's Little Theorem
  If $p$ is prime and $a$ is an integer not divisible by $p$, then $a^{p-1} \equiv 1$ (mod $p$).
  Furthermore, for every integer $a$ we have $a^p \equiv a$ (mod $p$).
* **Definition** : 
  Let $b$ be a positive integer. If $n$ is a composite positive integer, and $b^{n−1} \equiv 1$ (mod $n$), then $n$ is called a **pseudo-prime** to the base $b$.
* **Definition** :
  A composite integer $n$ that satisfies the congruence $b^{n−1} \equiv 1$ (mod $n$) for all positive integers $b$ with gcd$(b, n) = 1$ is called a **Carmichael number**.
#### Primitive Roots and Discrete Logarithms
In the set of positive real numbers, if $b > 1,$ and $x = by,$ we say that $y$ is the logarithm of $x$ to
the base $b$.
* **Definition** :
  A **primitive root** modulo a prime $p$ is an integer $r$ in $\mathbb{Z}_p$ such that every nonzero element of $\mathbb{Z}_p$ is a power of $r$.
* **Definition** :
  Suppose that $p$ is a prime, $r$ is a primitive root modulo $p$, and $a$ is an integer between $1$ and $p - 1$ inclusive.
  If $r^e$ mod $p = a$ and $0 \leq e \leq p - 1,$ we say that $e$ is the **discrete logarithm** of $a$ modulo $p$ to the base $r$ and we write $\log_{r} a = e$ (where the prime $p$ is understood).

## Applications Of Congruences
#### Hashing Functions
A **hashing function** $h$ assigns memory location $h(k)$ to the record that has $k$ as its **key**.
One of the most common is the function $h(k) = k$ mod $m$ where $m$ is the number of available memory locations. Hashing functions should be easily evaluated so that files can be quickly located. The hashing function $h(k) = k$ mod $m$ meets this requirement; to find $h(k)$, we need only compute the remainder when $k$ is divided by $m$.
Furthermore, the hashing function should be onto, so that all memory locations are possible. The function $h(k) = k$ mod $m$ also satisfies this property.
#### Pseudo-random Numbers
The numbers generated by systematic methods are not truly random, they are called **pseudorandom numbers**. 
The most commonly used procedure for generating pseudorandom numbers is the **linear congruential method**. We choose four integers: the **modulus** $m$, **multiplier** $a$, **increment** $c$, and **seed** $x_0$, with $2 \leq a < m, 0 \leq c < m,$ and $0 \leq x_0 < m.$ We generate a sequence of pseudorandom numbers {$x_n$}, with $0 \leq x_n < m$ for all $n$, by successively using the recursively defined function **$x_{n + 1} = (ax_n + c)$ mod $m$**.
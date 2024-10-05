### The hiring problem
Suppose that you need to hire a new office assistant. Your previous attempts at hiring have been unsuccessful, and you decide to use an employment agency. The employment agency sends you one candidate each day. You interview that person and then decide either to hire that person or not. You must pay the employment agency a small fee to interview an applicant. To actually hire an applicant is more costly, however, since you must hire your current office assistant and also pay a substantial hiring fee to the employment agency. You are committed to having, at all times, the best possible person for the job. Therefore, you decide that, after interviewing each applicant, if that applicant is better qualified than the current office assistant, you will hire the current office assistant and hire the new applicant. You are willing to pay the resulting price of this strategy, but you wish to estimate what that price will be.

>[!tldr] $\text{HIRE-ASSISTANT}(n)$
>$best = 0$ $\qquad\qquad$ // candidate $0$ is a least-qualified dummy candidate  
>for $i= 1$ to $n$  
>$\qquad$ interview candidate $i$  
>if candidate $i$ is better than candidate $best$  
>$\qquad\qquad$ $best = i$  
>$\qquad\qquad$ hire candidate $i$  

the total cost of this algorithm is $O(c_i n + c_h m)$ where $c_i$ is cost of interviewing and $c_h$ is cost of hiring a candidate, n is number of total candidate and m is the no of total hired candidate.
#### Worst-case analysis
In the worst case, you actually hire every candidate that you interview. This situation occurs if the candidates come in strictly increasing order of quality. in which case you hire n times , for a total hiring cost of $O(c_hn)$ 
#### Probabilistic analysis
**probabilistic analysis** is the use of probability in the analysis of problems. it is mostly used to analyze the running time of an algorithm. In order to perform probabilistic analysis we must use or make an assumption about the distribution of inputs. Then we take the average over the distribution of the possible inputs. this kind of running time is also called the **average-case running time**.
We assume the the order of quality of candidates is random. in other words the order list $(rank(1), rank(2), \dots , rank(n))$ is a permutation of the list $(1,2,3, \dots , n)$ .
alternatively we say that the ranks form a **uniform random permutation** (each $n!$ permutation appears with equal probability).
#### Randomized algorithms
An algorithm is called **randomized** if its behaviour is determined not only by its input but also by values produced by a **random-number generator**.
When analyzing the running time of a randomized algorithm we take the expectation of the running time over the distribution of values returned by the random number generator.
### Indicator random variables
In order to analyze many algorithms, including the hiring problem, we use indicator random variables. it provides a convenient method for converting between probabilities and expectation.
Given a sample space $S$ and an event $A$, the indicator random variable $I\{A\}$ with even $A$ is defined as 
$$
I\{A\} = \begin{cases} 1 & \text{if }A\text{ occurs} \\
0 & \text{if }A\text{ does not occurs}\end{cases}
$$
### Randomized algorithms types
Randomized algorithms make random choices during execution. They can often provide good average-case performance for all inputs, not just for assumed input distribution.
- Las Vegas algorithms : These randomized algorithms guarantee correctness, and are usually efficient.  Example - Quicksort
- Monte Carlo algorithms : These randomized algorithms are provably efficient and usually produce the correct answer or something close to it. Example - Random sampling.

##### Randomized Hiring algorithm
Instead of interviewing candidates in order, we can randomly permute the order of candidates.
>[!tldr] $\text{RANDOMIZED-HIRE-ASSISTANT}(n)$
>// randomly permute the list of candidates 
>$best = 0$ // dummy variable
>for $i=1$ to $n$
>$\qquad$ interview candidate $i$
>$\qquad$if candidate $i$ is better than the $best$
>$\qquad\qquad$ $best =i$
>$\qquad\qquad$ hire candidate $i$

### Probabilistic analysis and further uses of indicator random variable
#### birthday paradox
How many people must there be in a room before there is 50% chance that two of them were born on the same day of the year?
To answer this question, we index the people in the room with the integers $1,2,3, \dots, k$ where k is the no of people in the room. We assume n = 365 (no leap year) . For $i = 1,2, \dots, k$ , let $b_i$ be the day of the year on which person i's birthday falls, where $i\le b_i \le n$. We also assume that birthdays are uniformly distributed across the n days of the year, so that $Pr{b_i=r}=1/n$ for $i=1,2,\dots, n$.
Probability that $i$'s birthday and $j$'s birthday both fall on day $r$ is 
$$
\begin{align}
Pr\{b_i = r \text{ and } b_j = r\}  & = Pr\{b_i = r\} \space Pr\{b_j = r\} \\ 
& = \frac 1 n^2\qquad \qquad \qquad\qquad \qquad
\end{align}
$$
Thus, the probability that they both fall on the same day is 
$$
\begin{align}
Pr\{b_i = b_j\} & = \sum_{r=1}^n {Pr\{b_i=r \text { and } b_j=r\}} \\
& = \sum_{r=1} ^n {\frac 1 {n^2}} \\
& = \frac 1 n
\end{align}
$$

one $b_i$ is chosen, the probability that $b_j$ is chosen to be the same day is 1/n. 
We can analyze the probability of at least 2 out of k people having matching birthday by looking at the complementary event.
The probability that at least two of the birthdays match is 1 minus probability that all the birthdays are different.
The event $B_k$ that $k$ people have distinct birthdays is
$$
B_k = \bigcap_{i=1}^k A_i.
$$
where $A_i$ is the event that person $i$'s birthday is different from person $j$'s for all $j<i$. Since we can write $B_k = A_k \cap B_{k-1}$, we obtain from equation .

$$Pr\{B_k\} = Pr\{B_{k-1}\} \space Pr \{A_k | B_{k-1}\}, \qquad \qquad (5.8)$$
Where we take $Pr\{B_{k-1}\} \space Pr\{A_k | B_{k-1} \} = 1$ as an initial condition. In other words, the probability that $b_1, b_2, \dots, b_k$ are distinct birthdays equals the probability that $b_1, b_2, \dots , b_k$ are distinct birthdays multiplied by the probability that $b_k \ne b_i$  for $b_1, b_2, \dots, k-1$ , given that $b_1, b_2, \dots, b_{k-1}$ are distinct.
If $b_1, b_2, \dots, b_{k-1}$ are distinct , the conditional probability that $b_k \ne b_i$ for $i=1,2,\dots , k-1$ is $Pr\{A_k | B_{k-1}\} = (n-k+1)/n$, since out of the n days , $n-(k-1)$ days are not taken.  

We iteratively apply the recurrence (5.8) to obtain 
$$
\begin{align}
Pr\{B_k\} & = Pr\{B_{k-1}\} \space Pr\{A_k | B_{k-1}\} \\
& = Pr\{B_{k-2}\} \space Pr\{A_{k-1} | B_{k-2}\}\space Pr\{A_k | B_{k-1}\} \\
& \qquad \vdots \\
&= Pr\{B_1\} Pr\{A_2 | B_1\} Pr\{A_3 | B_2\} \dots Pr\{A_k | B_{k-1}\} \\
& = 1 \cdot (\frac {n-1} n) \cdot (\frac {n-2} n) \dots (\frac {n-k+1} n) \\
& 1 \cdot (1 - \frac 1 n) (1 - \frac 2 n) \dots (1 - \frac {k-1} n) \\
\end{align}
$$

Inequality $1 + x \le e^x$ gives us
$$
\begin{align}
Pr{B_k} & \le e^{-1/n} \space e^{-2/n} \space\dots \space e^{-(k-1)/n} \\
& = e^{-\sum_{i=1}^{k-1} {i/n}} \\
& = e^{-k(k-1)/2n} \\
& \le \frac 1 2
\end{align}
$$

When $-k(k-1)/2n \le ln(1/2)$  The probability that all $k$ birthdays are distinct is at most 1/2 when $k(k-1) \ge 2n \text{ ln } 2$ or, solving the quadratic equation, when $k \ge (1+ \sqrt{1+ (x \text{ ln }2)n}) /2$ For $n = 365$, we must have $k \ge 23$. Thus, if at least 23 people are in a room, the probability is at least $1/2$ that at least two people have the same birthday.
#### Balls and bins
#### Streaks
___
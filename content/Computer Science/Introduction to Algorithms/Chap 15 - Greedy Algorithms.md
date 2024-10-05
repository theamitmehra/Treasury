# Greedy Algorithms

A *greedy algorithm* always makes the choice that looks best at the moment. That is, it make a locally optimal choice in the hope that this choice leads to a globally optimal solution.
Greedy algos do not always yield optimal solutions, but for many problems they do.

### An Activity-selection problem
Imagine that you are in charge of scheduling a conference room. You are presented with a set $S =\{ a_{1},a_{2}, \dots a_{n} \}$ of n proposed *activities* that wish to reserve the conference room, and the room can serve only one activity at a time.
Each activity $a_{i}$ has a *start time* $s_{i}$ and a *finish time* $f_{i}$ where $0\leq s_{i} < f_{i}< \infty$. If selected, activity $a_{i}$ takes place during the half open time interval $[s_{i}, f_{i}]$. Activities $a_{i}$ and $a_{j}$ are compatible if the intervals $[s_{i}, f_{i}]$ and $[s_{j}, f_{j})$ do not overlap. That is, $a_{i}$ and $a_{j}$ are compatible if $s_{i}\geq f_{j}$ or $s_{j}\geq f_{i}$ . 
Your goal is to select a maximum-size subset of mutually compatible activities. Assume that the activities are sorted in monotonically increasing order of finish time:
$$
f_{1} < f_{2} \leq f_{3} \leq \dots \leq f_{n-1} \leq f_{n}
$$

##### Optimal substructure of the activity-selection problem

$$
c[i,j] = \begin{cases}
0 & \text{if } S_{ij} = \emptyset, \\
\max\{ c[i,k]+c[k,j]+1 : a_{k} \in S_{ij}\} & \text{if }S_{ij} \neq \emptyset 
\end{cases}
$$

##### making a greedy choice
##### A recursive greedy algorithm
The procedure `RECURSIVE-ACTIVITY-SELECTOR` takes the start and finish time of activities, represented as arrays $s$ and $f$, the index$k$ that defines the subproblem $S_{k}$ it is to solve and the size n of the original problem. 
It returns a maximum size set of mutually compatible activities in $S_{k}$. 

>[!tldr] $\text{RECURSIVE-ACTIVITY-SELECTOR}(s, f, k, n)$
>$m = k+1$  
>while $\space m\leq n$ and $\space[m] < f[k] \qquad\qquad$ // find the first activity in $S_{k}$ to finish  
>$\qquad$ $m= m+1$  
>if $m \leq n$  
>$\qquad$return $\{ a_{m} \} \space \cup\text{RECURSIVE-ACTIVITY-SELECTOR}(s, f, m, n)$   
>else return $\emptyset$   

##### An iterative greedy algorithm
The procedure `GREEDY-ACTIVITY-SELECTOR` is an iterative version of above procedure. It, too, assumes that input activities are ordered by monotonically increasing finish time. 
It collects selected activities into a set $A$ and return this set when it is done.

>[!tldr] $\text{GREEDY-ACTIVITY-SELECTOR}(s, f, n)$
> $A = \{ a_{1} \}$  
> $k = 1$   
> for $\space m=2$ to $n$  
> $\qquad$ if $s[m]\geq f[k]$  
> $\qquad\qquad A = A \cup \{ a_{m} \}$  
> $\qquad\qquad k = m$  
> return $A$

The procedure works as follows. The variable $k$ indexes the most recent addition to $A$, corresponding to the activity $a_{k}$ in the recursive version. Since the procedure considers the activities in order of monotonically increasing finish time, $f_{k}$ is always the maximum finish time of any activity in $A$. That is
$f_{k}= \max\{ f_{i}:a_{i} \in A\}$ 

We first select activity $a_{1}$, initialize $A$ to contain just this activity, and initialize $k$ to index this activity. The for loop finds the earliest activity in $S_k$ to finish. The loop considers each activity $a_m$ in turn and adds $a_m$ to A if it is compatible with all previously selected activities. Such an activity is the earliest in $S_k$ to finish. To see whether activity am is compatible with every activity currently in $A$, it suffices by equation $f_{k} = \max\{ f_{i}:a_{i}\in A \}$ to check that its start time $s_m$ is not earlier than the finish time $f_k$ of the activity most recently added to A. If activity $a_m$ is compatible, then  add activity $a_m$ to $A$ and set $k$ to $m$. The set $A$ returned by the call $\text{GREEDY-ACTIVITY-SELECTOR}(s, f)$  is precisely the set returned by the initial call $\text{RECURSIVE-ACTIVITY-SELECTOR}(s,f,0,n)$. Like the recursive version, $\text{GREEDY-ACTIVITY-SELECTOR}$ schedules a set of n activities in $\Theta(n)$ time, assuming that the activities were already sorted initially by their finish times.
### Elements of greedy strategy
##### Greedy-choice property
The first key ingredient is the *greedy-choice property* : you can assemble a globally optimal solution by making locally optimal (greedy) choices.
In DP you make a choice at each step, but the choice usually depends on the solution to subproblem. Consequently, we typically solve dynamic programming problems in a bottom up manner, progressing from smaller subproblems to larger subproblems. In Greedy algorithm, we make whatever choice seems best at the moment and then solve the subproblem that remains.
The choice made by a greedy algorithm may depend on choices so far, but it does not depend on any future choices or on the solution to subproblems.
##### Optimal substructure
A problem exhibits *optimal substructure* if an optimal solution to the problem contains within it optimal solution to subproblems.  This property is a key ingredient of assessing whether dp applies, and it's also essential for greedy algorithms. we know that If an optimal solution to subproblem $S_{ij}$ includes an activity $a_{k}$ then it must also contain optimal solution to sub problems $S_{ik}$ and $S_{kj}$ . 
Given this optimal substructure we can construct an optimal solution to $S_{ij}$ by selecting $a_{k}$ along with all activities in optimal solutions to the subproblem $S_{ik}$ and $S_{kj}$.
### Huffman codes
Huffman codes are used to compress data. It uses a table giving how often each character occurs (frequency) to build a optimal way of representing each character as a binary string. 
We consider the problem of designing a  binary character code in which each character is represented by a unique binary string, which we is called *codeword*. 
If we use a *fixed-length code*, we need $\lceil \lg n \rceil$ bits to represent $n\geq_{2}$ character. Whereas a *variable-length code* can do better than a fixed-length code. The idea is simple we give frequent characters short codewords and infrequent characters long codewords. 

##### Constructing a Huffman code
Huffman invented a greedy algorithm that constructs an optimal prefix-free code, 
called a *Huffman code* in his honor. 
The procedure `HUFFMAN` assumes that $C$ is a set of $n$ characters and that each character $c \in C$ is an object with an attribute $c.freq$ giving its frequency. The algorithm builds the tree $T$ corresponding to an optimal code in a bottom-up manner. It begins with a set of $|C|$ leaves and performs  a sequence $|C|-1$ "merging" operation to create the final tree. 
The algorithm uses a min-priority queue $Q$ on the $freq$ attribute, to identify the two least frequent objects to merge together. The result of merging two least-frequent objects is a new objects whose frequency is the sum of the frequencies of the two objects that were merged.

 >[!tldr] $\text{HUFFMAN}(C)$
>$n = |C|$  
>$Q = C$  
>for $i=1$ to $n-1$  
>$\qquad$allocate a new node $z$   
>$\qquad$$x =\text{EXTRACT-MIN}(Q)$  
>$\qquad y =\text{EXTRACT-MIN}(Q)$  
>$\qquad z.left = x$  
>$\qquad z.right = y$  
>$\qquad z.freq = x.freq + y.freq$  
>$\qquad\text{INSERT}(Q, z)$  
>return $\text{EXTRACT-MIN}(Q)$  

### Offline Caching
A *cache* organized data into *cache blocks* typically comprising 32, 64, 128 bytes. We can think of main memory as a cache for disk-resident data in a virtual-memory system. Blocks are called *pages* and 4096 is the typical size.
As a computer program execute it makes a sequence of memory requests, to data in blocks $b_{1},b_{2},\dots,b_{n}$ in that order. The blocks in the access usually not distinct. Each request causes at most one block to enter the cache and at most one block to be evicted from the cache. 
Upon a request for block $b_{i}$ any one of three scenarios may occur:
1. Block $b_{i}$ is already in the cache, due to a previous request for the same block. The cache remains unchanged. This situation is known as *cache hit*.
2. Block $b_{i}$ is not in the cache at that time but that cache contains fewer than $k$ blocks. In this case block $b_{i}$ is placed into the cache. so that cache contains one more block than it did before the reques.t
3. Block $b_{i}$ is not in the cache at that time and cache is full: it contains $k$ block. Block $b_{i}$ is placed into the cache, but before that happens, some other block must be evicted from the cache in order to make room.
The latter two situation are called *cache misses*. The goal is to minimize the number of cache misses. A cache miss that occurs while that cache holds fewer than $k$ blocks - that is, as the cache is first being filled up - is known as *compulsory miss*.
Caching is an online problem. here however let's consider the offline version of this problem in which computer knows in advance the entire sequence of n requests and the cache size $k$ with a goal of minimizing the total number of cache misses.
To solve this problem, we use a  greedy strategy called *furthest-in future* which chooses to evicts the block in the cache whose next access in the request sequence comes furthest in the future

##### Offline substructure of offline caching
To show that the offline problem exhibits optimal substructure, let's define the subproblem $(C,i)$ as processing requests for blocks  $b_{i}, b_{i+1}, \dots, b_{n}$ with cache configuration $C$ at the time that 

$$
\text{miss}(C, i) = \begin{cases}
0 & \text{if } i = m \text{ and } b_{n} \in C, \\
1 & \text{if } i = n \text{ and } b_{n} \not \in C, \\
miss(C, i+1) & \text{if } i <n \text{ and } b_{i} \in C, \\
1 + min\{ miss(C', i+1): C' \in R_{c,i} \} & \text{if } i<n  \text{ and } b_{i} \not\in C
 \end{cases}
$$

##### Greedy-choice property


___
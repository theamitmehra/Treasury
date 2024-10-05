A **hash table** is an effective data structure for implementing dictionaries.  The Major advantages of using hash table is that searching an element in hash table takes $O(1)$ time in average case which is fruitful in programming. 
In practice hashing works extremely well.
A hash table generalizes the simpler notion of an ordinary array. Directly addressing into an ordinary array takes advantages of the $O(1)$ access time for any array element. To use direct addressing you must be able to allocate an array that contains a position for every possible key.
#### Direct-address tables 
Direct addressing is a simple technique that works well when the universe $U$ of keys is reasonably small. Suppose that an application needs a dynamic set in which each element has a distinct key drawn from the universe $U = \{0,1, \dots, m-1\}$ where $m$ is not too large.
**Direct-address table** denoted by  $T[0:m-1]$ are used to represent the dynamic set. Each position or slot corresponds to a key in key in the universe $U$.
Dictionary operations are `DIRECT-ADDRESS-SEARCH`, `DIRECT-INSERT`, `DIRECT-ADDRESS-DELETE` each of these takes only $O(1)$ time.

```psuedocode
DIRECT-ADDRESS-SEARCH(T,k)
__________________________
return T[k]

DIRECT-ADDRESS-INSERT(T,k)
__________________________
T[x.key] = x

DIRECT-ADDRESS-DELETE(T,x)
__________________________
T[x.key] = NIL
```
___
### Hash tables
The downside of direct addressing is that if universe $U$ is large and infinite storing a table $T$ of size $|U|$ becomes impractical or even impossible.

With direct addressing, an element with key $k$ is stored in slot k, but with hashing, we use a **hash function** $h$ to compute the slot number from the key $k$ , so that the element goes into slot $h(k)$. The hash function $h$ maps the universe $U$ of keys into the slots of a hash table $T[0:m-1]$.
$h:U \rightarrow \{0,1, \dots, m-1\}$
where the size $m$ of the hash table is typically much less than $|U|$.  We say the an element with key $k$ hashes to slot $h(k)$, and also that $h(k)$ is the hash value of key $k$.
An example of a simple but not particularly good, hash function is $h(k) = k \text{ mod } m$.

When two keys map to the same slot we refer to this situation as **collision**.

#### Independent uniform hashing
An ideal hashing function $h$ would have, for each possible input $k$ in the domain $U$ , an output $h(k)$ that is an element randomly and independently chosen uniformly from the range $\{0,1, \dots, m-1\}$. Once a value $h(k)$ is randomly chosen, each subsequent call to $h$ with the same input $k$ yields the same output $h(k)$.
This type of ideal hash function is called **independently uniform hash function** or **random oracle**. 
Independently uniform hashing is an ideal theoretical abstraction, but it is not something that can reasonably be implemented  in practice.
#### Collision resolution by chaining
Hashing can be thought as a non recursive form of DAC. the input set of $n$ elements is divided randomly into $m$ subsets, each of approximate size $n/m$. A hash function determines which subset an element belongs to. Each subset is managed independently as a list.

![[Collision resolution by chaining.png]]
$$
fig :\text{Collision resolution by chaining.}
$$
each nonempty slot points to a linked list, and all the elements that hash to the same slot go into that slot’s linked list. Slot $j$ contains a pointer to the head of the list of all stored elements with hash value $j$ . If there are no such elements, then slot j contains $\text{NIL}$ .
The worst-case running time for insertion is $O(1)$. The insertion procedure is fast in part because it assumes that the element x being inserted is not already present in the table. To enforce this assumption, you can search (at additional cost) for an element whose key is $x$: key before inserting. For searching, the worst-case running time is proportional to the length of the list. Deletion takes $O(1)$ time if the lists are doubly linked, as in Figure 11.3. (Since `CHAINED-HASH-DELETE` takes as input an element $x$ and not its key $k$, no search is needed. If the hash table supports deletion, then its linked lists should be doubly linked in order to delete an item quickly.

>[!tldr] $\text{CHAINED-HASH-INSERT}(T, x)$
>$\small{\text{LIST-PREPEND}}(T[h(x.key)], x)$  

>[!tldr] $\text{CHAINED-HASH-SEARCH}(T,k)$
>return $\small \text{LIST-SEARCH}(T[h(k)], k)$  

>[!tldr] $\text{CHAINED-HASH-DELETE}(T,x)$
>$\small\text{LIST-DELETE}(T[h.key]),x$  
### Hashing Functions
An approach which tries to provide a single fixed hash function that works well one any data is called **static hashing**.
An approach of designing a suitable $family$ of hash functions and choosing a hash function at random, independent of the data to be hashed is called **random hashing**. 
A good hash function satisfies the assumption of independent uniform hashing.

##### Static hashing
Static hashing uses a single, fixed hash function. The only randomization available is through distribution of input keys.
###### The division method
The division method for creating hash functions maps a key $k$ into one of $m$ slots by taking the remainder of $k$ divided by m.  
The hash function is
$$
h(k)= k \text{ mod } m
$$

###### The multiplication method
The general **multiplication method** for creating hash functions operates in two steps. First, multiply the key $k$ by a constant $A$ in the range $0<A<1$ and extract the fractional part of $kA$. Then, multiply this value by $m$ and take the floor of the result. The hash function is
$$
h(k) = \lfloor m(kA \text { mod } 1) \rfloor
$$
where "$kA \text{ mod } 1$"  means the fractional part of $kA$, that is , $kA - \lfloor k A \rfloor$. The general multiplication method has the advantage that the value of $m$ is not critical and you can choose it independently of how you choose the multiplicate constant A.

#### Random hashing
Choosing the hash function randomly in a way that is independent of the keys is called random hashing. A special case of this approach is called universal hashing. It can yield provably good performance on average when collisions are handled by chaining.
 Let $\mathcal{H}$ be a  family of hash functions that map a given universe $U$ of keys into the range $\{0,1, \dots, m-1\}$. Such a family is said to be universal if for each pair of distinct keys $k1, k2 \in U$, the number of hash functions $h\in \mathcal{H}$ for which $h(k_1)/ = h(k_2)$ is at most ${|\mathcal{H}|/m}$. In other words, with a hash function randomly chosen from $\mathcal{H}$, the chance of a collision between distinct keys $k_{1}$ and $k_{2}$ is no more than the chance $1/m$ of a collision if $h(k_1)$ and $h(k_2)$ were randomly and independently chosen from the set $\{0,1, \dots, m-1\}$.
 ___
#### Achievable properties of random hashing
- The family $\mathcal{H}$ is uniform if for any key k in $U$ and any slot $q$ in the range $\{0, 1, \dots, m-1$\} , the probability that h(k) = q is 1/m. 
- The family $mathcal{H}$ is universal if for any distinct keys k1 and k2 in U, the probability that $h(k_{1}) = h(k_{2}$$ is at most $1/m$.
- The family $\mathcal{H}$ of hash functions is $\epsilon$-universal if for any distinct keys $k_{1}$ and $k_{2}$ in U, the probability that $h(k_{1}) = h(k_{2})$ is at most $\epsilon$. Therefore, a universal family of hash functions is also $1/m-\text{universal}$.
- The family $\mathcal{H}$ is $d$-independent if for any distinct keys $k_{1},k_{2},\dots, k_{d}$ in $U$ and any slots $q_{1}, q_{2}, . . . , q_{d}$ , not necessarily distinct, in $\{0,1, \dots, m-1\}$ the probability that $h(k_i) = q_i$ for $i = 1, 2, \dots , d$ is $1/m^d$.
##### Cryptographic hashing
Cryptographic hash functions are complex pseudorandom functions, designed for applications requiring properties beyond those needed here, but are robust, widely implemented, and usable as hash functions for hash tables.
A cryptographic hash function takes as input an arbitrary byte string and returns a fixed-length output. For example, the NIST standard deterministic cryptographic hash function `SHA-256 [346]` produces a `256-bit (32-byte)` output for any input.
There are many ways to use a cryptographic hash function as a hash function
for example
$$
h(k) = \text{SHA-256}(a||k)\space mod \space m
$$
To define a family of such hash functions one may prepend a "salt" string a to the input before hashing it, 
$$
h_{a}(k) = \text{SHA-256}(a||k)\space mod \space m
$$
where $a || k$ denotes the string formed by concatenating the strings $a$ and $k$.
___

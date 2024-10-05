### Algorithms 
An **algorithm** is any well-defined computational procedure that takes some value, or set of values, as **input** and produces some value, or set of values, as **output** in a finite amount of time.
As an example, suppose that you need to sort a sequence of numbers into monotonically increasing order. This problem arises frequently in practice.
Here is how we formally define the **sorting problem**.
- **Input** : A sequence of $n$ numbers $\langle a_1, a_2, ..., a_n \rangle$ 
- **Output** : A permutation (reordering) $\langle {a'}_1, {a'}_2, ..., {a'}_n\rangle$ of the input sequence such that ${a'}_1 \le {a'}_2 \le ...\le {a'}_n$
Thus, given the input sequence $\langle 31,41,59,26,41,58\rangle$, a correct sorting algorithm returns as output the sequence $\langle 26,31,41,41,58,59\rangle$. Such an input sequence is called an **instance** of the sorting problem. 
An algorithm for a computation problem is **correct** if, for every problem instance provided as input, it halts and outputs the correct solution to the problem instance.

### Data structures 
A **data structure** is a way to store and organize data in order to facilitate access and modifications. Using appropriate data structure is an important part of algorithm design.

This book also presents several data structures. A data structure is a way to store and organize data in order to facilitate access and modifications. Using the appropriate data structure or structures is an important part of algorithm design.

To express an algorithm, we will use Pseudocode. What separates pseudocode from real code is that in pseudocode, we employ whatever expressive method is most clear and concise to specify a given algorithm. Another difference between pseudocode and real code is that pseudocode often ignores aspects of software engineering$-$such as data abstraction, modularity, and error handling$-$in order to convey the essence of the algorithm more concisely.
### Algorithms as a technology
Algorithms are at the core of most technologies used in contemporary computers. They can be considered as a technology in their own right, with the following characteristics
- Efficiency
- Reusability
- Problem-solving tool
- Hardware/software tradeoff

>[!info]
>If computers were infinitely fast and computer memory were free, would you have any reason to study algorithms? The answer is yes, if for no other reason than that you would still like to be certain that you solution method terminates and does so with the correct answer.

#### Efficiency
Different algorithms devised to solve the same problem often differ dramatically in their efficiency. These differences can be much more significant that differences due to hardware and software.
As an example **insertion sort** takes time roughly equal to $c_1 n^2$  to sort $n$ items where $c_1$ is a constant and $merge sort$ takes time roughly equal to $c_2 n \space lg \space n$ where $lg \space n$ stands for $log_2 n$  and $c_2$ is another constant.

```c
void insertion_sort(item_type s[], int n) {
	int i, j; /* counters */
	for(i = 1; i<n; i++) {
		j = i;
		while( (j > 0) && (s[j] < s[j-1])) {
			swap(&s[j], &s[j-1]);
			j = j-1;
		}
	}
}
```

### Algorithms and other technologies
We should consider algorithms, like computer hardware as a **technology**.
Total system performance of a system depends on choosing efficient algorithms as much as on choosing fast hardware. 
- Programming Languages & Paradigms - The choice of programming languages can affect how easily an algorithm can be implemented and its efficiency.
- Computer Architecture - The underlying hardware also impacts the algorithm performance. Features like cache, parallel processing unit and memory hierarchy all play a role.
- Operating system - The way an operating system affect how efficiently system manages resources can affect how efficiently algorithms run.
- Networking - In distributed systems, network topology and protocols can be crucial in determining the overall efficiency of algorithmic solutions.

### The Impact of Algorithms
Algorithms have a profound impact on various fields, some of them are as follows :
- Scientific computing
- Operations research
- AI & ML
- Computer Graphics
- Cryptography
- Bioinformatics

___

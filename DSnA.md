# <h1 align="center"> Data Structures & Algorithms ❤️ (as read by Liya) </h1>

## DSA with JS Theoretical Prep

#### Algorithm

- In mathematics and computer science, an **algorithm** (ˈælɡərɪðəm) is a finite sequence of well-defined instructions, typically used to solve a class of specific problems or to perform a computation. 
- As an effective method, an algorithm can be expressed within a finite amount of space and time, and in a well-defined formal language for calculating a function. Starting from an initial state and initial input (perhaps empty),[ the instructions describe a computation that, when executed, proceeds through a finite number of well-defined successive states, eventually producing "output" and terminating at a final ending state.

In contrast, a **heuristic** is an approach to problem solving that may not be fully specified or may not guarantee correct or optimal results, especially in problem domains where there is no well-defined correct or optimal result.

##### Heuristic algorithm

- A **heuristic algorithm** is one that is designed to solve a problem in a faster and more efficient fashion than traditional methods by *sacrificing optimality, accuracy, precision, or completeness for speed*. 
Heuristic algorithms often times used to solve NP-complete problems (nondeterministic polynomial-time complete). In these problems, there is no known efficient way to find a solution quickly and accurately although solutions can be verified when given (Solved by brute-force?). Heuristics can produce a solution individually or be used to provide a good baseline and are supplemented with optimization algorithms. Heuristic algorithms are most often employed when approximate solutions are sufficient and exact solutions are unnecessarily computationally expensive.

***Polynomial time refers to an amount of time that is considered "quick" for a deterministic algorithm to check a single solution, or for a nondeterministic Turing machine to perform the whole search.***

![](http://www.cse.buffalo.edu/~rapaport/510/alg-shoe.gif)

#### Algorithmic (Computational) Complexity

**Computational complexity theory** focuses on classifying computational problems according to their resource usage, and relating these classes to each other. A computational problem is a task solved by a computer. A computation problem is solvable by mechanical application of mathematical steps, such as an algorithm.

A problem is regarded as inherently difficult if its solution requires significant resources, whatever the algorithm used. The theory formalizes this intuition, by introducing mathematical models of computation to study these problems and quantifying their computational complexity, i.e., the amount of resources needed to solve them, such as time and storage. Other measures of complexity are also used, such as the amount of communication (used in communication complexity), the number of gates in a circuit (used in circuit complexity) and the number of processors (used in parallel computing). One of the roles of computational complexity theory is to determine the practical limits on what computers can and cannot do.

- The **complexity of an algorithm** is the amount of resources required to run it. Particular focus is given to time and memory requirements. The complexity of a problem is the complexity of the best algorithms that allow solving the problem.

**[[ Most common time complexities ]](https://adrianmejia.com/most-popular-algorithms-time-complexity-every-programmer-should-know-free-online-tutorial-course/)**

**[[Contiguous & Non-contiguous Memory Allocation]](https://www.javatpoint.com/contiguous-and-non-contiguous-memory-allocation-in-operating-system)**

**[[Stuff]](https://www.studytonight.com/data-structures/search-algorithms)**


- **HOW** the N of operations grow as the input grows

##### Asymptotic Notation

- Asymptotic Notation is used to describe the running time of an algorithm - how much time an algorithm takes with a given input, n. There are three different notations: **big O, big Theta (Θ), and big Omega (Ω)**. big-Θ is used when the running time is the same for all cases, big-O for the worst case running time, and big-Ω for the best case running time.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--qKYRIPrd--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/9hizrsfgzjn7lt7djo82.png)

![](https://o.quizlet.com/PPLANaPuXai5RUUb1zUFYw_b.png)


#### Linear Data Structures

- A **linear data structure** has data elements connected to each other so that elements are arranged in a sequential manner and each element is connected to the element in front of it and behind it. This way, the structure can be traversed in a single run.

Array lists (+ dynamic), linked lists, stacks, queues.

##### Array lists

- elements are contiguously stored in memory

- `.add()`: O(1)
- `.get(index)`: O(1)
- `.insert(index, item)`: must shift `n` elements, O(n)
- `remove(index)`: ditto, O(n)



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

- `.add(item)`: O(1)
- `.get(index)`: O(1)
- `.insert(index, item)`: must shift `n` elements, O(n)
- `.remove(index)`: ditto, O(n)

- A fixed array is an array for which the size or length is determined when the array is created and/or allocated.[1]

- A dynamic array is a random access, variable-size list data structure that allows elements to be added or removed. It is supplied with standard libraries in many modern programming languages. 
##### Linked lists
- A linked list is a linear data structure in which elements are linked using pointers. It consists of nodes where each node contains a data field and a reference(link) to the next node in the list. NC.


- `.addFirst(value)`: O(1)
- `removeFirst()`: O(1)
- `.insertAfter(node, item)`: O(1)
- `.removeAfter(node)`: O(1)
- `find(value)`: O(n), must traverse

```js
class DoublyLinkedList {
    #head = null;
    #tail = null;
    #count = 0;

    addFirst(value) {
        const newNode = new LinkedListNode(value);
        if (!this.#head) {
            this.#tail = newNode;
        } else {
            this.#head.prev = newNode;
            newNode.next = this.#head;
            
        }
        this.#head = newNode;
        this.#count++;
    }

    removeFirst() {
        if (!this.#head) throw new Error('List is empty!');

        const val = this.#head.value;
        this.#head = this.#head.next;
        if (this.#head) this.#head.prev = null;
        
        this.#count--;
        
        return val;     

    }

    addLast(value) {
        const newNode = new LinkedListNode(value);

        if (!this.#tail) {
            this.#head = newNode;
        } else {
            this.#tail.next = newNode;
            newNode.prev = this.#tail;
            
        }
        this.#tail = newNode;
        this.#count++;
    }

    removeLast() {
        if (!this.#tail) throw new Error('List is empty!');
            
        const val = this.#tail.value;
        this.#tail = this.#tail.prev;
        if (this.#tail) this.#tail.next = null;
        
        this.#count--;
        
        return val;    

    }

    insertBefore(node, value) {
        if (!node) throw new Error('Invalid node!');
        
        const newNode = new LinkedListNode(value);
        
        if (node === this.head) {
            newNode.next = this.#head;
            this.#head.prev = newNode;
            this.#head = newNode;
        } else {
            newNode.prev = node.prev;
            newNode.next = node;
            node.prev = newNode;
            if (newNode.prev) newNode.prev.next = newNode;
        }
        
        this.#count++;
    }
    
    insertAfter(node, value) {
        if (!node) throw new Error('Invalid node!');
        
        const newNode = new LinkedListNode(value);
        
        if (this.#tail === node) {
            newNode.prev = this.tail.prev;
            this.#tail.next = newNode;
            this.#tail = newNode;
        } else {
            newNode.next = node.next;
            newNode.prev = node;
            node.next = newNode;
            if (newNode.next) newNode.next.prev = newNode;
        }
        
        this.#count++;
    }

    find(value) {

        let n = this.#head;

        while(n) {
            if(value === n.value) {
                return n;
            }
            n = n.next;
        }
        return null;
    }

    values() {
        const vals = [];
        
        let n = this.#head;
    
        while(n) {
            vals.push(n.value);
            n = n.next;
        }
        
        return vals;
    }

    get count() {
        return this.#count;
    }
    get head() {
        return this.#head;
    }

    get tail() {
        return this.#tail;
    }

}
```

##### Stack

- A stack is a linear data structure that stores data elements in a Last-In/First-Out (LIFO) or First-In/Last-Out (FILO) order. Here, a new element is added at one end and an element is removed from that end only. Resizable array/ LL.

`top`

- `.push(value)`: O(1)
- `.pop()`: O(1)
- `.peek()`: O(1)

```js
class Stack {
    #top = null;
    #count = 0;

    push(value) {
        const node = new LinkedListNode(value);
        node.next = this.#top;
        this.#top = node;
        this.#count++;
    }

    pop() {
        if (this.isEmpty) throw new Error('Stack is empty!');
        
        const topValue = this.#top.value;
        this.#top = this.#top.next;
        this.#count--;
        return topValue;
        
    }

    peek() {
        if (this.isEmpty) throw new Error('Stack is empty!');
        return this.#top.value;
    }
    
    get count() {
        return this.#count;
    }
    get isEmpty() {
        return this.#top? false : true;
    }
}
```

##### Queue

- A queue is a linear data structure that stores data elements in First-In/First Out(FIFO) manner, i.e., the element that’s inserted first will be removed first. RArr/LL/DoubleStack

- `.enqueue(value)`: O(1); at `tail`
- `.dequeue()`: O(1); from `head`
- `.peek()`: O(1) at `head`

```js
class Queue {
    #front = null;
    #back = null;

    #count = 0;
    

    enqueue(value) {
        const node = new LinkedListNode(value);
        if (this.isEmpty) {
            this.#front = node;
            this.#back = node;
        } else {
            this.#back.next = node;
            this.#back = node;
        }
        this.#count++;      

    }

    dequeue() {
        if (this.isEmpty) throw new Error('Queue is empty!');
        const value  = this.#front.value;
        this.#front = this.#front.next;
        this.#count--;
        return value;
    }

    peek() {
        if (this.isEmpty) throw new Error('Queue is empty!');
        return this.#front.value;
    }

    
    get isEmpty() {
        return this.#front? false : true;
    }

    get count() {
        return this.#count;
    }
}
```

### Hashing

**Hashing** is a method for storing and retrieving records from a database. It lets you insert, delete, and search for records based on a search key value. When properly implemented, these operations can be performed in constant time. In fact, a properly tuned hash system typically looks at only one or two records for each search, insert, or delete operation. This is far better than the O(logn) average cost required to do a binary search on a sorted array of n records, or the O(logn) average cost required to do an operation on a binary search tree.

Hashing is not good for applications where multiple records with the same key value are permitted. Hashing is not a good method for answering range searches. In other words, we cannot easily find all records (if any) whose key values fall within a certain range. Nor can we easily find the record with the minimum or maximum key value, or visit the records in key order. Hashing is most appropriate for answering the question, ‘What record, if any, has key value K?’ For applications where all search is done by exact-match queries, hashing is the search method of choice because it is extremely efficient when implemented correctly. 

[Intro](https://opendsa-server.cs.vt.edu/ODSA/Books/CS3/html/HashIntro.html)



**[HASH](https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/tutorial/)**
**[HASH FUNCS](https://opendsa-server.cs.vt.edu/ODSA/Books/CS3/html/HashFuncExamp.html)**

##### Collision

Collision resolution techniques can be broken into two classes: open hashing (also called separate chaining) and closed hashing (also called open addressing). (Yes, it is confusing when “open hashing” means the opposite of “open addressing”, but unfortunately, that is the way it is.) The difference between the two has to do with whether collisions are stored outside the table (open hashing), or whether collisions result in storing one of the records at another slot in the table (closed hashing).

The simplest form of **open hashing** defines each slot in the hash table to be the head of a linked list. All records that hash to a particular slot are placed on that slot’s linked list. The following figure illustrates a hash table where each slot points to a linked list to hold the records associated with that slot. The hash function used is the simple mod function.

![](https://gitlab.com/limeohme/theoretical-preparation/-/raw/main/images/open-hashing.png)

**Closed hashing** stores all records directly in the hash table. Each record R with key value kR has a home position that is h(kR), the slot computed by the hash function. If R is to be inserted and another record already occupies R’s home position, then R will be stored at some other slot in the table. It is the business of the collision resolution policy to determine which slot that will be. Naturally, the same policy must be followed during search as during insertion, so that any record not found in its home position can be recovered by repeating the collision resolution process.

One implementation for closed hashing groups hash table slots into **buckets**. The M slots of the hash table are divided into B buckets, with each bucket consisting of M/B slots. The hash function assigns each record to the first slot within one of the buckets. If this slot is already occupied, then the bucket slots are searched sequentially until an open slot is found. If a bucket is entirely full, then the record is stored in an overflow bucket of infinite capacity at the end of the table. All buckets share the same overflow bucket. A good implementation will use a hash function that distributes the records evenly among the buckets so that as few records as possible go into the overflow bucket.

##### Alternative bucket hashing

A simple variation on bucket hashing is to hash a key value to some slot in the hash table as though bucketing were not being used. If the home position is full, then we search through the rest of the bucket to find an empty slot. If all slots in this bucket are full, then the record is assigned to the overflow bucket. The advantage of this approach is that initial collisions are reduced, because any slot can be a home position rather than just the first slot in the bucket.
![](https://gitlab.com/limeohme/theoretical-preparation/-/raw/main/images/alt-bucket-hashing.png)

##### Closed Hashing No Bucketing, Collision Resolution

During insertion, the goal of collision resolution is to find a free slot in the hash table when the home position for the record is already occupied. We can view any collision resolution method as generating a sequence of hash table slots that can potentially hold the record. The first slot in the sequence will be the home position for the key. If the home position is occupied, then the collision resolution policy goes to the next slot in the sequence. If this is occupied as well, then another slot must be found, and so on. This sequence of slots is known as the probe sequence, and it is generated by some probe function that we will call p. 

- ***Linear probing:***

!! Primary clustering

![](https://gitlab.com/limeohme/theoretical-preparation/-/raw/main/images/closed-hash-linear-probing.png)

- ***Double Hashing***

![](https://gitlab.com/limeohme/theoretical-preparation/-/raw/main/images/double-shashing.png)

### Recursion 




![](https://pbs.twimg.com/tweet_video_thumb/C9_SP6KUIAAkYb-.jpg)

That's infinite, just sayin'.

In computer science, **`recursion`** is a method of solving a computational problem where the solution depends on solutions to smaller instances of the same problem. Recursion solves such recursive problems by using functions that call themselves from within their own code.

A recursive function definition has one or more `base cases`, meaning input(s) for which the function produces a result trivially (without recurring), and one or more `recursive cases`, meaning input(s) for which the program recurs (calls itself). For example, the factorial function can be defined recursively by the equations 0! = 1 and, for all n > 0, n! = n(n − 1)!. Neither equation by itself constitutes a complete definition; the first is the base case, and the second is the recursive case. Because the base case breaks the chain of recursion, it is sometimes also called the "terminating case".

[Recursive functions, general](https://plato.stanford.edu/entries/recursive-functions/)

##### Direct/Indirect Recursion

A function `func` is called direct recursive if it calls the same function `func`. A function `func` is called indirect recursive if it calls another function `other_func` and `other_func` calls `func` directly or indirectly. 

```js
function func() {
    // do something

    func()

    // something else
}
```

```js
function func() {
    // do something

    other_func()

    // something else
}
function other_func() {
    // do something

    func()

    // something else
}
```

##### Tail-recursion

A recursive function is tail recursive when a recursive call is the last thing executed by the function (after returning there is nothing left to evaluate).

```js
// tail
function func(n) {
    if (n === 0) {
        return;
    } else {
        console.log(n);
        return func(n-1);
    }
}

func(3); 
```
```js

function func(n) {
    if (n === 0) {
        return;
    } else {
        func(n-1); 
        // the logger must be evaluated after the recursive call
        console.log(n);
    }
}

func(3); 
```
##### Memoization
In computing, memoization or memoisation is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

```js
storage = {param1: result1, param2: result2}

function func(params) {
    if (params in storage) return storage[params];
    else: compute and store;
}
```

##### Backtracking

Backtracking is a general algorithm for finding solutions to some computational problems, notably constraint satisfaction problems, that incrementally builds candidates to the solutions, and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.

*constraint satisfaction problems*: are mathematical questions defined as a set of objects whose state must satisfy a number of constraints or limitations (sudokus, crosswords).  

The classic textbook example of the use of backtracking is the eight queens puzzle, that asks for all arrangements of eight chess queens on a standard chessboard so that no queen attacks any other. In the common backtracking approach, the partial candidates are arrangements of k queens in the first k rows of the board, all in different rows and columns. Any partial solution that contains two mutually attacking queens can be abandoned.

[8 Queens](https://www.interviewbit.com/blog/8-queens-problem/)

[Knight Through the Board](https://www.freecodecamp.org/news/backtracking-algorithms-explained/)

### Trees
**Node**
A node is an entity that contains a key or value and pointers to its child nodes.

The last nodes of each path are called leaf nodes or external nodes that do not contain a link/pointer to child nodes.

The node having at least a child node is called an internal node.

**Edge**

It is the link between any two nodes.

**Root**

It is the topmost node of a tree.

**Height of a Node**

The height of a node is the number of edges from the node to the deepest leaf (ie. the longest path from the node to a leaf node).

**Depth of a Node**

The depth of a node is the number of edges from the root to the node.

**Height of a Tree**

The height of a Tree is the height of the root node or the depth of the deepest node.

**Degree of a Node**

The degree of a node is the total number of branches of that node.

#### Binary Tree 

In computer science, a binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child.
- There is one root.
- There is only one path between a given node and the root. 

![](https://c.tenor.com/-GnZ6NOpsXkAAAAC/thats-all-folks.gif)

#### Binary Search Tree

In computer science, a binary search tree (BST), also called an ordered or sorted binary tree, is a rooted binary tree data structure whose internal nodes each store a key greater than all the keys in the node's left subtree and less than those in its right subtree. The time complexity of operations on the binary search tree is directly proportional to the height of the tree.
- The left subtree of a node contains only nodes with keys lesser than the node’s key.
- The right subtree of a node contains only nodes with keys greater than the node’s key.
- The left and right subtree each must also be a binary search tree.


[BST](https://www.javatpoint.com/binary-search-tree)

<table class="infobox-subbox infobox-3cols-child"><tbody><tr><th scope="row" class="infobox-label" style="white-space:nowrap;">Algorithm</th><td class="infobox-data infobox-data-a">
</td><td class="infobox-data infobox-data-b">
<b>Average</b></td><td class="infobox-data infobox-data-c">
<b>Worst case</b></td></tr><tr><th scope="row" class="infobox-label" style="white-space:nowrap;">Space</th><td class="infobox-data infobox-data-a">
</td><td class="infobox-data infobox-data-b">
<span class="texhtml"><span class="texhtml">O(<i>n</i>)</span></span></td><td class="infobox-data infobox-data-c">
<span class="texhtml"><span class="texhtml">O(<i>n</i>)</span></span></td></tr><tr><th scope="row" class="infobox-label" style="white-space:nowrap;">Search</th><td class="infobox-data infobox-data-a">
</td><td class="infobox-data infobox-data-b">
<span class="texhtml"><span class="texhtml">O(log <i>n</i>)</span></span></td><td class="infobox-data infobox-data-c">
<span class="texhtml"><span class="texhtml">O(<i>n</i>)</span></span></td></tr><tr><th scope="row" class="infobox-label" style="white-space:nowrap;">Insert</th><td class="infobox-data infobox-data-a">
</td><td class="infobox-data infobox-data-b">
<span class="texhtml"><span class="texhtml">O(log <i>n</i>)</span></span></td><td class="infobox-data infobox-data-c">
<span class="texhtml"><span class="texhtml">O(<i>n</i>)</span></span></td></tr><tr><th scope="row" class="infobox-label" style="white-space:nowrap;">Delete</th><td class="infobox-data infobox-data-a">
</td><td class="infobox-data infobox-data-b">
<span class="texhtml"><span class="texhtml">O(log <i>n</i>)</span></span></td><td class="infobox-data infobox-data-c">
<span class="texhtml"><span class="texhtml">O(<i>n</i>)</span></span></td></tr></tbody></table></td></tr></tbody></table>




A `balanced binary tree`, also referred to as a height-balanced binary tree, is defined as a binary tree in which the height of the left and right subtree of any node differ by not more than 1.

![](https://gitlab.com/limeohme/theoretical-preparation/-/raw/main/images/BST.png)

#### Breadth-first search

Breadth-first search (BFS) is an algorithm for searching a tree data structure for a node that satisfies a given property. It starts at the tree root and explores all nodes at the present depth prior to moving on to the nodes at the next depth level. Extra memory, usually a queue, is needed to keep track of the child nodes that were encountered but not yet explored.

For example, in a chess endgame a chess engine may build the game tree from the current position by applying all possible moves, and use breadth-first search to find a win position for white. Implicit trees (such as game trees or other problem-solving trees) may be of infinite size; breadth-first search is guaranteed to find a solution node if one exists.

In contrast, (plain) depth-first search, which explores the node branch as far as possible before backtracking and expanding other nodes, may get lost in an infinite branch and never make it to the solution node. Iterative deepening depth-first search avoids the latter drawback at the price of exploring the tree's top parts over and over again. On the other hand, both depth-first algorithms get along without extra memory.

```
BFS (G, s)                   //Where G is the graph and s is the source node
      let Q be queue.
      Q.enqueue( s ) //Inserting s in queue until all its neighbour vertices are marked.

      mark s as visited.
      while ( Q is not empty)
           //Removing that vertex from queue,whose neighbour will be visited now
           v  =  Q.dequeue( )

          //processing all the neighbours of v  
          for all neighbours w of v in Graph G
               if w is not visited 
                        Q.enqueue( w )             //Stores w in Q to further visit its neighbour
                        mark w as visited.
```

The time complexity of BFS is O(V + E), where V is the number of nodes and E is the number of edges.

#### Depth-first Search 

Depth-first search is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking. So the basic idea is to start from the root or any arbitrary node and mark the node and move to the adjacent unmarked node and continue this loop until there is no unmarked adjacent node. Then backtrack and check for other unmarked nodes and traverse them. Finally, print the nodes in the path.



![](https://gitlab.com/limeohme/theoretical-preparation/-/raw/main/images/DFSnBFS.png)
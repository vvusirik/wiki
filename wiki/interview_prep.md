# Interview Prep

## Coding Interviews
[Blind 75](https://leetcode.com/list/xi4ci4ig/) - a collection of commonly used interview questions that covers a range of data structures and algorithms concepts that are essential for coding interviews.

An outline for answering coding interview questions:
1. Read the prompt.
2. Ask clarifying questions.
3. Come up with an example (or add an example test case if you feel it would be better than the one given).
4. Analyze the prompt in terms of the example.
5. Start explaining your thought process for a potential solution. It doesn't have to be the optimal solution right away. 
    a. If there's a clear brute force solution and you can't think of the optimal solution right away, explain what the brute force is, what its time / space complexity is, and why it's suboptimal. 
    b. Start thinking through the checklist of data structures / algorithms that may help you solve the problem. Often this is about pattern recognition.
    c. Draw pictures and to help yourself and the interviewer visualize your solution.
    d. Write out a numbered list of logical steps (ie a code skeleton) that your code will take before writing the code itself.
       If you're typing out your solution, you can turn this numbered list into comments when you're implementing your solution.
    e. Talk through complexity analysis as part of this problem solving phase, you don't have to wait to mention it until after the coding as many candidates do. This shows that you're thinking about performance prior to coding.

7. Coding
    a. Speak as you're coding to let the interviewer know what each code snippet corresponds to in your logic 
    b. (If typing) Write comments as you're coding so that the interviewer can understand your thought process even after the interview or in case they missed something you explained as they were taking notes.
    c. Use type hints so it's clear what variables are
    d. If you need to handwave something and come back to it later, explain that you're doing that and will come back to it later.
       You can also mention optimizations / refactors that can be made that are lower priority in the moment, but show the interviewer that you're paying attention to detail.
   
### Problem Solving Techniques
There's a good chance you'll encounter a question that you haven't seen before, so it's important to have some techniques for problem solving an unfamiliar question.

* Build up a repertoire of solution patterns as you do practice problems. Often you'll see similarities in questions that use a common algorithm or data structure.
  As you do practice problems keep a mapping of data structure and algorithm type to each problem prompt and you'll 
  eventually be able to associate certain key words in a prompt with potential tools to solve it just through word association.

Some example problem patterns:
* Sorted array -> binary search
* Binary trees -> recursion over left / right subtrees, dfs, bfs
* Substrings -> 2 pointers
* Sorting / priorities -> Heaps
* Symmetrical patterns -> Stacks 
* Repetition of patterns -> Divide and conquer

* Break the problem down to the simplest possible base case and build up from there. 
  Some problems are very confusing when dealing with a complex case, especially problems that involve DP or recursion. 
  In these cases, it's much easier to consider the simplest possible example rather than the one that the interviewer has given you.
  Once you have a solution for the base case, the question becomes how do you solve the incremental case now that you know the base case answer.
* When practicing, implement the common data structures / algorithms by yourself at least once. 
  It's unlikely that you'll be asked to just implement a sorting algorithm from scratch, but this exercise gets you very familiar with the benefits, tradeoffs, use cases, and complexities of each data structure and algorithm and will help you recall the tools you have to for each coding question.

Follow these 5 steps for general problem solving during an interview:
1. Think of a brute force solution.
2. Simplify the problem / think of a solution for an easier version of the problem.
3. Visualize the problem (draw a sample tree, grid, graph, array, etc..).
4. Try finding a pattern with the simpler version of the problem.
5. Test solution on some examples.


#### Data Structures
You should know the time complexities associated with data structure opterations (like insertion, deletion, update, and search) for elements for the following:
* Array / Vector
* HashMap
* HashSet
* Linked List
* Doubly Linked List
* Stack
* Queue
* Deque
* Heap / Priority Queue
* Binary Tree
* Binary Search Tree
* N-ary Tree
* Trie
* Graph

##### Advanced Data Structures
* Bloom Filter
* Red-Black Tree / AVL Tree
* B-Tree

#### Algorithms
* BFS
* DFS
* (pre/in/post) order traversal
* Djikstra's
* Topological sort
* Quicksort
* Mergesort
* Binary Search
* Quickselect
* Prim's (MST)
* Union Find (Connected Components)
* Sliding Window
* Two Pointer
* Fast / Slow pointer
* Merge Intervals
* Backtracking

## Behavioral Interviews
Curate a list of experiences that you think would demonstrate valuable people skills. Reviewing these will give you starting points to relate behavioral questions to.

## System Design Interviews
A large part of the system design interview comes from building up an intuition from practical experience with industry tools.
However, there is plenty of great reading material on system architectures and their benefits and tradeoffs that will help you brush up if you're unfamiliar or rusty.

* Partitioning
* Replication
* Indexes
* Caching
* CAP Theorem
* async / await
* multiprocessing / multithreading
* Job Scheduler
* Batch Processing (Ex. Spark, Hive)
* Stream Processing (Ex. Kafka)
* Encoding (Ex. Thrift)
* Relational Databases
* Document Databases
* Colocation
* Load balancing
 
Reading
* Designing Data Intensive Applications

Watch system design talks:
* Slack - https://www.youtube.com/watch?v=WE9c9AZe-DY
* Instagram - https://www.youtube.com/watch?v=hnpzNAPiC0E

Do Exercises
From this book: https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF/ref=pd_bxgy_img_2/141-6791720-6254822?pd_rd_w=UTSsg&pf_rd_p=c64372fa-c41c-422e-990d-9e034f73989b&pf_rd_r=8ZXZYQEZV5F7YG9520BR&pd_rd_r=921cdb14-9e7a-4638-9b80-257b9e507f86&pd_rd_wg=cLZwx&pd_rd_i=B08CMF2CQF&psc=1&asin=B08CMF2CQF&revisionId=&format=4&depth=1
* Design a rate limiter
* Design consistent hashing
* Design key-value storage
* Design unique ID generator in distributed systems
* Design URL shortener
* Design web crawler
* Design notification system
* Design news feed
* Design chat system
* Design search autocomplete
* Design Youtube
* Design Google Drive

### Asking questions
It's very important to spend the beginning of the interview asking clarifying questions about the requirements of the system we're building.
This shows the interviewer how you deal with ambiguity and will help guide your design.
Ask questions along these 4 categories:
1. Users / Customers - Who is the audience for the system we're building? Could be powering an end user experience, internal use, could be used by data scientists, etc..
2. Scale (read / write) - How much data is coming into the system? How much data is transferred per query.
    i. Do we need to deal with traffic spikes 
3. Performance - What is the expected latency (both query latency and write to read)?
4. Cost - Development cost and cost of maintainence.

### Functional Requirements
Functional requirements comprise the actual functionalities that the system requires. As opposed to non-functional requirements like SLAs, latencies, QPS, etc..
In other words, these can be viewed as APIs (functions and the data they operate on):
notify(event, source_id, destination_id)

At this point, we should define the APIs that we want our system to implement.

### Non-functional Requirements
* System should be scalable, performant, and available
* Scalable - Can process lots of data
* Performant - API returns results quickly
* Available - System survives various failures, no single point of failure.
* Secondary concerns are consistency and cost minimization

### System Design Interview Steps
1. Ask clarifying questions
2. Gather functional requirements. Determine what data we need to store. Define schema and the operations that may occur on that data.
3. Gather non-functional requirements.
4. Start whiteboarding the high level components for a simple version of the system.
5. Discuss tradeoffs between different data model designs.

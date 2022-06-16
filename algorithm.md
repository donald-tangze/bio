### 1. Stack   

####  1.1 definition

Lifo，last-in-first-out, pop()  push()   

#### 1.2 leetcode example matching parentheses

(()())

> iterate the char[] of given String,
>
> ​	when it is open parentheses, push into Stack
>
> ​	when it is closed parentheses,  pop out the opposite open parentheses, if pop char failed, then it's not matching
>
> at last, verify the stack is empty,
>
> ​	if  the stack isn't empty, then it's not matching

#### 1.3 depth-priority search

### 2. Queue

#### 2.1 definition

Fifo， first-in-first-out

#### 2.3 width-priority search

leetcode question200

### 3.binary Tree

####  3.1 definition

> A `tree` is a frequently-used data structure to simulate a hierarchical tree structure.
>
> Each node of the tree will have a root value and a list of references to other nodes which are called child nodes. From graph view, a tree can also be defined as a directed acyclic graph which has `N nodes` and `N-1 edges`.
>
> 3 ways to `traversal`  a tree,    first is preorder Traversal 前序(root-left-right)， second is Inorder Traversal (left-root-right)中序， third is postorder traversal  (left-right-root) 后序
>
> alogrithm to search a tree

### 4.Graph

https://leetcode.com/explore/featured/card/graph/618/disjoint-set/

### 5.Array

### 6.LinkedList

### 7.Heap
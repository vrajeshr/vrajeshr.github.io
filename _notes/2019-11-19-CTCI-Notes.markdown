---
layout: post
title:  "CTCI Notes"
description: Notes I took while reading Cracking the Coding Interview.
date:   2019-11-19
---


# Big O
Try to remember this pattern. When you have a recursive function that makes multiple calls, the runtime will
often (but not always) look like O( branchesdepth), where branches is the number of times each recursive
call branches. In this case, this gives us O (2N)

![this](../assets/img/CTCI-Notes/BigO.png)

# Hashmaps 

Data structure that maps keys to values, 

Simple implementation is using linked list and a hash code.
    Hash code is something like hash(key) % array_len

# String Builder
String builders are better to use when concatanting strings

This fucntion would run O(xn^2) times because every iteration would copy O(x + 2x + 3x ... + nx)
```java
String joinWords(String[] words){
    String secntence = "";
    for(String w : words){
        sentence = sentence + w
    }
    return secntence
}
```

This function would run O(n) times becase it is just adding the sentences to each other.
```java
String joinWords(String[] words)}{ 
    StringBuilder sentence = new StringBuilder();
    for(String w : words)){
        sentence.append(w);
        sentence.append(' ');
    }
    return sentence.toString();
}
```

# Linked Lists

Simple singly linked list :

```java
class Node {
    Node next = null
    int data;
    public Node(Data d) { data = d; }
    void append(int d){
        Node end = new Node(d);
        Node n = this;
        while(n.next != null){
            n = n.next;
        }
        n.next = end;
    }
}
```

Deleting a node from a singly linked list:

```java
Node delete(Node head, int num){
    Node n = head;
    if(n.data == num ){
        return n.next;
    }
    while( n.next != null ){
        if( n.next.data == num ){
            n.next = n.next.next;
            return head;
        }
    n = n.next
    }
    return head;
}
```

Hare and tortoise technique : Have one "fast" pointer and one "slow" pointer every move and will detect 
	
# Trees

Trees are ternary trees. (10-ary tree, with up to 10 children nodes)

Binary trees are trees with up to 2 children

Binary tree vs Binary search tree:
- Bianry Search trees is a binary which every nodes a specific property
- All Left Descendent <= n < All right descendent

		Binary Search Tree : 

					8				
				  /    \			
				4		10			
			  /   \		 \		
			2		6		20		


Balanced :

- Balancing means that tree is "not terribly imbalanced", balanced enough to ensure O(log n)
- Common balanced trees are red-black trees and AVL trees

Complete binary tree:
    Binary tree in which each level of the tree is fully fixed, filled left to right

Full binary trees
    Each node has exactly 0 or 2 children (No children has 1 child)

Perfect Bianry tree:
    A tree that is both full and complete. 
    All leaf nodes are at the same level and the level has max num of nodes.

## Tree traversals : 

    Pre-order:
        print(node)
        traversal(node.left)
        traversal(node.right)

    In order:
        traversal(node.left)
        print(node)
        traversal(node.right)

    Post-ordeR:
        traversal(node.left)
        traversal(node.right)
        print(node)

## Min/max heaps:

Min heaps:
- A complete binary tree where each node is smaller than it's children

Max heaps:
- A complete binary tree where each node is larger than it's children
	
Insterting elements:
- Always start by inserting elements at the bottom, right-most spot to complete the tree property.
- Then fix the tree until the new element is either larger/smaller than it's children (bubbling) Takes O(log n) time

Extracting:
- Always the first element
- Remove the first element and swap it with the last element in the heap. (Bottom most, right most element)
- Then bubble down that element, swapping with the children until the min-heap property is satisfied

## Tries (Prefix trees)
	Each path down a tree represents a word.
	* node means null nodes, indicated complete words.
	
# Graphs

Tree is a type of graph, but not all graphs are trees.

A Tree is a connected graph without cycles.

A graph is a collection of nodes with edges between (some of) them

- Directed: one-way streets, one direction 
- Undirected : two-way streets, both directions
	
If there is a path between every pair of vertices == connected graph

No cycles == Acyclic graph

## Adjacency list
Most common representation of a graph

Every vertex (or node) stores a list of adjacent vertices
		

	0: 1
	1: 2
	2: 0, 3
	3: 2
	4: 6
	5: 4
	6: 5

## Adjacency Matrices

A NxN matrix where true values at matrix[i][j] indicates an edge from node i and node j 

![Example](../assets/img/CTCI-Notes/adjmatrix.png)

## Graph search
	
Common ways to search a graph is depth-first search and breadth first search

If we want to visit every node in the graph, DFS would be a bit simpler.

If we want to find the shortest path between 2 nodes, BFS is generally better. 

- Breadth first search
  - Uses a Queue
    -  Mnemonic  : BBQ => Barbeque => __B__*(readth)*__arbeque__*(ue)* => ***B***arbe***que***
  - Start at the root and explore each neighbor before going on to any of their children 
  - We go wide hence breadth
  - Example code:
    ``` java
    void DFS(Node root){
        visit(root);
        root.visited = true;
            for each (Node n in root.adjacent){
                if(n.visited == false)
                    DFS(n);
            }
        }
    ```
  	    
- Depth first search
  - Uses a Stack
  - Start at the root and explore each branch completely before moving to the next.
  - we go deep first, hence depth.
  - Example code:
    ```java
    void BFS(Node root) {
        Queue queue = new Queue();
        root.marked= true;
        queue.enqueue(root); // Add to the end of queue
        while (!queue.isEmpty()) {
            Node r = queue.dequeue(); // Remove from the front of the queue
            visit(r);
            foreach (Node n in r.adjacent) {
                if (n.marked == false) {
                    n. marked = true;
                    queue.enqueue(n);
                }
            }
        }
    }
    ```


# Bit Manipulation
## Addition ( + )
       0    0    1    1
      +0   +1   +0   +1
     ---  ---  ---  ---
      00   01   01   10

## Subtraction ( - )
		1	0	1	1	0	1	1
	−			1	0	0	1	0
		-------------------------
		1	0	0	1	0	0	1

## Multiplication ( * ) 
            1 0 1 1 1
           *  1 1 0 1
			--------- 
            1 0 1 1 1
		  0 0 0 0 0
        1 0 1 1 1
	  1 0 1 1 1
	----------------

## NOT(~)
- Complement of a number
- Flips the bits of the numbers.
  - N = 5 = 101
  - ~N = ~5 = ~101 = 010 = 2

## AND (&)
- Operates on 2 equal length bit patterns
- If both bits in the compared position of the bit is 1, then the resulting bit is 1, otherwise 0.
  - A = 5 = 101
  - B = 3 = 011
  - A & B = 101 & 011 = 001 = 1
  
## OR ( | )
- Operates on 2 equal length bit patterns
- If both bits in the compared position of the bit is 0, then the resulting bit is 0, otherwise 1.
  - A = 5 = 101
  - B = 3 = 011
  - A | B = 101 | 011 = 111 = 7

## XOR ( ^ )
- Operates on 2 equal length bit patterns
- If **both** bits in the compared position are 0 or 1, then the resulting bit is 0, otherwise 1.
  - A = 5 = 101
  - B = 3 = 011
  - A ^ B = 101 ^ 011 = 110


| X   | Y   | X&Y | X\|Y | X\^Y | ~(X) |
| --- | --- | --- | ---- | ---- | ---- |
| 0   | 0   | 0   | 0    | 0    | 1    |
| 0   | 1   | 0   | 1    | 1    | 1    |
| 1   | 0   | 0   | 1    | 1    | 0    |
| 1   | 1   | 1   | 1    | 0    | 0    |


## Left shift ( << )
- Operator that shifts the number of bits, in the given bit pattern, to the left. Then it will append 0's at the end. 
- Left shift is equivalent to multiplying the bit by 2<sup>k</sup> (if we are shifting k bits.
  - Base bit...........0001  = 1<sub>dec</sub>
  - 0001 << 1 =  0010 = 0001 * 2<sup>1</sup> = 2<sub>dec</sub>
  - 0001 << 2 =  0100 = 0001 * 2<sup>2</sup> = 4<sub>dec</sub>
  - 0001 << 3 =  1000 = 0001 * 2<sup>3</sup> = 8<sub>dec</sub>

## Right shift ( >> )
- Operator that shifts some number of bits to the right and append 1 at the end. 
- Equivalent to diving the bit by 2k
  - 00100 >> 1 = 00010 = 2
  - 00110 >> 1 = 00011 = 3
  - 00101 >> 1 = 00010 = 2
  - 10000 >> 4 = 00001 = 1

## Tricks
- 0110 + 0110 == 2 * 0110 == 0110 << 1
- 0100 * 0011 -> Multiplying by 4 is the same as left shifting 2
  - 0011 = 3, 0011 << 2 = 1100, 12
- 1101 ^ (~1101) = a^(~a) will always be a seq. of 1's

|              |             |                |
| ------------ | ----------- | -------------- |
| x ^ 0's = x  | x & 0's = 0 | x \| 0's = x   |
| X ^ 1's = ~x | x & 1's = x | x \| 1's = 1's |
| x ^ x = 0    | x & x = x   | x \| x = x     |

## Two's compliment and negative numbers

- 3 = 011
- flip = 100
- add 1 = 101
- add sign bit = 1101

Arithmetic vs Logical right shift
- Arithmetic basically divides by 2.
  
    ![this](../assets/img/CTCI-Notes/ArithmeticShift.png)
    - We shift the valuse to teh right and fill in teh new bit with the sign bit.
    - This (roughly) divides by 2. 
    - Indicated by >>
        
- Logical right shift does 

    ![this](../assets/img/CTCI-Notes/LogicalRightShift.png)
    - We shift the bits and put a 0 in the most significant bit
    - indicated with a >>> operator



End @133 drive


=======================================================================================

# OTHER NOTES
 
Compile time polymorphism (static polymorphism)

- Polymorphism that can be resolved during compile time. Method overloading can be an example of this

```java
class Example{
	int add (int a, int b){
		return a + b;
	}
	
	int add (int a, int b, int c){
		return a + b + c;
	}
}

public class Main{
	Example obj = new Example();
	cout << obj.add(1,2);
	cout << obj.add(1,2,3);
}
```

Runtime polymorphism

- A call to an overriden method is resolved at runtime

```java
class ABC{
   public void myMethod(){
	System.out.println("Overridden Method");
   }
}
public class XYZ extends ABC{

   public void myMethod(){
	System.out.println("Overriding M2312312ethod");
   }
   public static void main(String args[]){
	ABC obj = new XYZ();
	obj.myMethod();
   }
}
```
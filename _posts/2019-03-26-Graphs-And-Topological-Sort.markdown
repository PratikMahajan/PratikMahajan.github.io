---
layout: post
title:  "Graphs and Topological Sort"
date:   2019-03-26 17:08:49 -0800
categories: Graphs
---
## Types of Nodes:
1. Black: No outgoing or all outgoing nodes are visited
2. Grey: Currently exploring the node, but not yet finished
3. White: Currently unexplored node, i.e. not yet visited

## Types of Edges:
1. Grey to White: Discovery Edge
2. Grey to Grey: Back Edge
3. Grey(first) to Black: Forward Edge
4. Grey to Black(first): Cross Edge

## What is Discovery Time and Finish Time:
Consider that you start at node A. The discovery time of this node will be 1 as it is the first node. As we go deep into the graph, keep incrementing this number. When we reach a node which has no outgoing edge, we consider that the discovery of this node is complete, thats when we mark it as finish time. As we come one level up after completed discovery, we still keep on incrementing this time untill the end of algorithm. This time can be imaginary and we dont have to keep track of it. Its just the order in which we discover and finish discovering a node. Thus the source will be the first one to be discovered and last one to be finished in its own tree. 

## Topological sort with DFS Algorithm basics:
* If next node is white, convert it from white to grey and keep going deep. 
* if there is no outgoing node from the current node, convert it to black and go one level up. 
* Once all the node is marked as black, insert it to the front of the LinkedList that keeps node in a topologically sorted order.
* If all child nodes are black, convery the current node(grey) to black and go one level up. 
* If while exploring, we encounter a node which is grey, there is a cycle in graph. (Cycle should not be there in a DAG- Directed Acyclic Graph). Its better to check for this condition as it has various uses in Algorithms. In this case, add this node to a list of cycling nodes. One way to handle it can be convert it to black and go one level up. 
* If all nodes originating at one source are traversed, check if there is any independent tree in the graph. If yes, continue the same algorithm again. 

Here,
* Visited :
	* Can be an array where 
		* 0-> White
		* -1 -> Black
		* 1 -> Grey
	* if we consider it as a `set` , we will have to maintain 3 sets, one each for white, grey and black. 
* We will have to maintain a LinkedList to keep toplogically sorted nodes in order. Or we can also use an OrderedDict which is nothing but a datastructure made up of dictionary and linkedlist. 

## Topological Sort Algo:
*According to Algorithm Design-CLRS*<br/>
TOPOLOGICAL-SORT(G)<br/>
1. call DFS(G) to compute finishing times 􏰁v.f for each vertex 􏰁v<br/>
2. as each vertex is finished, insert it onto the front of a linked list<br/>
3. return the linked list of vertices<br/>


## Problem Statement
The goal is to find the minimum spanning tree of the graph. Define the weight of the tree as the sum of weight of each edge. Then, the MST is the tree touching each edge which has the minimum weight.

## Observations
* Divide the graph into two subgraphs, $(S, V-S)$. The lightest edge crossing between these two sub-graphs must be in the MST. If it is not, then we can generate a minimum spanning structure of smaller size by replacing it with the smallest such edge.

## Pseudo-Code
```
sort edges in increasing order of weight.      -- O(E.log(E))
define T as the set of all edges in the MST.

for each (edge e) with (i from 0 to E),        -- O(E)
	if adding e to T does not make a cycle,   
		add e to T.                            -- O(1), upto V times
``` 

This requires $V$ Find / Union operations to add a point to the chart. We can perform a find union in $O(log^*n)$ time with path compression technique, which makes the complexity basically $O(V)$. Total complexity is given as $O(E.\log(V))$ 

## Find-Union Algorithm
Basically, we link each element to it's "parent". For each chain, there is a ternimating element. We consider this as the parent of the graph component. If two elements share the same parent / leader, a cycle is formed. This can be evaluated very quickly.


## Correctness
Correctness of Kruskal's algorithm can be proven by contradiction.

Kruskal's algorithm produces a graph with no cycles, by definition of the algorithm. That is the first requirement.

Secondly, Consider a situation with components $S$ and $S'$, and an edge $e$ between them, given by Kruskal's algorithm. Assume there exists an edge $e'$, such that picking $e'$ over $e$ gives a better outcome. Since the weights inside $S$ and $S'$ are independent of which edge is chosen, the difference comes only from this bridge edge. Since Kruskal's algorithm selects edges in ascending order of weight, if $e'$ were truly lighter than $e$, it would've been chosen first. 


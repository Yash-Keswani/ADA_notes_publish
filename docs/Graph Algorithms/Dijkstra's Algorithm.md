## Problem Statement
The goal of Dijkstra's algorithm is to find all the shortest paths connecting a source vertex $S$, to every vertex in a directed graph. It can also be used to calculate just one Source-Destination pair efficiently.

## Approach
We will divide the graph into two components, $S$ and $S'$. In $S$, we store all the points whose shortest distance from the origin we know of. The goal will be to expand $S$ till eventually it includes every point in the graph.

## Observations
* If we know the distance to every point in some region $S$, we can tell with certainty the shortest distance to one and only one point in $S'$ with absolute certainty. 
* This point is the one with the minimum value of shortest distance to any point in $S$, i.e. the closest point to $S$.
* Any other point may have a shorter path to it from $S$, which flows through this optimal path. 
* At the start, the optimal path is only known for the source.

## Pseudo-Code
```
set distance of each vertex from source to +inf.
create a min heap H with all vertices in, measured by their distance.

while H is not empty,
	frontier vertex f = delete_min(H).           - O(V. log V)
	for all outgoing edges from (fv) to S',      - O(E. log V)
		relax d[v] till d[f] + l[fv].
		update the heap to reflect this change.  - O(log V)
```

## Runtime
We run heapify every time a point is moved into the frontier. As this happens no more than $V$ times, the time taken by this is $O(V \log V)$. 

We check each edge once for potential relaxation and heap reset. So the runtime of this part is $O(E \log V)$. Therefore the total runtime is $O((E + V)log(V))$  

## Proof Of Correctness
This proof is performed via induction.

At any iteration, suppose $f$ is the frontier vertex, being moved from $S'$ to $S$. Then, d\[w] is the shortest path length from $S$ to $w$ 

Base Case - $S = \{s_0\}$

Induction Hypothesis - Suppose we have $S$ of some arbitrary size, and are moving a vertex $f$. 

$$d[f] = d[u] + l_{uw} \quad [U \in S]$$

Suppose an alternate shorter path $P$ exists. If it connects directly from $S$ to $f$, then it cannot be shorter than the existing path. If it connects through $S'$, it connects through another vertex, which is further apart, making it longer than the path given by Dijkstra.
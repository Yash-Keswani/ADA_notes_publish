## Problem Statement
Imagine a directed graph, except now it has negative length edges too. Dijkstra's algorithm is no longer sufficient for this purpose. 

## Observation
This problem may not have a defined solution in the first place. In the presence of a negative cycle, there will be no longest path connecting a source to its destination.

## Approach
Bellman-Ford handles this problem with a Dynamic Programming approach. The optimal path to a point is defined with both the terminal point, and the maximum number of edges in the path.

## Pseudo-Code
```
define dp table of size V x V.
set dp of all lengths pointing to the source as 0.
set dp of zero length pointing to any vertex as 0.

for each (length i) from (1 to n-1),                   - O(V^3)
	for each (vertex v),                               - O(V^2) 
		for each edge going into v (parent vertex u),  - O(V) 
			dp[v, i] = min(dp[u, i-1] + l[u, v]).      - O(1)
```

## Runtime Analysis
This algorithm has a runtime of $O(VE)$. 

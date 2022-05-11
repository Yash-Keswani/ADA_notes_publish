## Problem Definition
Given a set of $n$ matrices {$A_i$}, the goal of this algorithm is to multiply matrices in the optimal order, to minimise number of computations required.

## Motivation
Multiplying matrices quickly is obviously important for many mathematical tools (_cough cough_, linear algebra), but the applications of this algorithm are far beyond that. Anything which involves optimally combining $n$ elements, with known costs / benefits of combining $k\; (< n)$ elements can utilise this algorithm.   

## Subproblem Definition
$\Omega(X)$ = Optimal cost for computing value of $X$ (contiguous) matrix set.
$\sigma(X, Y)$ = Cost of multiplying the result of $X$ matrix set and $Y$ matrix set. Equivalent to $rows(X_1) \cdot cols(Y_y)$

## Recurrence 
$$\Omega(A) = min(\Omega(X) + \Omega(X') + \sigma(X,X'))$$
provided $X$ and $X'$ constitute the optimal breakdown of matrix set $A$, assuming $X$ ends at element $A_k$. We can do this by considering every breakdown, and taking the minimum of those. 

Base Case: $\Omega(M) = 0$ if $|M| = 1$

## Complexity
The DP table has a size of $n^2$, and filling each cell takes a time of $O(n)$. This gives us a total complexity of $O(n^3)$. The space complexity is proportional to the size of the table, which is just $O(n^2)$.  Note that we only fill the upper triangle of the DP table.

## Pseudo-Code
```
for i form 1 to n:
	DP[i, i] = 0 
for length from 1 to n-1:
	for i from 1 to n-length:
		j = i + length
		tot_min = 1000000000
		for k from i+1 to j:
			DP[i, j] = min{tot_min, DP[i, k] + DP[k+1, j] + sigma(k)}
return DP[1, n]
```

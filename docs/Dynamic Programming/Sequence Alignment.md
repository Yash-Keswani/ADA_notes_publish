## Edit Distance
The Needleman-Wunsch score defines the edit distance as the sum of 'cost' of mismatches and the 'cost' of gaps.

## Motivation
Edit distance is useful for finding the difference between two strings. This is helpful in using `diff` operations, autocorrect, speech recognition, and computational biology.

## Problem Definition
We are given two strings, $X = [x_i]$ and $Y = [y_i]$  of lengths $m$ and $n$ respectively. The goal is to find the insertion of gaps so as to achieve the minimum edit distance for these two strings.

$\Omega(A, B)$ = optimal solution for strings $A$ and $B$.

## Subproblem Definition
Let's look at the end of these strings. We have three possibilities. One is that they're both perfectly aligned, the other two involve one of them ending in a gap. Let us define the ideal strings (gaps included) as $X'$ and $Y'$, of lenths $m'$ and $n'$  respectively. We may end up with three cases:

1) $m = n$ => $\Omega(X,Y) = f(\Omega(X-x_m, Y-y_n))$ 
2) $m > n$  => $\Omega(X,Y) = f(\Omega(X-x_m, Y))$
3) $m < n$  => $\Omega(X,Y) = f(\Omega(X, Y-y_n))$

## Proof of Optimal Substructure
Claim: $\Omega(X,Y)$ with $x_m, y_n$ removed = $\Omega(X-x_m, Y-y_n)$.
$$\quad Let \ \Omega (X, Y) = \Omega (X-x_m, Y-y_n) + \alpha (x_m, y_n)$$
If there is any other string $\overline{X}$ , $\overline{Y}$ that gives $\Omega(\overline{X},\overline{Y}) > \Omega(X-x_m, Y-y_m)$, that would imply that $\Omega(\overline{X}, \overline{Y}) + \alpha (x_m, y_m)$ > $\Omega(X, Y)$, which would violate the optimality of the solution. Therefore, no such string is possible.

## Recurrence Relation
Define $A_i$ as the string $A$ up till $i$ (included)
$$
\quad \Omega(X_i, Y_j) = min
	\begin{cases}
	\Omega(X_{i-1}, Y_{j-1}) + \alpha(x_i, y_j) \\ 
	\Omega(X_{i-1}, Y_j) + \alpha(gap) \\
	\Omega(X_i, Y_{j-1}) + \alpha(gap) \\
	\end{cases}
$$
Base Case:
$$\begin{align}
  \quad & \Omega(X_i, 0) = i \cdot \alpha(gap)\\
        & \Omega(0, Y_j) = j \cdot \alpha(gap)
\end{align}$$
## Complexity
This gives us time and space complexities of $\Theta(mn)$ , when we memoise the DP table.

## Pseudo-Code
```
Define P[m+1, n+1]
Align (X, Y):
	for each i: P[i, 0] = i.alpha(gap)
	for each j: P[0, j] = j.alpha(gap)
	for i from 1 to m:
		for j from 1 to n:
			P[i, j] = min(P[i-1, j-1] + alpha(x[i], y[j]),
						  P[i, j-1] + alpha(gap)
						  P[i-1, j] + alpha(gap)
						  )
	return P[m, n]
```

## Space Optimisation
Each row only needs the values in the current row, and the row above it to fill (provided we are filling the table in row major). In this scenario, we choose to only store the current row and the row above it. This improves our time complexity to $O(min(m, n))$.


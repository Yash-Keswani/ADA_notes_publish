## Problem Statement
You are given an array of size n containing integers. Design a linear time algorithm to find the contiguous sub-array such that the sum of elements is as large as possible.
___
## Recurrence Relation
$a_i$ := the i'th element of the array
$S_i$ := sub-sequence of largest value ending at $i$, including $a_i$
$\Omega_i$ := sum of all elements in $S_i$

Suppose we are at $a_i$. Consider the sub-sequence $S_i$. If $\Omega_{i-1}$ is positive, then  
$$
\quad \Omega_i = \Omega_{i-1} + a_i
$$
Otherwise,
$$
\quad \Omega_{i} = a_i
$$
This gives the general value of $\Omega_i$ as
$$
\quad \Omega_i = max{
	\begin {cases}
		\Omega_{i-1} + a_i & \\
		a_i & \\
	\end {cases}
}
$$
Since the largest sub-sequence possible must end at *some* position, we can find it with the expression,
$$\quad \Omega = max(\Omega_i)$$
___
## Recursive Algorithm
Base Case: 
* for i = 0, $\Omega_i$ = 0

Recursive Case:
* $\Omega_i = max(\Omega_{i-1} + a_i, a_i)$

Starting Point:
* $\Omega_n$

Alternatively, we can perform this iteratively by calculating all $\Omega_i$ from 1 to n in that order.
___
## Complexity
This algorithm performs $n$ passes to calculate each value of $\Omega_i$ , then performs $max$ operation in $n-1$ comparisons. This gives us a time complexity of $O(n)$, i.e. linear.

Additionally, it has space complexity of $O(n)$ with a naive approach, that can be optimised to $O(1)$, by storing ($\Omega_i$ , $\Omega_{i-1}$ , and $\Omega_{max}$ only)
___
## Runtime Implementation
Let a be $1, 2, 5, -1, -3, -20, 4, 2, 1$ 

| i          | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
| ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| $\Omega_i$ | 1   | 3   | 8   | 7   | 4   | -16 | 4   | 6   | 7   |

$max(\Omega_i)$ = 8
___

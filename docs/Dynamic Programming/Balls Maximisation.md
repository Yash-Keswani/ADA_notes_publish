## Problem Statement
Say you have an array of balls with weights
$$[2, 5, 6, 4, 3, 5]$$
You aren't allowed to pick adjacent balls. The goal is to maximise the weight of balls that you choose.

## Greedy Approach
Pick the ball with the maximum weight, unless you have picked any of its neighbours. Repeat till no other ball can be picked.

This seems (somewhat) sound, but can be disproved quickly via counterexample.

## Recursive Approach
The goal of the recursive approach is to break this problem into subproblems, such that an inner subproblem should never have to rely on the output of an outer subproblem.

### Problem Definition
$B_i$ := the i'th ball
$W_i$ := the weight of the i'th ball
$S_i$ := the optimal selection of balls up till the i'th ball
$\Omega_{\,i}$ := the optimal weight possible from selecting balls $B_1$ through $B_i$

The desired solution is $\Omega_{\,n}$
<div style="page-break-after: always;"></div>
## Recurrence Relation
Consider the series 
$$\quad B_1, B_2, B_3, B_4, ... B_{n-1}, B_n$$
$B_i$ may or may not be a part of $S_i$. In the event that it is, $B_{i-1}$ cannot be a part of $S_i$. So, the optimal weight becomes
$$\quad W_i  + \Omega_{\,i-2}$$
In the other case, $B_i$ is not a part of $S_i$ ,anything from $B_1$ to $B_{i-1}$ may be included in $S_i$. However, this means that $S_i$ and $S_{i-1}$ must be the same (by definition). This gives us the final weight as
$$\quad \Omega_{i-1}$$
We have the power to choose from either of these cases. And because we want the maximum weight overall, we will choose maximum of the two possibilities. This gives us the optimal solution as
$$
\quad \Omega_i = max
	\begin {cases}
		W_i + \Omega_{i-2} & \; B_i \; selected\\
		\Omega_{i-1} & \; B_i \; not\  selected\\
	\end {cases}
$$
## Recursive Algorithm
Base Case: if i=1, $\Omega_i$ = $W_i$
Recursive Case: if i > 1, $\Omega_i$ = $max(W_i + \Omega_{i-2},\; \Omega_{i-1})$ 
Starting: $\Omega_n$

#### Runtime
The runtime is observed as $O(2^n)$, which honestly sucks.

#### Memoisation
With memoisation, we can boost the runtime to $O(n)$, which is honestly epic.
However, this means we also needs $O(n)$ space alongside it.
<div style="page-break-after: always;"></div>
## Iterative Algorithm
The iterative approach converts this recursive algorithm to an iterative one.

for each $i$'th ball from left to right,
	$\sc{SELECT}\sc{UPTO}(i)$

Where $\sc{SELECT}\sc{UPTO}$ is the same as that of the recursive algorithm.

## Reconstruction
A ball is only added to the set if Case I is achieved, i.e. if it's better to add it.

so we can modify the algorithm as such,

```
S = []
i = n
while i >= 1:
	if maxw[i] = maxw[2] + W[i]:
		add B[i] to S
		i -= 2
	else:
		i -= 1
```

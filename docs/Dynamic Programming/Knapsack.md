## Problem Statement
Say you have a knapsack of size $W$ ($W \in I, W > 0$). You have $n$ indivisible items to put in that knapsack. Each item has a weight of $w_i$ , and value of $v_i$ . Your goal is to maximise the value inside the knapsack, without overfilling it.
___
## Greedy Approach
Start by picking the ball with highest value of $v_i / w_i$ . Repeat this until the knapsack is filled.

While this approach seems intuitive, it may fail. 

Consider this example

| $w_i$ | $v_i$ | $v_i/w_i$ |
| ----- | ----- | --------- |
| 1     | 2     | 2         |
| 100   | 199   | 1.99      |

$W = 100$

in this case, the greedy approach starts by picking the first item. Then it picks one of the remaining items. This gives us a final value of 2 in the knapsack. Meanwhile, by picking the last item, one can get a value of 199. This can be extended to get a ratio between the optimal and greedy value as high as possible.
___
## Recursive Approach

$I_i$ := the $i'th$ item
$w_i$ := weight of the $i'th$ item
$v_i$ := value of the $i'th$ item
$W$ := maximum weight in knapsack
$w$ := weight of knapsack in subproblem
$vmax(i, w)$ := optimal solution for given value of $i$ and $w$

Consider the final state in which we have every optimal item in the knapsack. Now let us follow the steps of this approach in reverse. 

Say the last item was in the knapsack. So we remove this item. Now the knapsack is optimal for a weight up till $W - w_n$ , and can only contain items between $1$ and $n-1$.

Otherwise, the last item cannot be in the knapsack. So, the knapsack must contain items between $1$ and $n-1$, and must be optimal up to a weight of $W$. 

Now we end up in the same state as before. We can repeat this till we get to any $i'th$ item. So, the recurrence relation for the $i'th$ item is given as
$$
vmax(i, w) = max \begin {cases}
	vmax(i-1, w-w_i) + v_i & \quad I_i \; chosen \\
	vmax(i-1, w) & \quad I_i\; not\ chosen\\
	\end {cases}
$$
___
## Recursive Algorithm

Base Cases: 
* for $w=0$, $vmax =0$ {there is no space to add elements}
* for $i = 0$, $vmax = 0$ {there are no elements to add}

Recursive Case:
* $vmax(i,w) = max(vmax(i-1, w-w_i) + v_i, vmax(i-1, w))$ 

Starting:
* $vmax(n, W)$ 

#### Runtime
This algorithm has a runtime of $O(2^n)$, which again kinda sucks.

#### Memoisation
With the power of memoisation, we can reduce the runtime to $O(nW)$ {which needn't necessarily be better than $2^n$, but it'll mostly be}.

This is referred to as a pseudopolynomial runtime.

However, we will need $O(nW)$ space to use memoisation. This isn't always desirable.
___
<div style="page-break-after: always;"></div>

## Runtime Demonstration

| I   | w   | v   |
| --- | --- | --- |
| 1   | 4   | 3   |
| 2   | 3   | 2   |
| 3   | 2   | 4   |
| 4   | 3   | 4   |

$W=6$

| i\\w  | 0   | 1        | 2   | 3        | 4   | 5   | 6        |
| ----- | --- | -------- | --- | -------- | --- | --- | -------- |
| **0** | 0   | <u>0</u> | 0   | 0        | 0   | 0   | 0        |
| **1** | 0   | <u>0</u> | 0   | 0        | 3   | 3   | 3        |
| **2** | 0   | <u>0</u> | 0   | 2        | 3   | 3   | 3        |
| **3** | 0   | 0        | 4   | <u>4</u> | 4   | 6   | 7        |
| **4** | 0   | 0        | 4   | 4        | 4   | 8   | <u>8</u> |
___
## Iterative Approach
An iterative approach to this problem just focuses on filling the table. We can traverse row major or column major.

```
for w = 0 to W:
	vmax[0, w] = 0
for i = 1 to n:
	for i = 0 to W:
		if (wt[i] > w):
			vmax[i, w] = vmax[i-1, w]
		else:
			vmax[i, w] = max(vmax[i-1, w], vmax[i-1, w - wt[i]] + v[i])
return vmax[n, W]
```


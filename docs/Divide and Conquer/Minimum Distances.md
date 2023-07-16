This algorithm involves finding the closest point pair in a lattice of $n$ points.

## Motivation
This algorithm can be used to find the closest entity to a user, whether it is a cab or a restaurant, by knowing the locations of both bodies. 

## 1-D Case
In 1 dimension, there's a straightforward solution to this. We can sort the points and measure the distance between each point and its adjacent point, while storing the minimum distance so far. This will give us an easy way to get the minimum distance between any pair.

## 2-D
Unfortunately such an algorithm won't work in 2D. An alternative approach helps us though.

For the array $P$, let $P_x$ be $P$ sorted by the x co-ordinate, and $P_y$ be $P$ sorted by the y co-ordinate. 

The next step is to divide $P_x$ by its median. Since these points are sorted, the median can be derived in $O(1)$ time.

## Divide and Conquer
The median divides $P_x$ into $Q_x$ and $R_x$, and $P_y$ into $Q_y$ and $R_y$. $Q_x$ and $R_x$ can be computed in $O(1)$, $Q_y$ and $R_y$ in $O(n)$ time. 

$$ClosestPair(P_x, P_y)$$

can be defined as 

```
ClosestOf(
	ClosestPair(Q_x, Q_y),
	ClosestPair(Q_x, Q_y),
	ClosestSplitPair(Q_x, Q_y, R_x, R_y)
)
```

The first two can be found recursively, the last one however, is more complex.

## Closest Split Pair
The closest split pair can be found by such. Call the minimum distance of closest pair on either side as $\delta$. Then look at all points within a $\delta$ neighbourhood of the median. Any point outside this neighbourhood cannot possibly be the closest split pair.

Traverse through points ahead of the top-most point. While you traverse downward, compare each point to the $7$ points ahead of it. Find the situation with the minimum distance in such a scenario.

## Why 7?
Take an arbitrary point $p$. Assume there is at least one point ahead of it in a $\delta$ neighbourhood. Now draw 8 boxes of width and height $\delta/2$ below $p$. Anything outside these boxes is further than $\delta$ away from p, and thus cannot be a candidate point. Furthermore, there can be only as many as 7 other points in these boxes. Any more and you have 2 in the same box, which gives us a distance between those two points of no more than $\delta/\sqrt2$ .

Suppose there is a point $q$ less than $\delta$ away from $p$ . This point must lie in one of the eight boxes. The maximum number of points we can fit between $q$ and $p$ is seven. Any more, and the closest point pair wil no longer be $p$ and $q$, but two of the internal points.

## Time Complexity
Sorting Points > $O(n.logn)$
Closest Split Pair > $O(n)$

Recurrence > $T(n) = 2T(n/2) + O(n)$
Solution > $O(n.logn)$ from Master's Theoreom

## Psuedo-Code
```
ClosestSplitPair(Q, R):
	select all points in delta-neighbourhood of divider
	start with top-most point
	min_dist = really_really_large
	for point S in set:
		calculate distance with 7 points ahead of S as T
		if any of these < min_dist:
			min_dist = this
	return min_dist	

ClosestPair(P):
	start with point set P
	sort in X and Y to get Px and Py
	divide P by median of Px, making Q and R
	get Qx, Qy, Rx, and Ry

	pair_q = ClosestPair(Q)
	pair_r = ClosestPair(R)
	pair_split = ClosestSplitPair(Q, R)
	return closest(pair_q, pair_r, pair_split)

```
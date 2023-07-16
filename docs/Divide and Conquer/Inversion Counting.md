Consider the sorted array,

$$[1, 2, 3, 4, 5, 6, 7, 8]$$

and the unsorted array,

$$[4, 3, 5, 2, 7, 6, 8, 1]$$
The pair $(4,3)$ is out of order in the unsorted array. Let us call this out-of-order-pair as an inversion. 

## Motivation
Why do we care about the number of inversions? Suppose we ask two people to give ratings to elements in a set. This is done often with movie or show review websites, but can also be applied to other things like elections. 

## Naive Approach
A naive approach would look at every pair of elements from $1$ to $n$. It will then check if this $(i, j)$ pair is inverted or not. There will be $nC2$ such pairs, giving us a complexity of $O(n^2)$

## Divide-and-Conquer Approach
The key observation here is:

Suppose we partition the unsorted array $A$ of length $n$ into two partitions $X$ and $Y$. We can find the inversions of the format $(X_i, Y_j)$ in $O(n)$ time. These can be referred to as cross-inversions or split-inversions, provided that they are sorted. How is this possible?

Say $X = [3, 4, 6]$ and $Y = [1, 2, 5]$. A mergesort-style algorithm will combine these two into $A$. We start by picking $1$ from $Y$, but that immediately tells us that it's smaller than every element in $X$. So we know there are $3$ inversions here {$(3, 1), (4, 2), (6, 2)$}. In fact, every time we pick an element from $Y$, we know it is smaller than every element remaining in $X$ {call this $x$}. So, every time we pick an element from $Y$, we add $x$ inversions to the total. If an element is picked from $X$, the natural order has been maintained. 

## Recurrence Relation
The subproblems are divided as:
-> Sort and count inversions to the left of the partition
-> Sort and count inversions to the right of the partition
-> Count the number of split inversions, add all three values, merge the array, and return that.

This gives us a Recurrence relation of

$$T(0, n) = 2T(n/2) + O(n)$$

Because this is a tiny modification of MergeSort, it comes to a complexity of $O(n.logn)$ as well

## Pseudo-Code

$$CountAndMerge(X, Y)$$

```
toret = []
for j, k in X, Y:
	if j <= k:
		append j to toret
		move head of X ahead
	else:
		append k to toret
		move head of Y ahead
		count += len(X, j onwards)
return (toret, count)
```

$$SortAndCountInv(A)$$
```
if len(A) == 1:
	return 0   <- base case

X = first half of A
Y = second half of A

(B, x) = SortAndCountInv (X)
(C, y) = SortAndCountInv (Y)
(D, z) = CountAndMerge(B, C)
return (D, x+y+z)
```
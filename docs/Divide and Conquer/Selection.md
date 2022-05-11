The Goal of this is to select the i'th smallest number in an *unsorted* array.

## Motivation
Calculating the $n'th$ place of winners in a race with unsorted arrays of time, or finding the median from disorganised data.

## Basic Solution
Pick a pivot element $p$. Partition the array around $p$. Push elements smaller than $p$ to its left and larger than $p$. Suppose the desired position is $i$, and the median ends up at $j$ after arranging the partitions.

If $i = j$ , then the $p$ is in fact, the desired element.
If $i > j$ , then $p$ must be to the left of the desired element. So, we will scan to the right of $p$.
If $i < j$, then $p$ must be to the right of the desired element. So, we will scan to the left of $p$.

In the ideal scenario, $p$ will be the median, allowing us to shorten our search group to half size with $c.n$ workcload. This will give us a recurrence relation of 
$$T(n) = c.n + T(n/2)$$which evaluates to $O(n)$. Great! Our job's done, now all we need to do is find the median... *uh-oh*.

## The Paradox
Finding the median in $O(n)$ time is something that we've taken for granted, and it is unfortunately a non-trivial algorithm. But it is possible! To do so though, we need an algorithm that uses a value other than the median for a pivot.

## The New Median Algorithm
There exists a median of "good enough" quality, which gives a 30-70 split in the worst-case scenario. If we use this pivot for partitioning, we can find the $n/2'th$ element (i.e. the median) in $O(n)$ time.

Step 1 -> Group $A$ into chunks of five. Conduct matches among these which end in $O(n)$ time roughly. 
Step 2 -> The winners of these matches, i.e. the individual medians, are taken to the next round.
Step 3 -> Find the *actual* median of *these* winners. This will give us the final pivot. Use this pivot to partition $A$, and calculate the _actual_ median with this pivot.

## Time Complexity
$$T(n) = c.n + T(n/5) + T(7n/10)$$
The rearrangement across partition element, and calculating the sub-medians takes $c.n$ time. $T(n/5)$ is taken to calculate the median of the sub-medians. A further $T(7n/10)$ is used to search for the desired element in the remaining array.

This evaluates to a final complexity of $O(n)$, which is derived purely by guessing.

## Why 70%?
![[Pasted image 20220303212940.png]]
This table taken from wikipedia shows that the MoM (median of medians) is well.. smack in the middle here. But consider the worst case scenario. It has to be larger than the 2nd and 1st element in at least half the sets, because it's larger than half the sub-medians. This means its larger than at least 30% of the sample space. For a similar reason, it must be smaller than at least 30% of the sample space.

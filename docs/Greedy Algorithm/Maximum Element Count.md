## Problem Definition
You are given $n$ tasks, with starting and finishing times $(s_i, f_i)$. The goal now is to find the maximum number of non-overlapping tasks that can be performed by one worker.

## Greedy Algorithm
Sort \[$t_i$] by Shortest Finishing Time First. Then pick the first element. Pick the next element if it doesn't overlap, or go to the one after if it does. Repeat this till you get to the last element.

## Proof via ???
TODO

## Time Complexity
This algorithm has a time complexity of $O(n \log n)$, which is the time taken to sort these $n$ tasks. The picking afterwards is done in $O(n)$ time.
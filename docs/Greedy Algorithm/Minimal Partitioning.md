## Problem Definition
You have been given $n$ tasks, \[$t_i$], just like last time. Each task has a starting time and a finishing time $(s_i, f_i)$. The goal is to find the minimum number of workers needed to perform these tasks without needing any amount of overlap.

## Motivation
A life-scale application is deciding the number of lecture halls needed to teach $n$ courses.

## Greedy Algorithm
Start by sorting the tasks by their starting times. After doing this, start with one worker. Give the first task to the first worker. If another task is started before the current one ends, assign it to another worker. Repeat this for all $n$ tasks.

## Proof via Lower Bound for the Optimal
Define the depth $d$ of $T$ as the maximum number of intervals active at any given time. The optimal number of workers needed must surely be equal to or more than the $d$. We will prove that the greedy algorithm will never use more than $d$ workers.

Say, when we got to a task $t$, there were $d$ active workers already. So, the algorithm gave $t$ to the $d+1th$ worker. This means that there are $d+1$ intervals overlapping with each other, so the depth must be $d+1$. This is a direct contradiction, and thus not possible. 

## Time Complexity
$O(n \log n)$ is the time complexity of sorting these $n$ tasks. The picking afterwards is done in $O(n^2)$ time, giving a total time complexity of $O(n^2)$.

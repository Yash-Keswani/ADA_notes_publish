## Problem Statement
Given two strings X = x1, x2, x3, · · · xm and Y = y1, y2, · · · yn, find a common subsequence (not necessarily contiguous) of X,Y that is of the longest possible length.
___
## Problem Definition
$X:= x_1, x_2, ... x_m$ ,  $Y := y_1, y_2, ... y_n$ 

___
## Recurrence Relation
Say we know the longest shared subsequence ending at some $x_i$ and $y_j$, not necessarily including those.

Say the last two letters are overlapping. In this scenario
$\quad\Omega_{i,\, j} = \Omega_{i-1, \, j-1} + 1$

Consider 
ABCDEFG
BCDEFGH
$\quad\Omega_{i,\,j} = \Omega_{i,\,j-1}$

if the two strings were interchanged, it would come as
$\quad\Omega_{i, j} = \Omega_{i-1,\,j}$

So, we can generalise this algorithm as 

$$
\Omega_{i,j} = max
	\begin {cases}
		\Omega_{i-1,\,j-1} + 1 & \text{}\\
		\Omega_{i-1,\,j} & \\
		\Omega_{i,\,j-1} & \\
	\end {cases}
$$

 

| -   | A   | B   | C   | F   | G   | H   | I   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| F   | 0   | 0   | 0   | 1   | 0   | 0   | 0   |
| G   | 0   | 0   | 0   | 0   | 2   | 0   | 0   |
| H   | 0   | 0   | 0   | 0   | 0   | 3   | 0   |
| I   | 0   | 0   | 0   | 0   | 0   | 0   | 4   |
| A   | 1   | 0   | 0   | 0   | 0   | 0   | 0   |
| B   | 0   | 2   | 0   | 0   | 0   | 0   | 0   |
| C   | 0   | 0   | 3   | 0   | 0   | 0   | 0   | 

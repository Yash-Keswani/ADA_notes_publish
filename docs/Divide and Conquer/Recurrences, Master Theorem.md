## Input Size
The input size describes the amount of space required to describe or set up the problem. It is proportional to the amount of bits needed to store the input. The input size is the only parameter that is needed to predict Time / Space Complexity for deterministic algorithms.

## Divide and Conquer
Divide and Conquer algorithms come in three steps

1) Divide the problem into smaller (typically disjoint) subproblems
2) Assume that you have already solved these subproblems below a certain layer
3) With this help from the recursion fairy, combine these solutions to get the solution of the current layer

## Recurrence
A recurrence describes the runtime of an input size of $n$ in terms of the same algorithm applied to smaller input sizes, and some additional overhead (the combine step).

Example: for Karatsuba multiplication

$$
\begin {align}
\quad &T(n) = 4T \left(\frac{n}{2} \right) + c_1 \cdot n \\
&T(1) = c
\end {align}
$$

$T(1)$ describes the base case of the algorithm

## Master Theorem
Define the recurrence as

$$
\quad T(n) = a \cdot T(n/b) + c\cdot n^d
$$

The master theorem gives a quick way to solve simple recurrences like this

$$
\quad T(n) = 
\begin {cases}
	O(n^d \log n)& a = b^d\\
	O(n^d)& a < b^d\\
	O(n^{\log_b a})& a > b^d\\
\end {cases}
$$

### Loose Proof
The number of levels in the recursion tree - $\log_b n$

The number of subproblems at level $j$ -  $a^j$

The subproblem size at level $j$ - $n/b^j$ 

Combine Phase at level $j$ : 

$$\quad a^j \cdot \left(\frac{n}{b^j}\right)^d \cdot c$$

So the total work is

$$\quad \sum_{j=0}^{\log_b(n)} n^d \cdot c \cdot \left(\frac{a}{b^d}\right)^j$$

This is a geometric progression. If $a=b^d$ , the sum evaluates to $O(n^d \log(n))$ 

If $a < b^d$, this can be totalled as an infinite sum.

$$\quad = n^d \cdot c \cdot \left(\frac{1}{1-\frac{a}{b^d}}\right) = O(n^d)$$

If $a>b^d$, we can't do the same because the ratio is > 1

$$\quad=n^d \cdot c \cdot \left(\left(\frac{a}{b^d}\right)^{\log_b n}-1\right) = O(n^{\log_ba})$$
## Problem Definition
#### Minimum Total Completion Time
We are given $n$ tasks with lengths \[$l_i$]. Our goal is to perform these tasks in an order such as to minimise the sum of finishing time for each task.

#### Minimum Weighted Completion Time
In this problem, each tasks also have a weight $w_i$. we have to miminise weighted completion time where weighted completion time $\overline{C_i} = w_i \cdot C_i$

## Greedy Algorithm
We sort the problems in order of $w_i\,/\,l_i$ . Then we perform the tasks in that order. Now why would that give the optimal solution?

## Proof via Exchange Argument
Say we arrange the tasks in the ideal order, which we are saying is also the hypothesised optimal order. Call this order as $\sigma = [t_1, t_2, ... t_n]$ 

Now suppose we create an order $\sigma^*$. This order is totally different from $\sigma$, but must have at least one inversion between adjacent elements. (Lemma: Having an inversion between non-adjacent elements will also create an inversion between some adjacent elements. Proof is (decently) trivial). Let's call these inverted adjacent elements as $t_q$ and $t_p$, 

$$\begin{align}
& \overline{C}(\sigma^*) = \left(\sum_{i\neq p,q} C_i \cdot w_i\right) + C^*_p \cdot w_p + C^*_q \cdot w_q \\

& \overline{C}(\sigma') = \left(\sum_{i\neq p,q} C_i \cdot w_i\right) + C'_p \cdot w_p + C'_q \cdot w_q \\\\

& \overline{C}(\sigma') - \overline{C}(\sigma^*) \\&=  
(C'_p - C^*_p)\cdot w_p + (C'_q - C^*_q)\cdot w_q \\&=
-l_q \cdot w_p + l_p \cdot w_q > 0 
\end{align}$$

By this, we can deduce that $\sigma'$ is a better arrangement. This means that no matter which arrangement we pick besides $\sigma$, a better arrangement exists. This means that $\sigma$ is the optimal arrangement. 

## Time Complexity
This algorithm has a time complexity of $O(n\log n)$, which is the time taken to sort these $n$ tasks.
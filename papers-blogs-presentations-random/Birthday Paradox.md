The birthday paradox is a collision problem:
Given a set of $N$ integers $\{0, 1, \ldots, N-1\}$, if you select $K$ elements uniformly from the set, what is the probability that at least 2 are equal? In the original problem, you need to find the min $K$ where the probability is above $50\%$.

Denote $\bar{P}$ as the probability of not having any collisions, then we have
$$\bar{P}=\prod_{i=1}^{k} 1-\frac{i-1}{n}=\prod_{i=1}^k\frac{n-i+1}{n}$$
Which is a very direct calculation: at step $i$, you are picking the $i$'th element and it must be different from the last $i-1$ elements, the chance of picking one of the last $i-1$ elements is $\frac{i-1}{n}$. Since we don't wan't to collide we grab the inverse event probability. Then the final probability is given by $P = 1-\bar{P}$.

[link](https://codeforces.com/contest/2070)
#### E
#### F
#revisit 
Couldn't finish the problem, here's the main points I think are probably important to solve it:
- we can do a OR convolution to get the number of ways $x|y$ is possible to be formed
- let $b$ be the mask of pizzas with odd size.
- if $(x|y)\&b > 0$, then some pairs could be invalid, in the case $x\&y\&b > 0$.
- if we can calculate the invalid pairs that form $x|y$, the problem becomes trivial
Some things I explored:
- $(x \oplus y) \& b = (x|y) \& b \iff x|y$ is valid 
- SOS dp may be involved -> having $x|y$ to calculate the invalid pairs then at bit $i$ if $b\&2^i > 0$ and $(x|y)\&2^i > 0$, then both x and y must have 1 active.
	- outline would be: fix (x|y) as msk
	- do $f(msk=(x|y), i=0) =$ count of subsets (elements) of msk
	- do $g(msk=(x|y), i=0, good = false)$ = count of pairs of elements that are subsets of msk where there is at least 1 bad bit active in both masks
	- Think I got close here, new thought process for next time:
		- fix a bit $b$ where $b$ is a odd pizza, that one will always be an active one in both mask pairs
		- now we have to solve $g(msk, i=0, forced)$ where the bad bit "forced" is 1 in both always, this leads to overcounting due to the subset nature of things
		- a clear way to think about this is having a subset $M$ of bits that will be 1 in both, which would make the solution $O(3^n)$.
		- maybe $g(msk, i=0, good)
		
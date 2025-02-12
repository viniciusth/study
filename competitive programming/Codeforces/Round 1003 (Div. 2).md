[LINK](https://codeforces.com/contest/2067)

### E
$$\forall i, min(a_1, \ldots, a_i) \geq mex(a_{i+1}, \ldots, a_n)$$
What shape does an array have for that to be true for all i?
$a_1 \geq 0$, which means that $mex(a_2, \ldots, a_n) = 0$ if $a_1=0$. Thus an array can't contain more than one 0. If the array contains no zeros, mex will always be 0 and youre good.
If $a_1 = 0$, then $min(a_1, \ldots, a_i) = 0$ which means $\forall i, i > 1, a_i \geq 1$
Looks optimal to choose the first 0 in the array and then all elements after it greater than 0.

Actually, since the amount of zeros can only be = 1, then just select all elements >0.
For each 0 that exists in the array you need to check if adding it doesnt break the rules.
-> invalid cases: 1, 1, 0; 1, 0, 1.
-> valid: 0, 1, 1.
-> for 2:
-> valid: 1, 2, 0, 2;
-> its valid for $x$ iff $j=min\{i, a_i = x\}, mex(a_j + 1, \ldots, a_n) \leq x$ 
-> heuristic: check only first 0 (argue about this)
-> AC!
for the heuristic, it makes sense because we are comparing for each $x$ if suffix mex after its first appearance is $\leq x$, thus if we choose a 0 that is AFTER the first 0 and it works, we can also pick the first 0, so it becomes a TTTTFFFF case.
### F
### G

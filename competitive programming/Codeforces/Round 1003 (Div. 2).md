[LINK](https://codeforces.com/contest/2067)

### E
#mex #adhoc
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

-> read the tutorial for this one, I could've just checked if the condition holds for the array with the first zero instead of creating a new condition to check lol
### F
Answer will be $3f(0)$ where $f(0)$ computes the answer by starting to put values into $P$ and handling putting other values in either $Q$ or $R$.

Observations:
- lets say we're at the state X 0 0 after $i - 1$ operations, we can only apply to $Q$ or $R$ if $a_i = X$. if we use it on $Q$ for example we'll have X X 0. We have two options: move to X X X or X X Y
- X X X is equivalent to 0 0 0.
- X X 0 is equivalent to X 0 0 (when the next element != X, which is the only case in which this matters)
- $prefix\_xor = P \oplus Q \oplus R$
if at element i, you know $P \oplus Q \oplus R$
```
def f(i, xor):
	
```

### G

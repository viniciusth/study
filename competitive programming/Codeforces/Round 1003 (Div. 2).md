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
#xor #dp
Answer will be $3f(0)$ where $f(0)$ computes the answer by starting to put values into $P$ and handling putting other values in either $Q$ or $R$.

Observations:
- lets say we're at the state X 0 0 after $i - 1$ operations, we can only apply to $Q$ or $R$ if $a_i = X$. if we use it on $Q$ for example we'll have X X 0. We have two options: move to X X X or X X Y
- X X X is equivalent to 0 0 0.

- - -
need some hints:
if at element i, you know $P \oplus Q \oplus R = prefix\_xor_i$ and the state must be a permutation of $(prefix\_xor_i, x, x)$ for some x.
- - - 

Here's a python recursive implementation that solves the problem:
```python
def f(i, xor):
    if i == n:
        return 1
    ans = 0
    mult = 3 if p[i-1] == xor else 1
    ans += f(i+1, xor) * mult
    if (a[i] ^ xor) == p[i-1]:
        ans += 2*f(i+1, p[i-1])
    return ans
```
$p[i]$ is the prefix xor. transitions:
- move forward maintaining the value x as the same, if $p[i-1] = xor$ this means that we have (x, x, x) and we can select any of the 3 to continue.
- if $a[i] \oplus x = p[i-1]$ then we can "swap" the x to the current prefix in two ways, next step becomes $(p[i-1], p[i-1], x) = (p[i-1], p[i-1], p[i])$
How to optimize? second index potentially has N values.

For the second transition to happen, we must have $p[i-1] \oplus a[i] = x \iff p[i] = x$, which means the x can only change in select positions. Still looks like it can have N/3 different values.

bottom up dp:
```
dp[i][x] = ways to place i+1 elements, with 2 equal to x.
dp[0][0] = 1
S = {0}
for i in 1..n:
	for x in S:
		// we are placing the ith element into the solution, 
		// current state is (x, x, p[i-1] ?? 0)
		if p[i-1] == x { // we can apply to all 3
			dp[i][x] += dp[i-1][x]*3
		} else dp[i][x] += dp[i-1][x]
		if (a[i] ^ x) == p[i-1] { // we can make (x, p[i-1], p[i-1])
			dp[i][p[i-1]] += dp[i-1][x] * 2
		}
```
we only increase 2 dp values at every i: $x = p[i-1], x = p[i]$, so we can optimize it with a map
### G
#todo

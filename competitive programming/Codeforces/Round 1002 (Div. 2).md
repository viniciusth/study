[LINK](https://codeforces.com/contest/2059)
### C
#adhoc #mex #2d 
Initially, didn't realize you could only use one 0 per column, so over complicated the problem. To get the maximal mex you can reorder the rows to make the one with element 0 at the row 1 and so on:
$$\begin{matrix}
a_{1,1} & a_{1,2} & a_{1,3} & \ldots & a_{1,n-1}  & 0 \\
a_{2,1} & a_{2,2} & a_{2,3} & \ldots & 0          & a_{2, n} \\
a_{3,1} & a_{3,2} & \ldots  & 0      & a_{3, n-1} & a_{3, n} \\ 
\vdots  & \vdots  & \vdots  & \vdots & \vdots     & \vdots\\ 
0       & a_{n,2} & a_{n,3} & \ldots & a_{n,n-1}  & a_{n, n}
\end{matrix}$$
Thus, for row 2 to have $mex = 1$ we need $a_{2,n}=1$, for row 3 we need $a_{3,n-1} + a_{3,n} = 2 \iff a_{3, n-1} = 1 \land a_{3, n} = 1$, and in general for row $i$ we need that the suffix of size $i-1$ contains only 1's.
With this observation we can simply count the size of suffix 1's of each row, put them in a set and grab the one with the smallest amount with value >= than the current mex and pop it, continue until you cant find any more.
### D
#dijkstra #upsolve
Didn't read during contest (mistake), looks pretty easy, for each pair (u, v) that is contained in both graphs we need to reach either u or v in the lowest cost possible, just run dijkstra $dist[u1][u2]$ and simulate the moves, super easy since $O(n^2\log{n})$ is allowed.
## E
#upsolve #revisit
Thinking about the operation in 1D seems to give a pretty interesting transformation:
1st sample: 2 6 3 4, operation (1, 1) makes 1 2 6 3, basically you choose a starting point $i \cdot m, 0 \leq i < n$ to insert an element, and then pop the last element of the 1D array.
#### first try
Now the problem becomes: given 2 1D arrays, whats the smallest number of moves to make them equal?
1st sample again:
2 6 3 4
1 2 7 8
maybe going by prefix works, as there is nothing you can do but place an element there if you don't have the correct values. When inserting a value you can treat it as wildcard that can be anything so we would have
 ? 2 6 3
 1 2 7 8
 the first m values match, so now we can move to the second m-sized array
 ? 2 ? 6
 1 2 7 8
 ? 2 ? ?
 1 2 7 8
 answer is 3
Looks correct, how to implement fast? $n, m \leq 3 \cdot 10^5$. feels like string matching.
we need to maintain offsets correctly so we know which part of the array we need to match with the j-th m-sized array 
2 6
1 2 -> compares [0, 1] with [0, 1], no match which means we need a new wildcard. increases offset by 1 and skips the first element of this m-sized array
-
? 2
1 2 -> compares [0, 0] with [1, 1], match all good
-
6 3 -> this is offset by 1 to the left
7 8 -> compares [1, 2] with [0, 1], no match.
#### second try
This is not enough, a wildcard from row j may be pushed forward by row i (i < j) if we do the operation for j first, which may be optimal.
Lets try doing some analysis:
how may a cell (i, j) be marked as a wildcard?
1. we fill some prefix of size $|P| \geq 1$ and the sum of wildcards from rows \[1, i) is equal to $j - |P|$
2. $|P| = j$
3. $|P| = 0$ and the wildcard comes from row i-1.
hmm, not sure if that helps, I wonder what types of arrays can be formed.
problem is binary searchable, if you do $k$ operations you always throw away the last k elements of the array, but then where can you place the k wildcards?
#### third try
There definitely is some greedy aspect since the array needs to match fully.
For E1 a guess would be just doing a LCS since everything is distinct and just printing $N - x$, this assumes that if you have a sequence of numbers you want to keep, you can always keep it and the other elements can be "set" to wildcards which I don't think is true. 

What do you get from matching positions? $A(i, j)$ -> $B(i', j')$, if you want to keep the element $A(i, j)$ then you must move it to that position, which may not be possible
- If $(i', j') < (i, j) \lor \nexists (i', j')$ -> impossible, must remove $(i, j)$.
- If $(i, j) < (i', j')$, the element must move by $(i'-i)m - j + j'$. 

too stuck, read hint 1:
`To minimize the number of operations, it is necessary to leave as many elements as possible in the original array. What are these elements?`
These elements should be the ones that have a match, so we know the lower bound of the operations. 

This is something I've come up with already, so lets go hint 2:
`These elements must form the initial array prefix and the final array subsequence.`
True, because if you do $k$ operations, the last $k$ elements will be removed and you will be left with $nm-k$ elements. Maybe just doing the prefix subsequence will give us the answer amount? I'm not convinced you can place wildcards anywhere.
Yeah it fails on the second sample:
```
5 4 1 2 3
5 4 3 2 1
```
we need to include a way to identify if we can put an element where it belongs, which is where I was stuck, so moving on to hint 3:
`What other condition needs to be imposed on the prefix so that additions can be used to obtain the final array?` 
That's what I've been trying to find out for quite a while now... not a super helpful hint, but it shows I'm in the right path, this hint show that there is 1 condition that is enough. AGHH I'm done with this one, lets go first line of solution that is new:
`Claim: For a sequence of actions to exist that leads to the final array, it is necessary and sufficient that for each such element, if it was in its array at position i (in the original array of arrays), there must be at least m−i elements in the final array that do not belong to the current prefix before it.`
not sure I understand fully, go gym and hopefully when I'm back I'll understand
-
still dont understand, editorial is quite confusing, tho there is one solution in the comments that is super simple:
```rust
let mut i = 0;
for j in 0..(n*m) {
	if a[i] == b[j] {
		i+=1;
	}
	else if i/m == j/m {
		i -= i % m;
	}
}
```
Basically, you go trying to match elements 1 by 1, but if they don't match AND you have matched all elements up to the same row, then you need to go back to the beginning of the row.

also dont know why it works...
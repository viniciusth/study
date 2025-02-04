- [x] C 
- [x] D 
- [ ] E 

[LINK](https://codeforces.com/contest/2059)
### C
#adhoc #mex #2d #overcomplicate
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
#dijkstra #noread
Didn't read during contest (mistake), looks pretty easy, for each pair (u, v) that is contained in both graphs we need to reach either u or v in the lowest cost possible, just run dijkstra $dist[u1][u2]$ and simulate the moves, super easy since $O(n^2\log{n})$ is allowed.
## E
#noread
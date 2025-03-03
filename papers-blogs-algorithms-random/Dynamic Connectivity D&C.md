#### Problem statement
You receive $Q$ queries for a undirected graph $G$, each query be in the following format:
- $1$ $u$ $v$: $u, v \in G$: add the edge $(u, v)$, if it already exists delete it.
- $2$ $u$ $v$: check if $u$ and $v$ belong to the same connected component.

#### D&C approach
Let's use DSU to maintain the connected component aspect of the problem, and define $[l, r]$ as the range that the recursive algorithm is currently looking at.

The core of the solution is realizing that each added edge has at most 1 associated event for deleting it, which means that each added edge will exist from $[i, rmv[i])$. 
Our D&C will maintain the state such that when we reach the state $[l , l]$, we'll have all edges with ranges that cover $l$ present in the DSU.

Clearly, our initial state will be $[1, n]$ with all edge ranges as candidates for activating.
Each candidate has 3 possibilities:
- edge range fully covers our subproblem -> activate the edge, filter out this candidate
- edge range is fully outside of our subproblem -> filter out this candidate
- if not one of the above, then it covers part of our subproblem, keep it as a candidate.
- after solving subproblems, rollback all dsu operations made in this level.
By following this, we will have applied all relevant edges for all queries when we reach a leaf node. The algorithm outline is:
```
def f(l, r, Q):
	if l == r:
		ans[l] = dsu.same(queries[l].0, queries[l].1)
		return;

	newQ = []
	count = 0
	for q in Q:
		if queries[q] covers (l, r):
			dsu.add(queries[q].0, queries[q].1)
			count += 1
		else if queries[q] intersects with (l, r):
			newQ.push(q)

	f(l, mid, newQ)
	f(mid+1, r, newQ)
	dsu.rollback(count)
```

#### Complexity analysis
For complexity analysis, it's clear that our recursion follows $T(q) = 2T(\frac{q}{2}) + O(|Q| \space log \space n)$, which will reduce to $T(q) = O(q \space log \space n \space log \space q)$.

A common way to prove these kinds of complexities is looking at the maximum size of $|Q|$ at each level of the tree which has height $log \space n$.

Let's start by setting our initial $|Q|$ = 1, which means we only have one edge range $(l, r)$.

You can imagine this very easily as a segment tree query, when we reach a node that fully covers it we apply the edge, fully outside we skip the edge and otherwise we move the edge to the two children.
An important result of proving the complexity of segment tree query is that each level of the tree will have at most 2 vertices visited by doing these operations. Thus for $|Q| = 1$ we have $O(log \space n)$ vertices visited by the query and at most nodes visited at each level.
Extending for any $Q$, we have that each level will have at most $2|Q|$ query values, which gives us a total of $2|Q| \space log \space |Q|$ total size of the arrays built by the recursion.
##### Proof Outline
Observe that if the statement is true, then we can only split the query $[L, R]$ into two paths only once, so our goal is to prove that after splitting the path we never split it again.

Let's assume we already split once, and we are on the left path of the recursion.
Now, if we were to split into two paths again, the right path would definitely be fully contained by $[L, R]$, since the first upper split to the right will cover some $[X, R]$ part of the query, and this current left split will cover some $[L, X']$ part, so our right split will cover $(X', X) \in [L, R]$. Same logic for the first right split.
This means that there will be no more steps in the recursion from there, since there are $O(log \space n)$ recursion steps, there will be at most $1$ extra step at each step to cover these fully internal ranges, and thus we maintain a $O(log \space n)$ amount of visited vertices for a arbitrary query $[L, R]$ on a segment tree.

Since our D&C recursion mimics a segment tree, we will have the same complexity $O(log \space n)$ for each query we carry through, and $O(q \space log \space n)$ for doing all queries simultaneously. Since we also operate on DSU with $O(log \space q)$ for merge + rollback, the total complexity becomes $O(q \space log \space q \space log \space n)$.

Note: this approach works to support offline removal for any structure that implement addition and rollback.
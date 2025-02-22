A data structure for maintaining a set of data, with proof of its validity.
Let $\mathcal{H}$ be a hashing function, then for a set of $n$ elements we will build a binary search tree for these values where the leaf values will be $\mathcal{H}(a_i)$.
Each inner node will hash the hashed values of both its children $T_i = \mathcal{H}(T_{2i} || T_{2i+1})$.
When querying for a value, return the value and all $log_2(n)$ siblings of the path, so the client can rebuild all hashes and make sure that no data was manipulated.
The client must store the root hash.

![[Excalidraw/Merkle tree example|center]]
Example of a merkle tree for maintaining a set of 4 values, when querying for $a_2$ the values circled in red are returned.
The client can then compute:
- $X_1=\mathcal{H}(a_2) = T_5$
- $X_2 = \mathcal{H}(T_4||X_1) = T_2$
- $X_3 = \mathcal{H}(X_2||T_3)=T_1$
- $a_2$ is valid $\iff X_3 = T_1$.

#flashcards/cryptography
What data needs to be stored by client & server when using a merkle tree?::Clients need to maintain the hash of the root of the tree, the server maintains the entire tree.

What values must be returned by a server so a client can verify the validity of the received data? i.e. what is a merkle proof?::The request data plus all neighbor values in the tree, so the user can rebuild the root hash based on it.
# Definition

- A _walk_ in a [[Graph | graph]] is any sequence of nodes such that every consecutive pair of nodes in the sequence is connected by an edge.
	-	In other words it is any route that runs from node to node along the edges. 
	-	Walks can be defined for both [[Graph#directed graph | directed]] and [[Graph#undirected graph | undirected]] graph.
		-	In a directed graph, each edge traversed by a walk must be traversed in the direction of that edge.
		-	In an undirected graph edges can be traversed in either direction.
			
![[Pasted image 20210413194752.png]]

In general a walk can intersect itself, revisiting a node it has visited before or running along an edge or set of edges more than once.
Walks that do not intersect themselves are called _paths_ or _self-avoiding walks_, and are important in many areas of network theory.

The _length_ of a walk in a network is the number of edges traversed along the walk (not the number of nodes).
- A given edge can be traversed more than once, and if so it is counted separately each time it is traversed.
- In layman’s terms the length of a walk is the number of “hops” the walk makes from node to adjacent node.

# Calculate Number of Walks and Paths
It is straightforward to calculate the number of walks of a given length _r_ on a [[Graph | graph]]. 

Generalizing to walks of arbitrary length $r$, it is straightforward to see that[^1]

$$N^{(r)}_{ij}=[A^r]_{ij}$$

A special case of this result is that the number of walks of length $r$ that start and end at the same node $i$ is $[A^r]_{ii}$. 
These walks are just loops in the network and the total number $L_r$ of loops of length $r$ in the graph is the sum of this quantity over all possible starting points $i$:

$$L_r=\sum_{i=1}^{N}[A^r]_{ii}=Tr A^r$$

**Note that this expression counts separately loops consisting of the same nodes in the same order but with different starting points.** 
Thus the loop 1→2→3→1 is considered different from the loop 2→3→1→2. The expression also counts separately loops that consist of the same nodes but traversed in opposite directions, so that 1→2→3→1 and 1→3→2→1 are distinct.[^2]


# References
Newman, M. E. J. (2018). 6.11 Walks and paths. In _Networks_ (2nd ed., pp. 131 - 132). essay, Oxford University Press.

# Notes
[^1]: For a more rigorous proof we can use induction. If there are $N^{(r−1)}_{ik} walks of length $r−1$ from $k$ to $i$, then by arguments similar to those above there are $N_{i j}^{(r)}=\sum_{k} N_{i k}^{(r-1)} A_{k j}$ walks of length $r$ from $j$ to $i$, or in matrix notation $\mathbf{N}^{(r)}=\mathbf{N}^{(r-1)} \mathbf{A}$, where $N^{(r)}$ is the matrix with elements $N^{(r)}_{ij}$. This implies that if $\mathbf{N}^{(r-1)}=\mathbf{A}^{r-1}$ then $N^{(r)}=A^r$. Starting from the base case $N^{(1)}=A$ we then have $N^{(r)}=A^r$ for all $r$ by induction, and taking the $ij$th element of both sides gives the equation
[^2]: If we wish to count each loop only once, we should roughly speaking divide by _r_, but this does not allow for walks that have symmetries under a change of starting points, such as walks that consist of the same subloop traversed repeatedly. Counting such symmetric walks properly is a complex problem that can be solved exactly in only a few cases.
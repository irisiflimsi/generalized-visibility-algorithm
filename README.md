# Motivation

Some games consider visibility not just from a point source, which is the usual for the _visibility problem_ but from an area. Particularly games, which only allow grid positions, checking visibility from only one point - say the center - leads to artifacts.  But we can make some assumptions that may prove to be valuable, because of the "gamey" nature of the problem.

# Formulation

Let $({c^E\_i})\_{i=0..n}$ be the vertices of a convex polygon $C$, the _center_. Let $({p^E\_i})\_{i=0..m}$ be the vertices of a linear graph $P$ of _obstacles_ in the plane. The individual obstacles are usually identified by the irreducible subgraphs of this graph. We also identify the graph with its "embedding" in the plane; all edges are straight lines. Find the boundary of the visibility region $V(C)$, i.e. the set $\bigcup\lbrace(c, x):\[c,x\]\cap P=\emptyset, c\in C, x\in\mathbb{R}^2\rbrace$.

We make a further assumption that the $V(C)$ is bounded, i.e. the boundary will be a polygon. We also assume that the obstacles contain their intersections as points, i.e. any pairwise intersections of edges from $P$ is contained in the vertex set of $P$.

We also assume that $C\cap P=\emptyset$, i.e. $C$ does not intersect any obstacles.

# Algorithm

We will unite all triangles we find in the following manner. Start with any point on the (boundary of the) center, called $c_0$ that intersects the obstacles at obstacle point $p_0$, where $p_0$ is closest to $c_0$. $q_0=p_0$. The line $(c_0,p_0)$ shall not intersect $C$.

$i$ will be the step counter and $c_i$ will always denote (boundary) center points and $p_i$ will be an obstacle point. $c_i$ does not need to be a $c^E\_j$, nor does $p_i$ need to be an $p^E_j$. $V(C)$ starts empty.

Generally speaking, we will rotate clockwise around obstacle points until we are blocked by an obstacle or the "end" of $C$. We will rotate counter-clockwise from such blocks or "end" until we hit a block or the other "end". We are then in the position of the outset, but we have moved overall to the left, i.e. counter-clockwise. We will have scanned the visible opening completely.

More formally, we start out in one of the positions (A)-(M). The images show abstract positions, where only the relation with respect to the grey line $\[c_i, q_i\]$ is important, not any concrete angles, but all depicted lines are actually (straight) lines. Also observe that in all situations, $p_i, p_{i+1}, q_i$ and $q_{i+1}$ may actually coincide.


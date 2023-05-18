# Motivation

Some games consider visibility not just from a point source, which is the usual for the _visibility problem_ but from an area. Particularly games, which only allow grid positions, checking visibility from only one point - say the center - leads to artifacts.  But we can make some assumptions that may prove to be valuable, because of the "gamey" nature of the problem.

# Formulation

Let $({c^E\_i})\_{i=0..n}$ be the vertices of a convex polygon $C$, the _center_. Let $({p^E\_i})\_{i=0..m}$ be the vertices of a linear graph $P$ of _obstacles_ in the plane. The individual obstacles are usually identified by the irreducible subgraphs of this graph. We also identify the graph with its "embedding" in the plane; all edges are straight lines. Find the boundary of the visibility region $V(C)$, i.e. the set $\bigcup\lbrace(c, x):\[c,x\]\cap P=\emptyset, c\in C, x\in\mathbb{R}^2\rbrace$.

We make a further assumption that the $V(C)$ is bounded, i.e. the boundary will be a polygon. We also assume that the obstacles contain their intersections as points, i.e. any pairwise intersections of edges from $P$ is contained in the vertex set of $P$.

We also assume that $C\cap P=\emptyset$, i.e. $C$ does not intersect any obstacles.

# Algorithm

We will unite all triangles we find in the following manner. Start with any vertex on the (boundary of the) center, called $c_0$ that intersects the obstacles at obstacle point $p_0$, where $p_0$ is closest to $c_0$. $q_0=p_0$. The line $(c_0,p_0)$ shall not intersect $C$.

$i$ will be the step counter and $c_i$ will always denote (boundary) center points and $p_i$ will be an obstacle point. $c_i$ does not need to be a $c^E\_j$, nor does $p_i$ need to be an $p^E_j$. $V(C)$ starts empty.

Generally speaking, we will rotate clockwise around obstacle points until we are blocked by an obstacle or the "end" of $C$. We will rotate counter-clockwise from such blocks or "end" until we hit a block or the other "end". We are then in the position of the outset, but we have moved overall to the left, i.e. counter-clockwise. We will have scanned the visible opening completely.

More formally, we start out in one of the positions listed in the following Completeness section. The images show abstract positions, where only the relation with respect to the grey line $\[c_i, q_i\]$ is important, not any concrete angles, but all depicted lines are actually (straight) lines. We add the trinagles that are bounded by the solid and dotted grey lines. Note that in a few rare cases, nothing is added, because we do not add triangles with area $0$. Any rotation stops in one of the positions and stops at the dotted line, when the (extended) line hits either a $c^E_j$ or a $p^E_j$. If a point indexed $i+1$ is not shown, this means, it coincides with that (of the same type) from step $i$. Otherwise, we do not allow $p_i, p_{i+1}, q_i$ and $q_{i+1}$ to coincide, we consider those separate positions. We alsways depict the closest points on the dotted line to the rotation point, not the point we actually stopped the rotation at.

One final note on the terms _right_ and _left_. They are meant regarding the direction of the rotation taking place. If speaking of the potential rotation point itself, the other potential rotation point is intended, i.e. only $c_i$ and $p_i$. In case of points in $(c_i,p_i)$, the points right regarding $p_i$ are left regarding $c_i$ and vice versa.

We need to prove that the position listing is complete, the algorithm terminates, and that the union of all triangles is the entirety of $V(C)$.

## Completeness

(A)-(E) describe all situations, where all obstacles ending at $p_i$ are to the right of our current axis and we are not at an outer right vertex $c_i$ as viewed from $p_i$. (F)-(H), (N), and (O) describe all situations, where some obstacles ending at $p_i$ are to the left of our current axis and we are not at an outer left vertex $c_i$ as viewed from $p_i$. (K)-(M) describe all situations, where we are at an outer right vertex $c_i$ as viewed from $p_i$. (I), (J), and (M) describe all situations, where we are at an outer left vertex $c_i$ as viewed from $p_i$.

### A
All obstacles at $p_i$ are to the right of our current axis and we are not at an outer right vertex $c_i$ as viewed from $p_i$. Rotating $CW$, we first encounter a closest outer right vertex from $C$.

### B
All obstacles at $p_i$ are to the right of our current axis and we are not at an outer right vertex $c_i$ as viewed from $p_i$. Rotating $CW$, we first encounter an obstacle from $P$ connected to $q_i$. Note that $q_{i+1}$ will not coincide with $p_i$, because we would have been in position (?) before.

### E
All obstacles at $p_i$ are to the right of our current axis and we are not at an outer right vertex $c_i$ as viewed from $p_i$. Rotating $CW$, we first encounter an obstacle from $P$ not connected to $q_i$. This obstacle point lies strictly between $p_i$ and $c_i$. $q_{i+1}$ will have all obstacle edges to the right of our new axis or on our new axis, because if there was one to the left, there are other points on that obstacle edge that would have been discovered first. (Note the various intersection conditions we have in pace for $P$ and $C$.)

### C
All obstacles at $p_i$ are to the right of our current axis and we are not at an outer right vertex $c_i$ as viewed from $p_i$. Rotating $CW$, we first encounter an obstacle from $P$ not connected to $q_i$. This obstacle point $q$ lies strictly between $p_i$ and any point connected to $q_i$ but there are obstacle points connected to $q_i$ on the ray extending $(p_i, q)$. (Note that $q_{i+1}$ will never coincide with $p_i$, because we would have been in position (?) before.) $q_{i+1}$ will have all obstacle edges to the right of our new axis, because if there was one to the left, there are other points on that obstacle edge that would have been discovered first. (Note the various intersection conditions we have in place for $P$ and $C$.)

### D
All obstacles at $p_i$ are to the right of our current axis and we are not at an outer right vertex $c_i$ as viewed from $p_i$. Rotating $CW$, we first encounter an obstacle from $P$ not connected to $q_i$. This obstacle point $q$ lies strictly beyond $p_i$ and there are no points connected to $q_i$ on the ray extending $(p_i, q)$. (Note that $q_{i+1}$ will never coincide with $p_i$, because we would have been in position (?) before.) We have not encountered a point between $p_i$ and $q$ but due to the boundedness of $V(C)$, we have encountered a line (sub)segment which bounds our triangle.

### F
All obstacles at $p_i$ are to the left of our current axis and we are not at an outer left vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we first encounter a closest outer left vertex from $C$.

### G
All obstacles at $p_i$ are to the left of our current axis and we are not at an outer left vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we first encounter an obstacle from $P$ connected to $q_i$. Note that $q_{i+1}$ will not coincide with $p_i$, because we would have been in position (?) before.

### H
All obstacles at $p_i$ are to the left of our current axis and we are not at an outer left vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we first encounter an obstacle from $P$ not connected to $q_i$. This obstacle point lies strictly between $p_i$ and $c_i$. $q_{i+1}$ will have all obstacle edges to the left of our new axis or on our new axis, because if there was one to the right, there are other points on that obstacle edge that would have been discovered first. (Note the various intersection conditions we have in pace for $P$ and $C$.)

### N
All obstacles at $p_i$ are to the left of our current axis and we are not at an outer left vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we first encounter an obstacle from $P$ not connected to $q_i$. This obstacle point $q$ lies strictly between $p_i$ and any point connected to $q_i$ but there are obstacle points connected to $q_i$ on the ray extending $(p_i, q)$. (Note that $q_{i+1}$ will never coincide with $p_i$, because we would have been in position (?) before.) $q_{i+1}$ will have all obstacle edges to the left of our new axis, because if there was one to the right, there are other points on that obstacle edge that would have been discovered first. (Note the various intersection conditions we have in place for $P$ and $C$.)

### O
All obstacles at $p_i$ are to the left of our current axis and we are not at an outer left vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we first encounter an obstacle from $P$ not connected to $q_i$. This obstacle point $q$ lies strictly beyond $p_i$ and there are no points connected to $q_i$ on the ray extending $(p_i, q)$. (Note that $q_{i+1}$ will never coincide with $p_i$, because we would have been in position (?) before.) We have not encountered a point between $p_i$ and $q$ but due to the boundedness of $V(C)$, we have encountered a line (sub)segment which bounds our triangle.

### K
All obstacles at $p_i$ are to the right of our current axis and we are at an outer right vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we cannot encounter an obstacle from $P$ connected to $p_i$. We thus may encounter $p_{i+1}$, which is connected to some $q$ on the ray $(c_i,q_i)$.

### L
All obstacles at $p_i$ are to the right of our current axis and we are at an outer right vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we cannot encounter an obstacle from $P$ connected to $p_i$. We thus may encounter $p_{i+1}$, which is not connected to some $q$ on the ray $(c_i,q_i)$. (Some line (sub)segment must be encountered, though.) $p_{i+1}$ will have all obstacle edges to the left of our new axis, because if there was one to the right, there are other points on that obstacle edge that would have been discovered first. (Note the various intersection conditions we have in place for $P$ and $C$.)

### M
All obstacles at $p_i$ are to the right of our current axis and we are at an outer right vertex $c_i$ as viewed from $p_i$. Or all obstacles at $p_i$ are to the left of our current axis and we are at an outer left vertex $c_i$. Rotating $CCW$, we first encounter a vertex from $C$.

### I
All obstacles at $p_i$ are to the left of our current axis and we are at an outer left vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, we may encounter an obstacle from $P$ connected to $p_i$: $p_{i+1}$.

### J
All obstacles at $p_i$ are to the left of our current axis and we are at an outer left vertex $c_i$ as viewed from $p_i$. Rotating $CCW$, the first obstacle $p_{i+1}$ encountered need not be connected to $p_i$. But we must encounter some line (sub)segment.

## Termination

Starting at $c^E_0$ we look at the sum of the angles $(c^E_{k+1},c^E_k,p_i)$ and $(c^E_k,c^E_{k+1},p_i)$, where the vertices on $C$ are ordered $CCW$-wise and $c_i\in\[c^E_k,c^E_{k+1}\]$. Notice that this sum always decreases and both angles are non-negative. The former angle can become $0$, but then we immediately move to a next segment of the $C$-boundary. But any rotation that leaves the former angle positive, also leaves the latter positive, which means which means we always move to the next segment before we reach a negative angle.

## Entirety

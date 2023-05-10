# Motivation

Some games consider visibility not just from a point source, which is the usual for the _visibility problem_ but from an area. Particularly games, which only allow grid positions, checking visibility from only one point - say the center - leads to artifacts.  But we can make some assumptions that may prove to be valuable, because of the "gamey" nature of the problem.

# Formulation

Let $({c^E\_i})\_{i=0..n}$ be a convex polygon $C$, the _center_. Let $({l\_i})\_{i=0..m}$ be a list of line segments called _obstacles_, where $l\_i=\[p^0\_i, p^1\_i\]$ for $i=0..m$. (This notation identifies the whole line segment, not just the end points.) Find the boundary of the visibility region $V(C)$, i.e. the set $\bigcup\lbrace(c\_i, x):\[c_i,x\]\cap({l\_j})\_{j=0..m}=\emptyset, i=0..n, x\in\mathbb{R}^2\rbrace$.

We make a further assumption that the $V(C)$ is bounded, i.e. the boundary will be a polygon. We also assume that the obstacles contain their intersections as points, i.e. we do not need to find these first: $l\_i\cap l\_j\subset\bigcup\lbrace(p^0_k,p^1_k : k=0..m)\rbrace$ for $i,j=0..m, i\neq j$.

We also assume that $C$ (as area) does not intersect any obstacles.

# Algorithm

We will unite all triangles we find in the following manner. Start with a point on the (boundary of the) center, called $c_0$ with smallest angle $0$ that intersects the obstacles at obstacle point $p_0$, where $p_0$ is closest to $c_0$.

$i$ will be the step counter and $c_i$ will always denote (boundary) center points and $p_i$ will be an obstacle point. $c_i$ does not need to be a $c^E\_j$, nor does $p_i$ need to be an $p^k_j$. $V(C)$ starts empty.

Generally speaking, we will rotate clockwise ($-$) around obstacle points until we are blocked by an obstacle or the "end" of $C$. We will then routate counter-clockwise ($+$) from that block or "end" until we hit a block or the other "end". We are then in the position of the outset, but we have moved overall to the left, i.e. counter-clockwise. We will have scanned the visible opening completely.

More formally, assume we are at $c_i$ and $p_i$. $p_i$ is the closest obstacle point along the ray $\[c_i, p_i\]$. Assume all $p_k$ and $c^E_k$ points are ordered according to a rotation around $p_i$ starting with the axis through $c_i$. This is asymmetrical ordering, i.e. only angles in $\[0,\pi)$ are considered. We can also ignore all $p_k$, where $(p_k,$p_i\]\cap C\ne\emptyset$ and all $c_k$ where $(c_k,$p_i\]\cap C\ne\emptyset$ . We call this the $p_i$-ordering. We do the same with rotations around $c_i$, which we call the $c_i$-ordering. When at this position, we distinguish the following cases:

### $p_i$ is a line segment endpoint $p^0_k$ or $p^1_k$ and all other endpoints of such lines have maximum angle less than 0 in $c_i$-ordering. There is a $c^E_k$ with negative angle in $p_i$ ordering.

Call the maximum angle $\alpha$. We ($-$)-rotate around $p_i$, until we hit an obstacle vertex $p_k$ or a center vertex $c^E_k$, whichever we encounter first. We will have rotated at most $\alpha$. If we reached an obstacle vertex, we take the closest center point $c_{i+1}$ that lies on the line through $(p_i,p_k)$, otherwise we take $c_{i+1}=c^E_k$, which we encountered directly. We add the triangle $\[c_{i+1}, c_i, p_i\]$ to $V(C)$. It is easy to see that no obstacles can be in it.

We take the point $q_i$, which is the closest obstacle along $(c_i,p_i)$ with a positive angle. This point need not be a $c^E$. We also take the point $q_{i+1}$, which is the closest obstacle along $(c_{i+1},p_i)$ with a negative angle. Note that $q_i$ and $q_{i+1}$ must be on the same line segment, because we have not encountered any other segment end during rotation. We then add $\[p_i,q_i,q_{i+1}\]$.

We already know $c_{i+1}$. As $p_{i+1}$ take the closest obstacle point to $c_{i+1}$ along the ray $(c_{i+1}, p_k)$.

### $p_i$ is a line segment endpoint $p^0_k$ or $p^1_k$ and all other endpoints of such lines have maximum angle less than 0 in $c_i$-ordering. There is no $c^E_k$ with negative angle in $p_i$ ordering.

### $p_i$ is a line segment endpoint $p^0_k$ or $p^1_k$ and the maximum angle of all other endpoints of such lines is 0 in $c_i$-ordering

### $p_i$ is a line segment endpoint $p^0_k$ or $p^1_k$ and at least one other endpoint has positive angle in $c_i$-ordering

### $p_i$ is not a line segment endpoint $p^0_k$ or $p^1_k$


# Motivation

Some games consider visibility not just from a point source, which is the usual for the _visibility problem_ but from an area. Particularly games, which only allow grid positions, checking visibility from only one point - say the center - leads to artifacts.  But we can make some assumptions that may prove to be valuable, because of the "gamey" nature of the problem.

# Formulation

Let $({c^E\_i})\_{i=0..n}$ be a convex polygon $C$, the _center_. Let $({l\_i})\_{i=0..m}$ be a list of lines called _obstacles_, where $l\_i=(p^0\_i, p^1\_i)$ for $i=0..m$. (This notation identifies the whole line, not just the end points.) Find the boundary of the visibility region $V(C)$, i.e. the set $\bigcup\lbrace(c\_i, x):(c\_i,x)\cap({l\_j})\_{j=0..m}=\emptyset, i=0..n, x\in\mathbb{R}^2\rbrace$.

We make a further assumption that the $V(C)$ is bounded, i.e. the boundary will be a polygon. We also assume that the obstacles contain their intersections as points, i.e. we do not need to find these first: $l\_i\cap l\_j\subset\bigcup\lbrace(p^0_k,p^1_k : k=0..m)\rbrace$ for $i,j=0..m, i\neq j$.

We also assume that $C$ (as area) does not intersect any obstacles.

# Algorithm

We will unite all triangle we find in the following manner. Start with a point on the (boundary of the) center, called $c_0$ with smallest angle $0$ that intersects the obstacles at obstacle point $p_0$, where $p_0$ is closest to $c_0$. We start by rotating counterclockwise at that point, denoting it $c_0^{CCW}$.

$i$ will be the step counter and $c_i$ will always denote (boundary) center points and $p_i$ will be the closest obstacle point. $c_i$ does not need to be a $C^E\_j$, nor does $p_i$ need to be an $p^k_j$. $V(C)$ starts empty.

## Position 1

$$c_i^{CCW}, p_i$$

Rotate around the point to the next point $q' \ne p_i$ (all $p^k_j$ being sorted accordingly). Then pick the closest point $q$ on the ray from $c_i$ through $q'$ on any of the obstacles. Note that the rotation may be $0$. If $q$ is on the same line as $p_i$, add area $(c_i, p_i, q)$ to $V(C)$. Let $p_{i+1} = q$. We are again in position 1. If $q$ is on a different line, it can either be a beginning $q^B$, meaning that the other end of the line has a greater angle with respect to $c_i$ rotation or an end $q^E$, meaning the angle of the other point is smaller. If both are the case, choose $q$ as $q^E$. We may also have the case that $q$ is neither : $q^I$

If $q^B$ is the case, find the closest line $l$ to $c_i$ that has _end_ with at least the angle of $q^B$. That line must exist, because the whole obstacle set bounds the area. It can't have $q^B$ as part, because $q$ was the next point and because of the precondition of the last statement of the last paragraph. This line must also intersect the ray from $c_i$ through $p_i$ because $q$ was the next point, so one end of $l$ must have a smaller angle. Take $l_q$ to be the intersection of the ray $c_i$ through $q$ and $l_p$ the intersection of the ray from $c_i$ through $p_i$. Add area $(c_i, l_q, l_p)$ to $V(C)$. Choose $p_{i+1}^{CW} = q^B$ and $c_{i+1} = c_i$. We are in position 2.

If $q^E$ or $q^I$ are the case, the beginning of the line must have a smaller angle than $p_i$, because $q$ was the next point. Let $l_p$ be the intersection of the ray from $c_i$ through $p_i$. (Probably $l_p$ has a greater distnce from $c_i$ than $p_i$, but I am to lazy to prove that.) Add area $(c_i, q, l_p)$ to $V(C)$. Choose $c_{i+1}^{CCW}=c_i$, $p_{i+1}=q$, we are in position 1.

## Position 2

$$c_i, p_i^{CW}$$

## Position 3

$$c_i, p_i^{CCW}$$

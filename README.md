# Motivation

Some games consider visibility not just from a point source, which is the usual for the _visibility problem_ but from an area. Particularly games, which only allow grid positions, checking visibility from only one point - say the center - leads to artifacts.  But we can make some assumptions that may prove to be valuable, because of the "gamey" nature of the problem.

# Formulation

Let $({c^E\_i})\_{i=0..n}$ be a convex polygon $C$, the _center_. Let $({l\_i})\_{i=0..m}$ be a list of lines called _obstacles_, where $l\_i=(p^0\_i, p^1\_i)$ for $i=0..m$. (This notation identifies the whole line, not just the end points.) Find the boundary of the visibility region $V(C)$, i.e. the set $\bigcup\lbrace(c\_i, x):(c\_i,x)\cap({l\_j})\_{j=0..m}=\emptyset, i=0..n, x\in\mathbb{R}^2\rbrace$.

We make a further assumption that the $V(C)$ is bounded, i.e. the boundary will be a polygon. We also assume that the obstacles contain their intersections as points, i.e. we do not need to find these first: $l\_i\cap l\_j\subset\bigcup\lbrace(p^0_k,p^1_k : k=0..m)\rbrace$ for $i,j=0..m, i\neq j$.

We also assume that $C$ (as area) does not intersect any obstacles.

# Algorithm

We will unite all triangle we find in the following manner. Start with a point on the (boundary of the) center, called $c_0$ with smallest angle $0$ that intersects the obstacles at obstacle point $p_0$, where $p_0$ is closest to $c_0$. We start by rotating counterclockwise at that point, denoting it $c_0^{CCW}$.

$i$ will be the step counter and $c_i$ will always denote (boundary) center points and $p_i$ will be the closest obstacle point. $c_i$ does not need to be a $C^E\_j$, nor does $p_i$ need to be an $p^k_j$.

## Position 1

$c_i^{CCW}$, $p_i$

## Position 2

$c_i$, $p_i^{CW}$

## Position 3

$c_i$, $p_i^{CCW}$

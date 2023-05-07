# Motivation

Some games consider visibility not just from a point source, which is the usual for the _visibility problem_ but from an area. Particularly games, which only allow grid positions, checking visibility from only one point - say the center - leads to artifacts.  But we can make some assumptions that may prove to be valuable, because of the "gamey" nature of the problem.

# Formulation

Let $({c\_i})\_{i=0..n}$ be a convex polygon $C$, the _center_. Let $({l\_i})\_{i=0..m}$ be a list of lines called _obstacles_, where $l\_i=(o^0\_i, o^1\_i)$ for $i=0..m$. (This notation identifies the whole line, not just the end points.) Find the polygon that bounds the visibility region $V(C)$, i.e. the set $\bigcup{(c\_i, x):(c\_i,x)\cap({l\_j})\_{j=0..m}=\emptyset}$.

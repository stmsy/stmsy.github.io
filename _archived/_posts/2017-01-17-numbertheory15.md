---
title: Elementary Number Theory, 15
---

## Solution to Problem 15 of Section 4

*Show that the difference of two consecutive cubes is never divisible by 5 (Dudley 33).*

**Proof:** Because of Problem 14 of the section, for $$n \gt 0$$,

$$(n+1)^3 - n^3 = 3n(n+1) + 1$$

and

\begin{align}
n \equiv 0 \mod 5 \quad & \Rightarrow \quad (n+1)^3-n^3 \equiv 1 \mod 5 \\\\\\
n \equiv 1 \mod 5 \quad & \Rightarrow \quad (n+1)^3-n^3 \equiv 7 \equiv 2 \mod 5 \\\\\\
n \equiv 2 \mod 5 \quad & \Rightarrow \quad (n+1)^3-n^3 \equiv 19 \equiv 4 \mod 5 \\\\\\
n \equiv 3 \mod 5 \quad & \Rightarrow \quad (n+1)^3-n^3 \equiv 37 \equiv 2 \mod 5 \\\\\\
n \equiv 4 \mod 5 \quad & \Rightarrow \quad (n+1)^3-n^3 \equiv 61 \equiv 1 \mod 5 \textrm{,}
\end{align}

the difference is not divisible by $$5$$. *Q.E.D.*

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

---
title: Elementary Number Theory, 17
---

## Solution to Problem 20 of Section 4

*Show that for $$k \gt 0$$ and $$m \geq 1$$, $$x \equiv 1 \mod m^k$$ implies $$x^m \equiv 1 \mod m^{k+1}$$ (Dudley 33).*

**Proof:** Since $$x \equiv 1 \mod m^k$$, there is an integer $$n$$ such that $$x = n \cdot m^k + 1$$. So

\begin{align}
x^m = (nm^k + 1)^m & = \sum_{i=0}^m \left( \begin{array}{c} m \\\\\\ i \end{array} \right)(nm^k)^i \\\\\\
                   & = 1 + nm^{k+1} + \sum_{i=2}^m \left( \begin{array}{c} m \\\\\\ i \end{array} \right)(nm^k)^i \\\\\\
\end{align}

and observe that $$ki \gt k+1$$ for each $$i \geq 2$$. Therefore $$x^m \equiv 1 \mod x^{k+1}$$. *Q.E.D.*

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

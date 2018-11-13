---
title: Elementary Number Theory, 19
---

## Solution to Problem 19 of Section 5

*Suppose that the moduli in the system*

$$x \equiv a_i \mod m_i, \quad i = 1, 2, \dots, k$$

*are not relatively prime in pairs. Find the condition that $$a_i$$ must satisfy in order that the system have a solution (Dudley 41).*

**Solution:** Suppose that the system given above has a solution. So, for every pair of $$i$$ and $$j$$ with $$i, j = 1, 2, \dots, k$$, choose the equations

$$x \equiv a_i \mod m_i$$

and

$$x \equiv a_j \mod m_j\text{.}$$

So there exists some $$t_i$$ such that $$x = m_it_i + a_i$$. Moreover

\begin{align}
x \equiv a_j \mod m_j & \Rightarrow m_it_i + a_i \equiv a_j \mod m_j \\\\\\
                      & \Rightarrow m_it_i \equiv a_j - a_i \mod m_j
\end{align}

and observe that the equation $$m_it_i \equiv a_j - a_i \mod m_j$$ of $$t_i$$ has a solution if and only if $$(m_i, m_j) \mid a_j - a_i$$. Therefore every pair of $$a_i$$ and $$a_j$$ must satisfy the condition that $$a_j - a_i$$ be divisible by $$(m_i, m_j)$$.

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

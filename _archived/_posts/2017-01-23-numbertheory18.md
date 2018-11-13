---
title: Elementary Number Theory, 18
---

## Solution to Problem 17 of Section 5

*If $$x \equiv r \mod m$$ and $$x \equiv s \mod m+1$$, show that*

$$x \equiv r(m+1) - sm \mod m(m+1)$$

*(Dudley 41).*

**Proof:** Since $$x \equiv r \mod m$$, there is an integer $$t$$ such that $$x = r + mt$$. Then

\begin{align}
x \equiv s \mod m+1 & \Rightarrow r + mt \equiv s \mod m+1 \\\\\\
                    & \Rightarrow mt \equiv s - r \mod m+1
\end{align}

and since $$m$$ and $$m+1$$ are relatively prime by the result of *Problem 9* of *Section 2*, there is a unique solution $$t = s-r + (m+1)u$$ for $$mt \equiv s - r \mod m+1$$. So

$$x = r + mt = r + m(s-r + (m+1)u) = r(-m+1) + sm + m(m+1)u$$

and

\begin{align}
x & \equiv r(-m+1) + sm + m(m+1)u + 2rm - 2ms \mod m \\\\\\
  & \equiv r(m+1) - sm + m(m+1)u \mod m
\end{align}

and therefore $$x \equiv r(m+1) - sm \mod m(m+1)$$ as desired. *Q.E.D.*

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

---
title: Elementary Number Theory, 6
---

## Solution to Problem 15 of Section 1

*(a) If $$x^2 + ax + b = 0$$ has an integer root, show that it divides $$b$$.* <br>
*(b) If $$x^2 + ax + b = 0$$ has a rational root, show that it is in fact an integer (Dudley 9).*

(a) **Proof:** Let $$x = r$$ be an integer root for the equation. Then, $$r^2 + ar + b = 0$$ and $$r(r+a) = -b$$, so $$r$$ divides $$b$$. *Q.E.D.*

(b) **Proof:** Let $$r = \frac{p}{q} \in \mathbb{Q}\setminus\mathbb{Z}$$ be a rational root in the lowest common term. Then

$$r^2 + ar + b = 0 \Rightarrow \Big( \frac{p}{q} \Big)^2 + a\Big( \frac{p}{q} \Big) + b = 0\text{,}$$

so $$\frac{p^2}{q} = -ap - bq$$. This is contradiction since the left hand side is in $$\mathbb{Q}\setminus\mathbb{Z}$$ while the right hand side is in $$\mathbb{Z}$$. *Q.E.D.*

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

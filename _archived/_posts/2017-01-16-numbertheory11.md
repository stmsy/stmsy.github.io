---
title: Elementary Number Theory, 11
---

## Solution to Problem 14 of Section 2

*Prove that if $$n$$ is composite, then $$2^n-1$$ is composite (Dudley 19).*

**Proof:** Suppose that $$n$$ is composite, *i.e.*, there exist positive integers $$a$$ and $$b$$ such that $$a \gt 2$$, $$b \gt 2$$ and $$n = ab$$. Then observe that 

\begin{align}
2^a\frac{(2^a)^b-1}{2^a-1} & = 2^a + (2^a)^2 + \cdots + (2^a)^b  \\\\\\
\Rightarrow (2^a)^b-1 & = \frac{2^a-1}{2^a}(2^a + (2^a)^2 + \cdots + (2^a)^b) \\\\\\
\Rightarrow (2^a)^b-1 & = (2^a-1)(1 + 2^{a} + \cdots + 2^{a(b-1)})
\end{align}

and therefore

$$2^n-1 = 2^{ab}-1 = (2^a)^b-1 = (2^a-1)(1 + 2^{a} + \cdots + 2^{a(b-1)})$$

is composite. *Q.E.D.*

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

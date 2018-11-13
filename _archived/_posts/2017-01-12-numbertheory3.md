---
title: Elementary Number Theory, 3
---

## Solution to Problem 10 of Section 1

*(a) Prove that $$(n, n+1) = 1$$ for all $$n > 0$$.* <br>
*(b) If $$n > 0$$, what can $$(n, n+2)$$ be (Dudley 9)?*

**Solution:** (a) **Proof:** Suppose first that $$n$$ is even, *i.e.*, $$n = 2k$$ for some $$k > 0$$. Then, by the Euclidean algorithm,

\begin{align}
n + 1 = 2k + 1 & = 2k \cdot 1 + 1 \\\\\\
2k & = 1 \cdot 2k
\end{align}

and therefore $$(n, n+1) = (2k, 2k+1) = 1$$. Similarly $$(n, n+1) = 1$$ if $$n$$ is odd. *Q.E.D.* <br>

(b) As discussed above, consider two cases: $$n$$ is even or $$n$$ is odd. If $$n$$ is even, then $$n = 2k$$ for some $$k > 0$$. Then,

$$(n, n+2) = (2k, 2k+2) = 2(k, k+1) = 1$$

by the Euclidean algorithm. If $$n$$ is odd, then $$n = 2k+1$$ for some $$k > 0$$, and

\begin{align}
2k + 3 & = (2k+1) \cdot 1 + 2 \\\\\\
2k + 1 & = 2 \cdot k + 1 \\\\\\
2 & = 1 \cdot 2
\end{align}

and hence $$(n, n+2) = (2k+1, 2k+3) = 1$$.

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

---
title: Elementary Number Theory, 8
---

## Solution to Problem 10 of Section 2

*Prove that $$n(n+1)$$ is never a square for $$n \gt 0$$ (Dudley 19).*

**Proof:** Suppose by contradiction that there exists some nonzero integer $$a$$ such that $$n(n+1) = a^2$$. Considering the prime factorization of $$a$$, $$a$$ can be expressed as follows:

$$a = p_{1}^{e_1}p_{2}^{e_2} \cdots p_{m}^{e_m}\text{,}$$

where each $$p_i$$ is prime and $$e_i \gt 0$$ for $$1 \leq i \leq m$$. So,

$$n(n+1) = a^2 = p_{1}^{2e_1}p_{2}^{2e_2} \cdots p_{m}^{2e_m}\text{.}$$

Now, for each $$i$$, let $$f_i$$ with $$0 \lt f_i \leq 2e_i$$ be the largest integer such that $$p_{i}^{f_i} \mid n$$. If $$f_i \neq 2e_i$$, then $$p_i$$ divides both $$n$$ and $$n+1$$, and this contradicts the fact proved in *Exercise 9* of the section. So $$f_i = 2e_i$$. This contradicts however the assumption that $$n \gt 0$$ since

\begin{align}
n(n+1) = p_{1}^{2e_1}p_{2}^{2e_2} \cdots p_{m}^{2e_m} & \Rightarrow n(n+1) = n \\\\\\
& \Rightarrow n+1 = 1 \\\\\\
& \Rightarrow n = 0
\end{align}

and thus $$n(n+1)$$ cannot be a square. *Q.E.D.*

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

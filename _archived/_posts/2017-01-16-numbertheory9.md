---
title: Elementary Number Theory, 9
---

## Solution to Problem 12 of Section 2

*Let $$p$$ be the least prime factor of $$n$$, where $$n$$ is composite. Prove that if $$p > n^{1/3}$$, then $$n/p$$ is prime (Dudley 19).*

**Proof:** Suppose by contradiction that $$n/p$$ is not prime. So let $$q$$ be the least prime factor of $$n/p$$. Observe that $$q \geq p$$ since otherwise $$q$$ would be also the least prime factor of $$n$$. Then

\begin{align}
p \gt n^{1/3} & \Rightarrow p^3 \gt n \\\\\\
              & \Rightarrow p^2 \gt n/p \\\\\\
	      & \Rightarrow p \gt \sqrt{n/p} \\\\\\
\end{align}

and therefore $$q \gt \sqrt{n/p}$$. So every prime factor of $$n/p$$ is greater than $$\sqrt{n/p}$$. This contradicts the result of *Lemma 4* of *Section 2*. Hence $$n/p$$ is prime. *Q.E.D.*

## Reference

Dudley, Underwood. *Elementary Number Theory*. Second Edition, Dover Publications, 2008.

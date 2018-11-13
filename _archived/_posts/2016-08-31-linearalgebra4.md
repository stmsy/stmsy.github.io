---
title: Linear Algebra, 4
#categories: [Linear Algebra, Math]
#tags: [Serge Lang]
---

## Solution to Exercise 12, Section 4 of Chapter III

*Notations being as in Exercise 11, show that the image of $$P$$ is equal to the kernel of $$Q$$ [Prove the two statements: Image of $$P$$ is contained in kernel of $$Q$$, Kernel of $$Q$$ is contained in image of $$P$$.] (Lang 71).*

**Proof:** Let $$v$$ be an element in $$Im P$$. There exists an element $$w$$ in $$V$$ such that $$v = Pw$$. Then

$$Qv = Q(Pw) = QPw = O0 = 0$$

and therefore $$v \in Ker Q$$. Conversely, let $$v$$ be an element of $$Ker Q$$. So $$Qv = 0$$ and 

$$v = Iv = (P + Q)v = Pv + Qv = Pv + 0 = Pv \in Im P$$

since $$Ker Q \subset V$$. *Q.E.D.*

## Reference

Lang, Serge. *Linear Algebra*. Third Edition, Springer, 1987.

---
title: Linear Algebra, 3
---

### Solution to Exercise 11, Section 4 of Chapter III

*Let $$V$$ be a vector space, and let $$P$$, $$Q$$ be linear maps of $$V$$ into itself. Assume that they satisfy the following conditions:

  (a) $$P + Q = I$$ (identity mapping).

  (b) $$PQ = QP = O$$.

  (c) $$P^2 = P$$ and $$Q^2 = Q$$.

Show that $$V$$ is equal to the direct sum of $$Im P$$ and $$Im Q$$ (Lang 71).*

**Proof:** It is easy to show that $$V = Im P + Im Q$$ since

$$v = Iv = (P + Q)v = Pv + Qv \in Im P + Im Q$$

by the condition (a) and the other inclusion is trivial. Now let $$v \in Im P \cap Im Q$$. There exist $$w_P$$ and $$w_Q$$ in $$V$$ such that $$v = Pw_P$$ and $$v = Qw_Q$$. Therefore, by the condition (b),

$$Qv = QPw_P = O0 = 0$$

and

$$Pv = PQw_Q = O0 = 0$$

and hence

$$v = Pv + Qv = PQw_Q + QPw_P = 0 + 0 = 0\text{.}$$

*Q.E.D.*

## Reference

Lang, Serge. *Linear Algebra*. Third Edition, Springer, 1987.

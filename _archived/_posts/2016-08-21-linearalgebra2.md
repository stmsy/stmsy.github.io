---
title: Linear Algebra, 2
#categories: [Linear Algebra, Math]
#tags: [Serge Lang]
---

## Solution to Exercise 10, Section 4 of Chapter III

*Let $$V$$ be a vector space. Let $$P: V \to V$$ be a linear map such that $$P^2 = P$$. Show that $$V = Ker P + Im P$$ and $$Ker P \cap Im P = \{0\}\text{,}$$ in other words, $$V$$ is the direct sum of $$Ker P$$ and $$Im P$$ [Hint: To show $$V$$ is the sum write an element of $$V$$ in the form $$v = v - Pv + Pv$$.] (Lang 71).*

**Proof:** Observe that $$Pv \in Im P$$ and $$v - Pv \in Ker P$$ since

$$P(v - Pv) = Pv - P^2v = Pv - Pv = 0\text{.}$$

So $$V = Ker P + Im P$$. Now let $$v \in Ker P \cap Im P$$. Since $$v \in Im P$$, there is an element $$w \in V$$ such that $$v = Pw$$. Then

$$Pv = P^2w \Rightarrow 0 = Pw$$

since $$v \in Ker P$$, and thus $$v = Pw = 0$$. Therefore $$Ker P \cap Im P = \{0\}$$. *Q.E.D.*

## Reference

Lang, Serge. *Linear Algebra*. Third Edition, Springer, 1987.

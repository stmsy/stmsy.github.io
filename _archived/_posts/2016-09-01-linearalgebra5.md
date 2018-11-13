---
title: Linear Algebra, 5
#categories: [Linear Algebra, Math]
#tags: [Serge Lang]
---

## Solution to Exercise 13, Section 4 of Chapter III

*Let $$T: V \to V$$ be a linear map such that $$T^2 = I$$. Let $$P = \frac{1}{2}(I + T)$$ and $$Q = \frac{1}{2}(I - T)$$. Prove: $$P + Q = I; P^2 = P; Q^2 = Q; PQ = QP = O$$ (Lang 71).*

**Proof:** It is easy to show that $$P + Q = I$$. Then

$$
P^2 = \frac{1}{4}(I + T)(I + T) = \frac{1}{4}(I + 2T + T^2) = \frac{1}{4}(2I + 2T) = \frac{1}{2}(I + T) = P
$$

and similarly $$Q^2 = Q$$. Finally 

$$
PQ = \frac{1}{4}(I + T)(I - T) = \frac{1}{4}(I - T^2) = O
$$

and similarly $$QP = O$$. **Q.E.D.**

## Reference

Lang, Serge. *Linear Algebra*. Third Edition, Springer, 1987.

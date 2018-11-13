---
title: Linear Algebra, 1
#categories: [Math, Linear Algebra]
#tags: [Serge Lang]
---

## Solution to Exercise 4, Section 3 of Chapter III

*Let $$L: V \to W$$ be a linear map. Let $$w$$ be an element of $$W$$. Let $$v_0$$ be an element of $$V$$ such that $$L(v_0) = w$$. Show that any solution of the equation $$L(X) = w$$ is of type $$v_0 + u$$, where $$u$$ is an element of the kernel of $$L$$ (Lang 63).* 

**Proof:** Let $$x = v_0 + u$$ with $$u \in Ker L$$. Then

$$L(x) = L(v_0 + u) = L(v_0) + L(u) = w + 0_W = w$$

and thus $$x$$ is a solution to the equation above. *Q.E.D.*

## Reference

Lang, Serge. *Linear Algebra*. Third Edition, Springer, 1987.
---
title: Fields and Galois Theory, 2
---

## Solution to Exercise 1.5 of Chapter 1

*Show that every finite integral domain is a field (Howie 5).*

**Proof:** It suffices to show that every nonzero and nonunity element of a finite integral domain $$D$$ is a unit. So suppose by contradiction that there is an element $$u$$ with $$u \neq 0$$ and $$u \neq 1$$ such that $$uv_i \neq 1$$ for every $$v_i$$ in $$D$$ with $$v_i \neq 0$$ and $$v_i \neq 1$$ for $$1 \leq i \leq n-2$$, or otherwise $$u$$ is a unit. Now observe that

$$u(v_1v_2 \cdots v_{n-2}) \neq 1$$

or otherwise $$u$$ is a unit. Also,

$$u(v_1v_2 \cdots v_{n-2}) \neq v_j$$

or otherwise the cancellation law applies, *i.e.*, 

\begin{align}
u(v_1v_2 \cdots v_{n-2}) = v_j & \Rightarrow v_ju(v_1v_2 \cdots v_{j-1}v_{j+1} \cdots v_{n-2}) = v_j1 \\\\\\
                               & \Rightarrow u(v_1v_2 \cdots v_{j-1}v_{j+1} \cdots v_{n-2}) = 1
\end{align}

and this contradicts the assumption that $$u$$ is not a unit. Therefore $$D$$ is a field. *Q.E.D.*

## Reference

Howie, John. *Fields and Galois Theory*, Springer, 2005.

---
title: Fields and Galois Theory, 4
---

## Solution to Exercise 1.14 of Chapter 1

*Show that $$\mathbb{Q}(i\sqrt{3}) = \{a + bi\sqrt{3} \mid a, b \in \mathbb{Q}\}$$ is a subfield of $$\mathbb{C}$$ (Howie 12).*

**Proof:** Let $$x$$ and $$y$$ be taken arbitrarily from $$\mathbb{Q}(i\sqrt{3})$$. There are $$a$$, $$b$$, $$a'$$ and $$b'$$ in $$\mathbb{Q}$$ such that $$x = a + bi\sqrt{3}$$ and $$x = a' + b'i\sqrt{3}$$. Then

\begin{align}
x - y & = (a + bi\sqrt{3}) - (a' + b'i\sqrt{3}) \\\\\\
      & = (a - a') + (b - b')i\sqrt{3} \\\\\\
\end{align}

implies that $$x - y \in \mathbb{Q}(i\sqrt{3})$$. Moreover, if $$x \neq 0$$, then $$a \neq 0$$, $$b \neq 0$$ and 

\begin{align}
x^{-1} & = \frac{1}{a + bi\sqrt{3}} \\\\\\
       & = \frac{1}{a + bi\sqrt{3}} \cdot \frac{a - bi\sqrt{3}}{a - bi\sqrt{3}} \\\\\\
       & = \frac{a - bi\sqrt{3}}{a^2 + 3b^2} \\\\\\
       & = \frac{a}{a^2 + 3b^2} - \frac{b}{a^2 + 3b^2}i\sqrt{3}
\end{align}

and hence $$x^{-1} \in \mathbb{Q}(i\sqrt{3})$$. Therefore $$\mathbb{Q}(i\sqrt{3})$$ is a subfield of $$\mathbb{C}$$. *Q.E.D.*

## Reference

Howie, John. *Fields and Galois Theory*, Springer, 2005.

---
title: Fields and Galois Theory, 5
---

## Solution to Exercise 1.15 of Chapter 1

*(i) Show that the set*

\begin{equation}
\begin{pmatrix}a & b \\\\\\ -3b & a \end{pmatrix}
\end{equation}

*is a field with respect to matrix addition and multiplication.*

*(ii) Show that $$K$$ is isomorphic to the field $$\mathbb{Q}(i\sqrt{3})$$ defined in the previous exercise (Howie 12).*

(i) **Proof:** *Left to readers*.

(ii) **Proof:** Define $$\varphi: \mathbb{Q}(i\sqrt{3}) \to K$$ by

\begin{equation}
\varphi(a + bi\sqrt{3}) = \begin{pmatrix}a & b \\\\\\ -3b & a \end{pmatrix}\text{.}
\end{equation}

It is easy to show that: $$\varphi$$ is one-to-one; $$\varphi$$ is onto. So it remains to show that $$\varphi$$ is a homomorphism. For all $$a + bi\sqrt{3}$$ and $$a' + b'i\sqrt{3}$$,

\begin{align}
\varphi((a+bi\sqrt{3})+(a'+b'i\sqrt{3})) & = \varphi((a+a')+(b+b')i\sqrt{3}) \\\\\\
       & = \begin{pmatrix}a+a' & b+b' \\\\\\ -3(b+b') & a+a' \end{pmatrix} \\\\\\
       & = \begin{pmatrix}a & b \\\\\\ -3b & a \end{pmatrix} + \begin{pmatrix}a' & b' \\\\\\ -3b' & a' \end{pmatrix} \\\\\\
       & = \varphi(a+bi\sqrt{3}) + \varphi(a'+b'i\sqrt{3})
\end{align}

and 

\begin{align}
\varphi((a+bi\sqrt{3})(a'+b'i\sqrt{3})) & = \varphi((aa'-3bb')+(ab'+ba')i\sqrt{3}) \\\\\\
 & = \begin{pmatrix}aa'-3bb' & ab'+ba' \\\\\\ -3(ab'+ba') & aa'-3bb' \end{pmatrix} \\\\\\
 & = \begin{pmatrix}a & b \\\\\\ -3b & a \end{pmatrix}\begin{pmatrix}a' & b' \\\\\\ -3b' & a' \end{pmatrix} \\\\\\
 & = \varphi(a+bi\sqrt{3})\varphi(a'+b'i\sqrt{3})
\end{align}

as desired. Therefore $$\varphi$$ is and isomorphism and $$K$$ is isomorphic to $$\mathbb{Q}(i\sqrt{3})$$. *Q.E.D.*

## Reference

Howie, John. *Fields and Galois Theory*, Springer, 2005.

---
layout: post
title: Properties of Direction Cosine Matrix
date: 2019-10-15
category: space
---

### Determinant of DCM is $$\pm 1$$

We know that,

$$
\begin{equation}
[C][C]^\intercal = [I_{3 \times 3}]
\end{equation}
\label{eq:c_identity}
$$

Taking determinant on both sides, we get,

$$
\begin{equation}
det([C][C]^\intercal) = det([I_{3 \times 3}]) = 1
\end{equation}
\label{eq:det_equn}
$$

For any square matrices $$A$$ and $$B$$, 

$$
\begin{equation*}
det(AB) = det(A)det(B).
\end{equation*}
$$

Therefore,

$$
\begin{equation}
det(CC^\intercal) = det(C)det(C^\intercal) = 1.
\end{equation}
$$

Since transposing a square matrix doesn't change its determinant value, 
$$det(C) = det(C^\intercal).

Now, equation \eqref{eq:det_equn} can be written as,

$$
\begin{equation}
det(CC^\intercal) = [\mathrm{det}(C)]^{2} = 1
\end{equation}
$$

or

$$
\begin{equation}
\boxed{\mathrm{det}(C) = \pm 1}.
\end{equation}
$$

It can also be shown that $$\mathrm{det}(C) = +1$$, if the reference frame
base vectors are right-handed.

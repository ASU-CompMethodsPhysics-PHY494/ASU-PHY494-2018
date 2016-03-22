---
layout: post
title: 12 Linear Algebra
---

A large number of problems in physics can be formulated in the
language of linear algebra. Not only is quantum mechanics "just"
linear algebra over a complex vector space but we encounter repeatedly
the case that a large number of equations have to be solved
simultaneously in a form that makes them amenable to linear algebra
methods.

## Basic problems in linear algebra

### Coupled linear equations

Given a known $$N \times N$$ matrix $$\mathsf{A}$$ and an $$N$$-element vector
$$\mathbf{b}$$, the matrix equation

\begin{gather}
\mathsf{A} \mathbf{x} = \mathbf{b}
\end{gather}

represents a system of $$N$$ **coupled linear equations** in the $$N$$
unknowns $$\mathbf{x} = (x_1, x_2, \dots, x_N)$$.

### Eigenvalue problem

The matrix equation

\begin{gather}
\mathsf{A} \mathbf{x}_i = \lambda_i \mathbf{x}_i
\end{gather}

is the **eigenvalue problem** and a solution provides the eigenvalues
$$\lambda_i$$ and corresponding eigenvectors $$\mathbf{x}_i$$ that
satisfy the equation. 

### Matrix inverse

Sometimes you want to explicitly find the **inverse of a matrix**, $$\mathsf{A}^{-1}$$, 

\begin{gather}
\mathsf{A} \mathsf{A}^{-1} = \mathsf{A}^{-1} \mathsf{A} = \mathsf{1}
\end{gather}

If the matrix is *singular* (i.e., the inverse does not exist or
equivalently, $$\det\mathsf{A} = 0$$) one can still obtain a useful
equivalent of the inverse, $$\mathsf{W}^{-1}$$, through **singular
value decomposition** ("SVD")

\begin{gather}
\mathsf{A} = \mathsf{U} \mathsf{W} \mathsf{V}^{T}
\end{gather}

where $$\mathsf{W} = \mathrm{diag}(w_j), \ 1 \leq j \leq N,$$ is a
diagonal matrix and the other matrices are orthogonal
$$\mathsf{U}\mathsf{U}^{T} = \mathsf{V} \mathsf{V}^{T} =
\mathsf{1}$$).[^1] For non-singular matrices

\begin{gather}
\mathsf{A}^{-1} =
  \mathsf{V}\, \mathrm{diag}\left(\frac{1}{w_j}\right) \, \mathsf{U}^{T}
\end{gather}

but even for singular matrices

\begin{gather}
\mathbf{x} = \mathsf{V} \mathsf{W}^{-1} \mathsf{U}^{T}\, \mathbf{b}
\end{gather}

will be a useful answer:

- For a $$N \times N$$ matrix, values $$w_j = 0$$ indicate precisely
  where $$\mathsf{A}$$ is singular and very small $$w_j$$ also alert
  you to possible numerical problems (the solution might easily become
  dominated by round-off error and the matrix is said to be
  "ill-conditioned").
- For an overdetermined system (more equations than unknowns[^2])
  $$\mathbf{x}$$ solves the **least-squares fitting problem** and
  determines the solution that minimizes the deviation in the
  least-squares sense.
- For an underdetermined system (fewer equations than unknowns[^3]) it
  can be used to find all the vectors that span the solution space.

## Numerical solution

Efficient algorithms exist to solve these problems and we will
primarily use the optimized algorithms in the
[numpy.linalg](http://docs.scipy.org/doc/numpy/reference/routines.linalg.html)
package:
{% highlight python %}
import numpy.linalg
{% endhighlight %}

For most linear algebra work you should be using *double precision*
because diagonalization routines and eigenvalue solvers have
problems with nearly singular matrices and the better the machine
precision is, the better one can distinguish a nearly singular matrix
from a truly singular one.

## Class material

The Jupyter notebook [12_Linear_Algebra.ipynb](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/12_linear_algebra/12_Linear_Algebra.ipynb) will contain the
(life-coded) lecture notes. Skeleton code for in-class exercises can
be found in [12_Linear_Algebra-students-1.ipynb](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/12_linear_algebra/12_Linear_Algebra-students-1.ipynb).[^4]


#### Additional resources:

* _Computational Physics_: Chapter **6**
* _[Numerical Recipes in C](http://apps.nrbook.com/c/index.html)_, WH
  Press, SA Teukolsky, WT Vetterling, BP Flannery. 2nd
  ed, 2002. Cambridge University Press. Chapter **2**.


--------

#### Footnotes

[^1]: For singular matrices, some elements on the diagonal of
      $$\mathsf{W}$$ are zero so in order to form the pseudo-inverse
      $$\mathsf{W}^{-1} = \mathrm{diag}(1/w_j)$$ these elements have
      to be augmented and replaced by zero in $$\mathsf{W}^{-1}$$.

[^2]: The *overdetermined system* has more equations $$M$$ than unknowns
      $$N$$, $$M > N$$, i.e., the solution vector $$\mathbf{x}$$ has
      $$N$$ elements but the matrix $$\mathsf{A}$$ now has the shape
      $$M \times N$$.

[^3]: The *underdetermined* system does not typically have a unique
      solution because is has $$M < N$$.

[^4]: As usual, `git pull` the
      [resources repository](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources)
      to get a local copy of the notebook. Then copy the notebook into
      your work directory in order to complete the exercises.
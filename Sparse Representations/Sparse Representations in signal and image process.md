# Sparse Representations

## Underdetermined Linear Systems

$$
A\underline x=\underline b
$$

with n equations and m>n unknowns, where A is full-rank. This system clearly has infinitely many solutions. We want to get a meaningful single solution.

## Regularization

The idea is to assign every possible solution with a grade that defines its "quality", and then choose the single solution that has the best such grade.

Define the general optimization problem (Pj)
$$
(P_j): \min_x J(\underline x) \space s.t.\pmb A\underline x=\underline b
$$
The most popular regularization is L2-based expressions of this form.
$$
J(\underline x)=\frac{1}{2}||\pmb B\underline x||_2^2
$$

for some chosen matrix B.

Advantages:

- simplicity
- closed-form
- unique

## Convexity

### Definitions

- convex sets

  A set Ω is convex if ∀x1, x2 ∈ Ω and ∀t ∈ [0, 1], the convex combination
  $$
  \underline x=t\underline x_1+(1-t)\underline x_2
  $$
  is also in Ω.

- convex functions

  A function
  $$
  J(\underline x):\Omega \rightarrow \R
  $$
  if ∀x1, x2 ∈ Ω and ∀t ∈ [0, 1], the convex combination point
  $$
  \underline x=t\underline x_1+(1-t)\underline x_2
  $$
  satisfies
  $$
  J(t\underline x_1+(1-t\underline )x_2)\le tJ(\underline x_1)+(1-t)J(\underline x_2)
  $$
  
- convex functions via derivatives

  A function
  $$
  J(\underline x):\Omega \rightarrow \R
  $$
   is convex if ∀x1, x2 ∈ Ω if and only if
  $$
  J(\underline x_2)\ge J(x_1)+\triangledown J(\underline x_1)^T(\underline x_2-\underline x_1)
  $$
  or alternatively, if and only if 
  $$
  \triangledown J(\underline x_1)
  $$
   is positive-definite.

- convexity vs. strict convexity

Example:

Is the following function (strictly) convex?
$$
J(\underline x)=\frac{1}{2}||\pmb B\underline x||_2^2
$$


Answer:

If
$$
J(\underline x)=\frac{1}{2}||\pmb B\underline x||_2^2=\frac{1}{2}((\sum_{k=1}^{n}(\pmb Bx_k)^2)^{1/2})^2=\frac{1}{2}\sum_{k=1}^{n}(\pmb Bx_k)^2
$$

then
$$
\frac{\partial}{\partial x_j}J(\underline x)=\frac{1}{2}\frac{\partial}{\partial x_j}\sum_{k=1}^{n}(\pmb Bx_k)^2=\frac{1}{2}\sum_{k=1}^{n}\frac{\partial}{\partial x_j}(\pmb Bx_k)^2=\begin{cases}
0 & if\space j \neq k,\\
\pmb B^T\pmb Bx_j & else.
\end{cases}
$$

The first derivative of this expression is given by 
$$
\triangledown J(\underline x)=\pmb B^T\pmb B\underline x
$$
and the second derivative is 
$$
\triangledown^2J(\underline x)=\pmb B^T\pmb B
$$
If B has full column-rank, then 
$$
\pmb B^T\pmb B
$$
is positive definite, and thus this function is strictly convex.

> Theorem: Consider the following constrained problem:
> $$
> \min_x f(\underline x)\space s.t. \underline x\in \Omega
> $$
> where 
> $$
> f(\underline x):\Omega \rightarrow \mathbb{R}
> $$
> is a convex function and Ω is a convex set. Then:
>
> - Every local minimum point is a global one
> - The set of optimal solutions forms a convex set
> - If f(x) is strictly convex, the solution is unique

### Which J(x) to Choose?

- Lp-norm (p≥1): 
  $$
  ||\underline x||_p=\sqrt[p]{\sum_k|x_k|^p}
  $$

- Special cases of interest are 
  $$
  L_1:||\underline x||_1=\sum_k|x_k|
  $$

  $$
  L_\infty:||\underline x||_\infty=\max_k|x_k|
  $$

  Note:

1. L1 is convex but not strictly so
2. For all 1<p<∞, the norm function is convex but not strictly so. Its p-th power becomes strictly-convex (just like the L2 case)
3. For p<1, the above is not a convex function, and therefore it is not a formal norm

### Norms vs. Convexity

A norm is a function
$$
||x||:\R^m\rightarrow \R
$$
with the properties:

- Non-negativity:
  $$
  \forall \space \underline x,\space ||\underline x||\ge 0 \space and \space ||\underline x||=0\rightarrow \underline x=0
  $$

- Homogeneity:
  $$
  \forall \underline x \space \& \space \forall c, \space ||c\underline x||=|c|\space||\underline x||
  $$

- Triangle-Inequality:
  $$
  \forall \underline x,\underline y,\space ||\underline x+\underline y|| \le ||\underline x||+||\underline y||
  $$

For 0≤t≤1 and for any pair of vector x and y,
$$
||t\underline x+(1-t)\underline y||\le ||t\underline x||+||(1-t)\underline y||
$$
or
$$
||t\underline x+(1-t)\underline y||\le t||\underline x||+(1-t)||\underline y||
$$
Any valid norm function is necessarily convex.
$$
||\underline x||_p^p=\sum_k|x_k|^p
$$
with p<1 is not convex and thus not a valid norm.

## A Closer Look at L1 Minimization

Recall:
$$
J(\underline x)=||\underline x||_1
$$
is convex but not strictly so. Thus, the problem
$$
(P_1): \min_x||\underline x||_1 s.t.\space \pmb A\underline x=\underline b
$$
may have more than one solution.

### Two theorems

> Theorem: The set of optimal solutions of (P1), denoted as S, forms a bounded and convex set.

> Theorem: The set of optimal solutions of (P1), denoted as S, must contain a solution with at most n non-zeros.

## Conversion of (P1) to Linear Programming

> Linear Programming (Wikipedia): Linear programming (LP, also called linear optimization) is a method to achieve the best outcome (such as maximum profit or lowest cost) in a mathematical model whose requirements are represented by linear relationships. Linear programming is a special case of mathematical programming (also known as mathematical optimization).

General LP structure:
$$
(LP):\min_x\underline  c^T\underline x \space s.t.\space \pmb A\underline x=\underline b \space\&\space \underline x \ge \underline0
$$
Split the unknown x to its positive and negative entries:
$$
\underline x=\underline u-\underline v\space where \space \underline x,\underline u,\underline v \in \R^m \space and \space \underline u\ge\underline 0 \space\&\space \underline v\ge\underline 0
$$
We can also get:
$$
\underline u^T \underline v=0
$$
For P1 problem, 
$$
(P_1): \min_x||\underline x||_1 s.t.\space \pmb A\underline x=\underline b
$$
We can get a new form of this equivalent description, 
$$
||\underline x||_1=\sum_{k=1}^m|x_k|=\sum_{k=1}^mu_k+\sum_{k=1}^mv_k=\left[\begin{matrix} \underline 1^T & \underline 1^T\end{matrix}\right]\left[\begin{matrix} \underline u\\\underline v\end{matrix}\right]
$$

$$
\underline b=\pmb A \underline x=\pmb A(\underline u-\underline v)=\left[\begin{matrix}\pmb A & -\pmb A\end{matrix}\right]\left[\begin{matrix}\underline u\\\underline v\end{matrix}\right] \space and \space \left[\begin{matrix}\underline u\\\underline v\end{matrix}\right] \ge \underline 0
$$

So, the final form looks like:
$$
(LP):\min_{\underline u,\underline v}\left[\begin{matrix} \underline 1^T & \underline 1^T\end{matrix}\right]\left[\begin{matrix} \underline u\\\underline v\end{matrix}\right] \space s.t. \space \underline b=\left[\begin{matrix}\pmb A & -\pmb A\end{matrix}\right]\left[\begin{matrix}\underline u\\\underline v\end{matrix}\right] \space and \space \left[\begin{matrix}\underline u\\\underline v\end{matrix}\right] \ge \underline 0
$$
However, there is one difficulty - the condition that u and v are orthogonal to each other ruins the LP structure.

> Theorem: The constraint 
> $$
> \underline u^T\underline v=0
> $$
> is a passive one and thus can be omitted from the LP formulation without harm.

That is, this constraint is a passive constraint.


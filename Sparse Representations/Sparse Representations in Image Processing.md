# Sparse Representations in Image Processing

## Section 0: Introduction

### What This Field is All About: Modeling Data

#### Model

A model: a mathematical description of the underlying signal of interest, describing our beliefs regarding its structure.

Good models: simplicity and reliability.

#### What This Field is all About?

Sparse Representation Theory puts forward a new and highly effective data model, along with the required tools for using it in practice.

#### Sparseland Model

<img src="Sparse Representations in Image Processing.assets/sparseland.png" style="zoom: 33%;" />

### Theoretical & Algorithmic Background

#### An Introduction of L0 and (P0)

<img src="Sparse Representations in Image Processing.assets/relation.png" alt="image-20210120162212238" style="zoom:67%;" />
$$
x=D\alpha
$$
In this relation, x is a signal of interest, and alpha would be its redundant representation.

D is an underdetermined m x n matrix (m > n), referred to as the dictionary, typically assumed to be full-rank.

So this linear system necessarily has infinitely many possible solutions.

Among these we seek the one with the fewest non-zones.

Problem P0:
$$
(P_0)\space\min_{\alpha} ||\alpha||\space subject\space to \space x=D\alpha
$$
The L0-norm
$$
||\alpha||_0
$$
counts the non-zeros in α.

It turns out that when you take the p-th power of the Lp norm and p is getting closer to zero, you get exactly this counting effect.

#### From (P0) to (P0-epsilon)

The problem P0 we have just defined is impractical, since it expects the signal x to be exactly equal to D times alpha. A more useful variation of it is the P0-epsilon problem, given by this expression.
$$
(P_0^\epsilon)\space\min_{\alpha} ||\alpha||\space subject\space to \space ||D\alpha-y||^0\leqslant\epsilon^2
$$
It is a relaxed version of (P0): robust to perturbations (additive noise) in D and y, and to small non-zero entries in the solution.

A Difficulty: (P0) and (P0 ε ) are too (NP-) hard to solve. If the solution has k non-zeros, the number of support possibilities to consider is m-choose-k, which is exponential in m.

Intuitively, this can be explained by the exponential number of possible supports (location of the non-zeros) that need to be checked in the quest for the solution.

#### Algorithms for Handling (P0-epsilon)

Using approximation methods:

- Greedy algorithms: OMP, LS-OMP, MP, WMP, THR
- Relaxation algorithms: Basis-Pursuit, IRLS, and more

Three algorithms in detail: OMP, Thresholding, and Basic Pursuit.

Our goal: Approximating the solution of
$$
(P_0^\epsilon)\space \min_{\alpha} s.t. ||D\alpha-y||_2^2\leqslant\epsilon^2
$$

#### The Orthogonal Matching Pursuit (OMP)

- The OMP is a greedy algorithm, building the solution D one non-zero at a time.

- In every round, the OMP holds the current residual 

$$
r_k=y-D\alpha_k
$$

- The next atom to join the support is the one most-correlated with the above residual.

- Once the support has been updated, the non-zeros are recomputed by a simple Least-Squares.

<img src="Sparse Representations in Image Processing.assets/OMP.png" alt="OMP" style="zoom: 50%;" />

In each round, we apply several steps.

1. The first of which is to compute the correlation of the current residual with all the atoms, and finding the one with the maximal absolute value.
2. Given the updated support we compute the non-zeros in these locations by least-squares.
3. We conclude by updating the residual, to be used in the next round.
4. If this residual's norm is small enough, the process stops, and otherwise we simply proceed.

Comments:

- The current residual is necessarily orthogonal to the chosen atoms, thus the name "Orthogonal ...".
- Because of this, OMP never chooses the same atom twice.

#### The Thresholding Algorithm

- The Thresholding algorithm is the simplest (and crudest) pursuit method.

- It decides on the order of atoms to join the support by sorting once the vector 
  $$
  D^Ty
  $$

- Once the support has been decided, the solution is computed either by 
  - a plain Least-Squares as in the OMP, or

  - simply taking the leading values of 
    $$
    D^Ty
    $$


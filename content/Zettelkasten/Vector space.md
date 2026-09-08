---
tags:
  - linear-algebra
date_created: 2025-10-29 23:12
status: concept
aliases: []
---

# Definition
*Addition* and *scalar multiplication* [@strangIntroductionLinearAlgebra2016]:
![[vector-space-mov.png]]
- An *addition* on a set $V$ is **a function** that assigns an element $u + v \in V$ to each pair of elements $u, v \in V$.
- A *scalar multiplication* on a set $V$ is **a function** that assigns an element $\lambda v \in V$ to each $\lambda \in F$ and each $v \in V$.

A *vector space* is a set $V$ with an *addition* and a *scalar multiplication* on $V$ that statisfy the properties:
## Commutativity
$$
u + v = v + u \quad \forall u, v \in V
$$
## Associativity
$$
\begin{align*}
(u + v) + w &= u + (v + w)\\
(ab)v &= a(bv)
\end{align*}
$$
$\forall u, v, w \in V, \quad \forall a, b \in F$
## Additive identity
There exists an element $0 \in V$ such that
$$
v + 0 = v \quad \forall v \in V
$$
## Additive inverse
For every $v \in V$, there exists $w \in V$ such that
$$
v + w = 0
$$
## Multiplicative indentity
$$
1 v = v \quad \forall v \in V
$$
## Distributive properties
$$
\begin{align*}
a(u + v) &= au + av\\
(a + b)v &= av + bv
\end{align*}
$$
$\forall a, b \in F, \quad \forall u, v \in V$
Notice that two distributive laws are different: in the first, on the LHS, $+$ is in $F$, in the second in $V$.

Elements of a *vector space* are called *vectors* or *points*.
# Direct consequences
## 0v = 0
$$
0v = 0, \quad \forall v \in V
$$
- The 0 in the RHS is the number $0 \in F$.
- The 0 in the LHS is the vector $0 \in V$.

PROOF:
$$
\begin{align*}
0v &= (0 + 0)v & (\text{additive indentity})\\
&= 0v + 0v & (\text{distributive property})
\end{align*}
$$
Add both sides with $-0v$,
$$
0v - 0v = 0v + 0v - 0v \iff 0 = 0v \quad (\text{additive identity + associativity})
$$

# Intuition
The motivation comes from the properties of addition and scalar multiplication in $F^n$ [@axlerLinearAlgebraDone2024]:
- Addition: commutative, associative, has an identity, additive inverse, distributive.
- Scalar multiplication: associative, multiplication by 1 acts as expected, distributive.

Since the scalar multiplication in a vector space depends on $F$, to be precise, instead of simply saying that $V$ is a vector space, we'll say 
$$
V \text{ is a vector space over } F
$$
- $\mathbb{R}^n$ is a vector space over $\mathbb{R}$.
- $C^n$ is a vector space over $C$.
# Examples
**Example 1:** Suppose $V$ is the set of real-valued functions on the interval $[0, 1]$. For $f, g \in V$ and $\lambda \in \mathbb{R}$, define $f+ g$ and $\lambda f$ by
$$
(f + g) (x) = f(x) + g(x)
$$
and
$$
(\lambda f) (x) = \lambda f(x)
$$
Thus $f + g \in V$ and $\lambda f \in V$.

**Example 2:** $F^n$ with the usual operations of addition and scalar multiplication is a vector space
- A vector space over $\mathbb{R}$ is called a *real vector space*.
- A vector space over $C$ is called a *complex vector space*.

**Example 3:** The simplest vector space is $\{0\}$, which contains only one point.
# Properties / Notes
## Unique additive identity theorem
A vector space has a unique additive identity.

PROOF [@axlerLinearAlgebraDone2024]:
Suppose $0$ and $0'$ are both additive identities for some vector space $V$,
Then
$$
\begin{align*}
0' &= 0' + 0 && (0 \text{ is an additive identity})\\
&= 0 + 0' && (\text{commutativity})\\
&= 0 && (0' \text{ is an additive identity})
\end{align*}
$$
Thus $0 = 0' \Rightarrow V$ has only one additive identity.
## Unique additive inverse theorem
Every element in a vector space has a unique additive inverse.

PROOF [@axlerLinearAlgebraDone2024]:
Suppose $V$ is a vector space. Let $v \in V$. Suppose $w$ and $w'$ are additive inverses of $v$. Then
$$
w = w + 0 = w + (v + w') = (w + v) + w' = 0 + w' = w'
$$
Thus $w = w'$.

CONSEQUENCE: Because additive inverses are unique, the notation of $-v, w - v$ are now make sense. Let $v, w \in V$. Then
- $-v$ denotes the additive inverse of $v$;
- $w - v$ is defined to be $w + (-v)$.
## A set can be a vector space over different fields
Some intuitive examples:
### R as a R-vector space
This is the real line, its basis consisting of one element, e.g. $\{1\}$.
$$
\dim_{\mathbb{R}} (\mathbb{R}) = 1
$$
A vector is just a number $r \in \mathbb{R}$. 
Scalar multiplication is just the usual multiplication
$$
r \cdot 1
$$
- $r \in \mathbb{R}$: scalar
### C as an R-vector space
This is the complex plane, a basis might be
$$
\{1, i\}
$$
with dimension
$$
\dim_{\mathbb{R}} (C) = 2
$$
A vector in $C$ can be expressed as
$$
z = a + bi
$$
- $a, b \in \mathbb{R}$
If $r \in \mathbb{R}$, we have scalar multiplication
$$
rz = r (a + bi) = ra + rb_i
$$
### C as an C-vector space
Back to one dimension, a basis might be
$$
\{1\}
$$
Its dimension
$$
\dim_C(C) = 1
$$
A vector in $C$ can be expressed as
$$
z = \underbrace{(a + bi)}_{\text{scalar}} \cdot 1
$$
## Finite sets vs finite-dimensional vector space

| sets                                                                                                             | vector spaces                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| $S$ is a finite set                                                                                              | $V$ is a finite-dimensional vector space                                                                        |
| $\#S$                                                                                                            | $\dim V$                                                                                                        |
| for subsets $S_1, S_2$ of $S$, the union $S_1 \cup S_2$ is the smallest subset of $S$ containing $S_1$ and $S_2$ | for subspaces $V_1, V_2$ of $V$, the sum $V_1 + V_2$ is the smallest subspace of $V$ containing $V_1$ and $V_2$ |
| $\#(S_1 \cup S_2) = \#S_1 + \#S_2 - \#(S_1 \cap S_2)$                                                            | $\dim(V_1 + V_2) = \dim V_1 + \dim V_2 - \dim(V_1 \cap V_2)$                                                    |
| $\#(S_1 \cup S_2) = \#S_1 + \#S_2 \iff S_1 \cap S_2 = \emptyset$                                                 | $\dim(V_1 + V_2) = \dim V_1 + \dim V_2 \iff V_1 \cap V_2 = \{0\}$                                               |
| $S_1 \cup \cdots \cup S_m$ is a disjoint union $\iff \#(S_1 \cup \cdots \cup S_m) = \#S_1 + \cdots + \#S_m$      | $V_1 + \cdots + V_m$ is a direct sum $\iff \dim(V_1 + \cdots + V_m) = \dim V_1 + \cdots + \dim V_m$             |
A comparison table from [@axlerLinearAlgebraDone2024] showing the analogy between sets and vector spaces.

---
# References

https://web.stanford.edu/class/math51h/vectorspaces.pdf

https://math.stackexchange.com/questions/3291348/what-is-the-precise-definition-of-a-complex-vector-space
Declaration: AlgebraicCombinatorics.CauchyBinet.det_charPoly_coeff', AlgebraicCombinatorics.CauchyBinet.det_charPoly_coeff
Module: AlgebraicCombinatorics.CauchyBinet

Statement id: stmt-algebraic-combinatorics-prop.det.charpol-explicit

## INFORMAL STATEMENT
prop.det.charpol-explicit

Let $n\in \mathbb {N}$. Let $A\in K^{n\times n}$ be an $n\times n$-matrix. Let $x\in K$. Let $I_n$ denote the $n\times n$ identity matrix. Then, 

\[  \det (A + x I_n) = \sum _{P\subseteq [n]} \det (\operatorname {sub}_P^P A) \cdot x^{n-|P|} = \sum _{k=0}^{n} \biggl(\sum _{\substack {P\subseteq [n];\\ |P|=n-k}} \det (\operatorname {sub}_P^P A)\biggr) x^k.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: yes. The elaborated signatures quantify over `{R : Type u} [CommRing R]`, `{n : \u2115}`, `A : Matrix (Fin n) (Fin n) R`, and `x : R`. The apparent `CommRing` hypothesis is not added drift: the source context states, \u201cFor the rest of Section ... we fix a commutative ring K.\u201d The first declaration asserts exactly `(A + x \u2022 1).det = \u2211 P, ...det * x ^ (n - #P)`, matching \u201cdet(A + x I_n) = sum_{P subseteq [n]} det(sub_P^P A) \u00b7 x^{n-|P|}.\u201d Here `P : Finset (Fin n)` ranges over every subset of `[n]`; `Matrix.submatrix` is documented as having entries `M (r i) (c j)`, and `P.orderEmbOfFin` is the increasing bijection onto `P`, so its determinant is precisely the principal minor indexed by P. The second declaration sums over `k \u2208 Finset.range (n + 1)` and filters all P by `P.card = n - k`, exactly representing `k=0,...,n` and `|P|=n-k`. Scalar multiplication `x \u2022 (1 : Matrix ...)` is the pointwise matrix scalar action on the identity, hence `x I_n`. Q2: yes. The informal displayed chain gives each of the two formal equalities separately after the standard encodings `K \u21a6 R`, `[n] \u21a6 Fin n`, and subsets `P \u21a6 Finset (Fin n)`. Conversely, the two Lean declarations share the same left-hand side, so together they give the full informal equality chain. There are no extra mathematical hypotheses, restricted ranges, or altered definitions."
}
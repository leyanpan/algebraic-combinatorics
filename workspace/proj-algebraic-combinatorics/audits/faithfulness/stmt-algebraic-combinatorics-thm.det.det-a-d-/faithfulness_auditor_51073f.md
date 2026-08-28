Declaration: AlgebraicCombinatorics.CauchyBinet.det_add_diagonal
Module: AlgebraicCombinatorics.CauchyBinet

Statement id: stmt-algebraic-combinatorics-thm.det.det-a-d-

## INFORMAL STATEMENT
thm.det.det(A+D)

Let $n\in \mathbb {N}$. Let $A$ and $D$ be two $n\times n$-matrices in $K^{n\times n}$ such that the matrix $D$ is diagonal. Let $d_1,d_2,\ldots ,d_n$ be the diagonal entries of the diagonal matrix $D$. Then, 

\[  \det (A+D) = \sum _{P\subseteq [n]} \det (\operatorname {sub}_P^P A) \cdot \prod _{i\in [n]\setminus P} d_i.  \]

 The minors $\det (\operatorname {sub}_P^P A)$ are called the \emph{principal minors} of $A$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: yes. The elaborated signature is `\u2200 {R : Type u} [CommRing R] {n : \u2115} (A : Matrix (Fin n) (Fin n) R) (d : Fin n \u2192 R), (A + Matrix.diagonal d).det = \u2211 P, (A.submatrix (P.orderEmbOfFin ...) (P.orderEmbOfFin ...)).det * \u220f i \u2208 P\u1d9c, d i`. This matches the informal formula `det (A+D) = \u2211_{P\u2286[n]} det (sub_P^P A) \u00b7 \u220f_{i\u2208[n]\\P} d_i`: finsets of `Fin n` represent all subsets of `[n]`, `P\u1d9c` is the complement in the full finite index set, and `P.orderEmbOfFin` enumerates P in increasing order, exactly as the source definition of `sub` requires. Mathlib documents `Matrix.diagonal d` as having entry `d i` on the diagonal and zero when the indices differ, matching the source's explicit `D = (d_i [i=j])`. The implicit `[CommRing R]` is not drift: the governing source convention says, `For the rest of Section ... we fix a commutative ring K`, while the Lean declaration generalizes uniformly over that fixed arbitrary ring. Q2: yes. Given the informal diagonal matrix D and its diagonal entries, the source explicitly says `so that D = (d_i [i=j])`; hence D is exactly `Matrix.diagonal d`, and the Lean equality is the informal equality after the standard identification of the source's one-based `[n]` with `Fin n`. Conversely, every `Matrix.diagonal d` is a diagonal D with those entries, so the Lean parameterization does not narrow the informal quantification. The final sentence calling these determinants 'principal minors' is explanatory terminology rather than an additional propositional claim; the project also defines `principalMinor` using this same principal submatrix determinant."
}
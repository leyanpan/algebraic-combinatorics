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
  "justification": "The elaborated signature is `\u2200 {R : Type u} [CommRing R] {n : \u2115} (A : Matrix (Fin n) (Fin n) R) (d : Fin n \u2192 R), (A + Matrix.diagonal d).det = \u2211 P, (A.submatrix (P.orderEmbOfFin ...) (P.orderEmbOfFin ...)).det * \u220f i \u2208 P\u1d9c, d i`. This directly matches the blueprint's `Let n\u2208\u2115`, matrices over `K`, and formula `det(A+D) = \u2211_{P\u2286[n]} det(sub_P^P A) \u00b7 \u220f_{i\u2208[n]\\setminus P} d_i`. The blueprint definition of the coefficient type makes `K` a commutative ring, exactly matching `[CommRing R]`; no stronger algebraic hypothesis is added. Mathlib's `Matrix.diagonal d` is explicitly the matrix with diagonal entries `d i` and zero off the diagonal, so replacing the blueprint's diagonal matrix `D` and its listed entries by the parameter `d : Fin n \u2192 R` is an equivalent parametrization of all diagonal matrices, not a restriction. The blueprint definition `def.det.sub` says that `sub_U^V A` selects the rows and columns in increasing order; its project formalization has body `A.submatrix (U.orderEmbOfFin rfl) (V.orderEmbOfFin rfl)`. Thus the target's two identical `P.orderEmbOfFin` arguments denote exactly the principal submatrix `sub_P^P A`. Finally, `P : Finset (Fin n)` ranges over all subsets of `[n]`, and `P\u1d9c` is its complement in `Fin n`, so `\u220f i \u2208 P\u1d9c, d i` is precisely the blueprint product over `[n] \\ P`. The use of zero-based `Fin n` rather than the blueprint's one-based labels is only a consistent relabeling of rows, columns, subsets, and diagonal entries."
}
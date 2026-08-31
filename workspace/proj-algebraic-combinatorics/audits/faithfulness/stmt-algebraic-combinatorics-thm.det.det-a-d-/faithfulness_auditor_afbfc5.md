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
  "justification": "The elaborated signature is `{R : Type u} [CommRing R] {n : \u2115} (A : Matrix (Fin n) (Fin n) R) (d : Fin n \u2192 R)`, matching the blueprint's \u201cLet n \u2208 \u2115\u201d and matrices over the commutative coefficient ring K. The blueprint quantifies a diagonal matrix D with diagonal entries `d_i`; Lean writes that matrix canonically as `Matrix.diagonal d`. Its definition states that `(diagonal d) i i = d i` and `(diagonal d) i j = 0` for `i \u2260 j`, so this parametrizes precisely the diagonal matrices and does not narrow the quantifier over D. The formal conclusion `(A + Matrix.diagonal d).det = \u2211 P : Finset (Fin n), ((A.submatrix (P.orderEmbOfFin rfl) (P.orderEmbOfFin rfl)).det) * \u220f i \u2208 P\u1d9c, d i` matches the blueprint's `det(A+D) = \u2211_{P\u2286[n]} det(sub_P^P A) \u00b7 \u220f_{i\u2208[n]\\P} d_i`: `Finset (Fin n)` ranges over all subsets of `[n]`, `P\u1d9c` is the complement in `[n]`, and the two `P.orderEmbOfFin` maps select the P-indexed rows and columns in increasing order, exactly as the blueprint definition of `sub_P^P` requires. Thus the determinant factors are precisely the principal minors described informally, with no added hypothesis or restricted range."
}
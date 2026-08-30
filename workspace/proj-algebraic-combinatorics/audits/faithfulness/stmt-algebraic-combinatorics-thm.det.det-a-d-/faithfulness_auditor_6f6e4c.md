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
  "justification": "The elaborated signature is `\u2200 {R : Type u} [CommRing R] {n : \u2115} (A : Matrix (Fin n) (Fin n) R) (d : Fin n \u2192 R), (A + Matrix.diagonal d).det = \u2211 P, (A.submatrix (P.orderEmbOfFin ...) (P.orderEmbOfFin ...)).det * \u220f i \u2208 P\u1d9c, d i`. This matches the blueprint binders \u201cLet n\u2208\u2115\u201d and \u201cA and D ... in K^{n\u00d7n} such that D is diagonal,\u201d with `R` representing the blueprint's commutative ring `K`, `Fin n` representing `[n]`, and `d : Fin n \u2192 R` representing its diagonal entries. Binding `d` and using `D = Matrix.diagonal d` is equivalent to binding an arbitrary diagonal `D`: Mathlib defines `Matrix.diagonal d i j = if i = j then d i else 0`, so its diagonal entries are exactly `d i`; conversely, any matrix diagonal in the stated sense equals `Matrix.diagonal (fun i => D i i)` by entrywise extensionality. The conclusion directly matches \u201cdet(A+D) = \u2211_{P\u2286[n]} det(sub_P^P A) \u00b7 \u220f_{i\u2208[n]\\P} d_i\u201d: `P : Finset (Fin n)` ranges over every subset of `[n]`, `P\u1d9c` is its complement, and the project definition `submatrixOfFinset A U V := A.submatrix (U.orderEmbOfFin ...) (V.orderEmbOfFin ...)` confirms that the displayed Lean submatrix is precisely the blueprint's naturally ordered `sub_P^P A`. There are no additional mathematical hypotheses or narrowed ranges."
}
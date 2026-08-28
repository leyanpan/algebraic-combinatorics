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
  "justification": "Q1: Yes. The elaborated signature is `{R : Type} [CommRing R] {n : \u2115} (A : Matrix (Fin n) (Fin n) R) (d : Fin n \u2192 R)`, with conclusion `(A + Matrix.diagonal d).det = \u2211 P : Finset (Fin n), (A.submatrix (P.orderEmbOfFin rfl) (P.orderEmbOfFin rfl)).det * \u220f i \u2208 P\u1d9c, d i`. This directly matches the informal formula `det(A+D) = \u2211_{P\u2286[n]} det(sub_P^P A) \u00b7 \u220f_{i\u2208[n]\\P} d_i`: `Matrix.diagonal d` is documented as having entry `d i` on the diagonal and `0` off it, `Finset (Fin n)` ranges over all subsets, `P\u1d9c` is the complement in the full finite index type, and the two identical increasing embeddings select the principal submatrix. Although the displayed informal statement does not restate the structure on `K`, its section context explicitly says, `We work over a commutative ring K`, exactly matching `[CommRing R]`. Q2: Yes. Given an informal diagonal matrix `D` with diagonal entries `d_i`, extensionality identifies it with `Matrix.diagonal d`, so the informal theorem specializes to precisely the Lean equality. Conversely, every `d : Fin n \u2192 R` defines such a diagonal matrix, so Lean does not restrict the informal quantification. The shift from informal one-based `[n]` to Lean's zero-based `Fin n` is only an indexing equivalence; the project context explicitly notes, `in the Lean formalization, indexing is 0-based`, and the increasing embeddings preserve the corresponding principal minors. Thus neither direction introduces an additional hypothesis or omits any case."
}
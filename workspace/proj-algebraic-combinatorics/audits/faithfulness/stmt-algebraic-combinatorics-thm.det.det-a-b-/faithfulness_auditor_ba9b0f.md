Declaration: AlgebraicCombinatorics.CauchyBinet.det_add_sum
Module: AlgebraicCombinatorics.CauchyBinet

Statement id: stmt-algebraic-combinatorics-thm.det.det-a-b-

## INFORMAL STATEMENT
thm.det.det(A+B)

Let $n\in \mathbb {N}$. For any subset $I$ of $[n]$, let $\widetilde{I} = [n]\setminus I$ denote its complement. 

Let $A$ and $B$ be two $n\times n$-matrices in $K^{n\times n}$. Then, 

\[  \det (A+B) = \sum _{P\subseteq [n]}\; \;  \sum _{\substack {Q\subseteq [n];\\ |P|=|Q|}} (-1)^{\operatorname {sum} P + \operatorname {sum} Q} \det (\operatorname {sub}_P^Q A) \cdot \det (\operatorname {sub}_{\widetilde{P}}^{\widetilde{Q}} B).  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: yes. Q2: yes. The elaborated declaration universally binds `{R : Type*} [CommRing R] {n : \u2115}` and `(A B : Matrix (Fin n) (Fin n) R)`, faithfully encoding the source's fixed commutative coefficient ring K and two n\u00d7n matrices. Its outer sums `\u2211 P : Finset (Fin n), \u2211 Q : Finset (Fin n)` range over all subsets, while `if h : Q.card = P.card then ... else 0` is equivalent to the source's constrained inner sum `Q \u2286 [n]; |P|=|Q|`. `Finset` complement `P\u1d9c` is relative to the finite universe `Fin n`, matching `\\widetilde{P}=[n]\\setminus P`. The sign is also equivalent: `finsetSumFin P` is defined as `\u2211 i \u2208 P, i.val`; translating the source's 1-based indices to `Fin n` subtracts `P.card + Q.card = 2 * P.card` from the exponent when the cardinalities agree, so `(-1)` is unchanged. There is an apparent argument reversal in the formal summands: the source has `det(sub_P^Q A) \u00b7 det(sub_\u1e54^Q\u0303 B)`, whereas Lean has `submatrixDet A Q P h * submatrixDet B Q\u1d9c P\u1d9c ...`, and `submatrixDet A U V h` is definitionally the determinant of `A.submatrix (U.orderEmbOfFin ...) (V.orderEmbOfFin ...)`, with U selecting rows and V selecting columns. Nevertheless, both P and Q are bound over all subsets, the cardinality condition and sign are symmetric in P and Q, and simultaneously exchanging the dummy variables P and Q converts the entire Lean double sum exactly into the informal double sum. Thus the reversal changes no asserted equality, and the two statements imply one another."
}
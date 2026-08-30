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
  "justification": "The elaborated binders are `{R : Type u} [CommRing R] {n : \u2115} (A B : Matrix (Fin n) (Fin n) R)`, matching the blueprint's \u201cLet n \u2208 \u2115\u201d and \u201cA and B be two n\u00d7n-matrices in K^{n\u00d7n}\u201d; the definition node for K specifies a commutative ring, so `[CommRing R]` is not an added hypothesis. The conclusion quantifies over all `P Q : Finset (Fin n)` and restricts the terms by `if h : Q.card = P.card`, exactly encoding \u201cP \u2286 [n]\u201d and \u201cQ \u2286 [n]; |P|=|Q|\u201d; `P\u1d9c` and `Q\u1d9c` are complements in the finite universe. The definition `finsetSumFin P := \u2211 i \u2208 P, i.val` uses zero-based `Fin n` indices rather than the blueprint's `[n]={1,\u2026,n}`, but for `|P|=|Q|` the two exponents differ by `|P|+|Q|=2|P|`, so `(-1)^(sum P + sum Q)` is unchanged. The formal summand is `(-1 : R) ^ (finsetSumFin P + finsetSumFin Q) * submatrixDet A Q P h * submatrixDet B Q\u1d9c P\u1d9c ...`. Its referenced definition says `submatrixDet A U V h := det (A.submatrix (U.orderEmbOfFin ...) (V.orderEmbOfFin ...))`, with the first set selecting rows and the second columns. Thus its displayed arguments are reversed relative to the blueprint definition of `sub_P^Q A` as rows P and columns Q. This does not change the double sum: simultaneously exchanging the dummy variables P and Q bijectively reindexes all equal-cardinality pairs and turns the formal factors into the blueprint factors `det(sub_P^Q A) \u00b7 det(sub_{P\u0303}^{Q\u0303} B)`, while leaving the symmetric sign exponent unchanged. Therefore the formal equality specializes to, and is equivalent to, the stated determinant formula."
}
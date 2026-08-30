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
  "justification": "The elaborated signature quantifies exactly over the required setting: `{R : Type u} [CommRing R] {n : \u2115} (A B : Matrix (Fin n) (Fin n) R)`. This answers the blueprint's \u201cLet n \u2208 \u2115\u201d and \u201cA and B [are] two n\u00d7n-matrices in K^{n\u00d7n}\u201d; the blueprint definition of K fixes K as a commutative ring, so `[CommRing R]` is not an added hypothesis. The formal conclusion is `(A + B).det = \u2211 P, \u2211 Q, if h : #Q = #P then ... else 0`, which is equivalent to the blueprint's `\u2211_{P\u2286[n]} \u2211_{Q\u2286[n]; |P|=|Q|}`: `Finset (Fin n)` ranges over all subsets, and the dependent conditional contributes zero precisely when the cardinalities differ. The referenced definition is `submatrixDet A P Q h := (A.submatrix (P.orderEmbOfFin rfl) (Q.orderEmbOfFin ...)).det`, so its first set selects rows and its second selects columns, agreeing with the blueprint definition of `sub_U^V A`. The displayed formal summand uses `submatrixDet A Q P h * submatrixDet B Q\u1d9c P\u1d9c ...`, apparently reversing the blueprint's `det(sub_P^Q A) * det(sub_{P\u0303}^{Q\u0303} B)`. However, both P and Q are dummy variables ranging independently over all subsets under the symmetric condition `|P|=|Q|`; exchanging P and Q in the entire double sum changes these factors to exactly the blueprint's row/column order, while leaving `finsetSumFin P + finsetSumFin Q` and the cardinality condition unchanged. Finally, Lean represents `[n]` by zero-based `Fin n`, whereas the blueprint uses `{1,...,n}`. Under the order-preserving identification, each subset sum gains its cardinality; because `|P|=|Q|`, the total exponent gains `|P|+|Q|=2|P|`, so `(-1)^(sum P + sum Q)` is unchanged. Complements `P\u1d9c` and `Q\u1d9c` are taken inside `Fin n`, exactly corresponding to `[n]\\P` and `[n]\\Q`."
}
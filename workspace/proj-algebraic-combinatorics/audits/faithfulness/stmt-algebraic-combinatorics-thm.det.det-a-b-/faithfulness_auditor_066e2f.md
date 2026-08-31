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
  "justification": "The elaborated signature binds exactly the intended setting: `{R : Type u} [CommRing R] {n : \u2115} (A B : Matrix (Fin n) (Fin n) R)`, matching the blueprint's \u201cLet n\u2208\u2115\u201d and \u201cA and B ... in K^{n\u00d7n}\u201d; the blueprint definition node for K fixes K as a commutative ring. The conclusion is `(A + B).det = \u2211 P : Finset (Fin n), \u2211 Q : Finset (Fin n), if h : Q.card = P.card then ... else 0`, which is the finite-sum encoding of \u201c\u2211_{P\u2286[n]} \u2211_{Q\u2286[n]; |P|=|Q|}`: unequal-cardinality terms are zero. The referenced definition is `submatrixDet A P Q h := (A.submatrix (P.orderEmbOfFin rfl) (Q.orderEmbOfFin ...)).det`, so its first set selects rows and its second selects columns, exactly as the blueprint definition `sub_U^V A` specifies. The formal summand uses `submatrixDet A Q P h * submatrixDet B Q\u1d9c P\u1d9c ...`, apparently reversing P and Q relative to the displayed blueprint summand `det(sub_P^Q A) \u00b7 det(sub_{P\u0303}^{Q\u0303} B)`. This does not change the whole statement: P and Q are dummy variables ranging independently over all subsets, the condition `Q.card = P.card` and exponent `finsetSumFin P + finsetSumFin Q` are symmetric, and reindexing the double sum by `(P,Q) \u21a6 (Q,P)` yields exactly the blueprint's row/column order and complements. Finally, `finsetSumFin P := \u2211 i\u2208P, i.val` uses the zero-based realization `Fin n`, whereas the blueprint has `[n]={1,\u2026,n}`. Under the canonical shift, the two exponent sums differ by `|P|+|Q|=2|P|`, so the factor `(-1)^(sum P + sum Q)` is unchanged. Thus the formal and blueprint equalities are equivalent."
}
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
  "justification": "Q1: yes. Q2: yes. The elaborated signature quantifies `{R : Type} [CommRing R] {n : \u2115}` and `A B : Matrix (Fin n) (Fin n) R`, matching the source context, which states, \u201cWe work over a commutative ring K,\u201d and the target\u2019s \u201ctwo n\u00d7n-matrices in K^{n\u00d7n}.\u201d The formal right-hand side is `\u2211 P, \u2211 Q, if h : Q.card = P.card then (-1 : R) ^ (finsetSumFin P + finsetSumFin Q) * submatrixDet A Q P h * submatrixDet B Q\u1d9c P\u1d9c ... else 0`; the conditional zero terms are exactly equivalent to the informal restriction `|P|=|Q|`. The referenced definitions are `finsetSumFin P := \u2211 i \u2208 P, i.val` and `submatrixDet A P Q h := (A.submatrix (P.orderEmbOfFin rfl) (Q.orderEmbOfFin ...)).det`, so the latter selects rows P and columns Q. Thus the displayed formal summand appears to reverse the informal `sub_P^Q` arguments, using rows Q and columns P. However, exchanging the two dummy variables P and Q throughout the unrestricted double sum converts it exactly into `det(sub_P^Q A) * det(sub_{P\u1d9c}^{Q\u1d9c} B)`; the cardinality condition and exponent are symmetric in P and Q. Finally, Lean uses zero-based `Fin n` while the source uses `[n]={1,...,n}`. Under the canonical shift, each subset sum gains its cardinality, so for `|P|=|Q|` the total exponent gains `|P|+|Q|=2|P|`; therefore the power of `-1` is unchanged. Complements and order-preserving submatrices correspond under the same shift. Hence the two formulas are equivalent in both directions."
}
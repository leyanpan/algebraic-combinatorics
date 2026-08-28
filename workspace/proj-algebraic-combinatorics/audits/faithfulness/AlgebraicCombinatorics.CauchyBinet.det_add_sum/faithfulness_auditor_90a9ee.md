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
  "justification": "Q1: yes. Q2: yes. The elaborated signature quantifies over `{R : Type u} [CommRing R]`, `{n : \u2115}`, and `A B : Matrix (Fin n) (Fin n) R`, matching the determinant chapter's ambient commutative ring K and arbitrary n\u00d7n matrices. The informal restricted inner sum, \u201c`Q \u2286 [n]; |P|=|Q|`,\u201d is represented exactly by the formal sum over every Q followed by `if h : Q.card = P.card then ... else 0`. The definitions also have the intended meanings: `finsetSumFin P := \u2211 i \u2208 P, i.val`, and `submatrixDet A P Q h := (A.submatrix (P.orderEmbOfFin rfl) (Q.orderEmbOfFin (h \u25b8 rfl))).det`, so its first subset selects rows and its second selects columns. Although the formal summand is written `submatrixDet A Q P h * submatrixDet B Q\u1d9c P\u1d9c ...`, while the informal summand is `det(sub_P^Q A) \u00b7 det(sub_P\u0303^Q\u0303 B)`, the two complete double sums coincide by globally exchanging the dummy variables P and Q; the cardinality condition and exponent `finsetSumFin P + finsetSumFin Q` are symmetric under that exchange. The use of `Fin n` gives zero-based representatives rather than the informal one-based `[n]`, but shifting every selected index by one changes the exponent by `P.card + Q.card = 2 * P.card` on the cardinality-restricted terms, so the factor `(-1)^(sum P + sum Q)` is unchanged. Complements and increasing-order submatrices likewise correspond under this identification. Thus the Lean equality and the informal equality are equivalent in both directions."
}
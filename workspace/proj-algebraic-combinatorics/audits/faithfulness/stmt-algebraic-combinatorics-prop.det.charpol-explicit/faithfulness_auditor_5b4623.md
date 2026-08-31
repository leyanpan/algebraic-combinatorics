Declaration: AlgebraicCombinatorics.CauchyBinet.det_charPoly_coeff', AlgebraicCombinatorics.CauchyBinet.det_charPoly_coeff
Module: AlgebraicCombinatorics.CauchyBinet

Statement id: stmt-algebraic-combinatorics-prop.det.charpol-explicit

## INFORMAL STATEMENT
prop.det.charpol-explicit

Let $n\in \mathbb {N}$. Let $A\in K^{n\times n}$ be an $n\times n$-matrix. Let $x\in K$. Let $I_n$ denote the $n\times n$ identity matrix. Then, 

\[  \det (A + x I_n) = \sum _{P\subseteq [n]} \det (\operatorname {sub}_P^P A) \cdot x^{n-|P|} = \sum _{k=0}^{n} \biggl(\sum _{\substack {P\subseteq [n];\\ |P|=n-k}} \det (\operatorname {sub}_P^P A)\biggr) x^k.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signatures quantify over `{R : Type u} [CommRing R] {n : \u2115}`, `(A : Matrix (Fin n) (Fin n) R)`, and `(x : R)`. This matches the blueprint\u2019s \u201cLet n\u2208\u2115. Let A\u2208K^{n\u00d7n} ... Let x\u2208K\u201d; the blueprint definition node for `K` makes it a commutative ring, so `[CommRing R]` is not an added hypothesis. The first declaration concludes `(A + x \u2022 1).det = \u2211 P, (A.submatrix (P.orderEmbOfFin ...) (P.orderEmbOfFin ...)).det * x ^ (n - P.card)`, exactly answering \u201cdet(A+xI_n)=\u2211_{P\u2286[n]} det(sub_P^P A)\u00b7x^{n-|P|}.\u201d Here `P : Finset (Fin n)` ranges over every subset of `[n]`; `Matrix.submatrix` has entries `A (r i) (c j)`, and the increasing embeddings `P.orderEmbOfFin` implement the natural ordering required by the blueprint\u2019s `sub` definition. The matrix `x \u2022 1` is the scalar multiple of the identity matrix, hence `xI_n`. The second declaration concludes `(A + x \u2022 1).det = \u2211 k \u2208 Finset.range (n + 1), (\u2211 P \u2208 univ.filter (fun P => P.card = n - k), (A.submatrix ... ...).det) * x ^ k`, exactly answering the grouped expression \u201c\u2211_{k=0}^{n}(\u2211_{P\u2286[n]; |P|=n-k} det(sub_P^P A))x^k\u201d: `range (n+1)` is precisely `0,\u2026,n`, and the filter imposes `P.card = n-k`. Taken together, the two declarations establish both equalities in the blueprint\u2019s chained equation, with no narrowed quantifiers or additional mathematical assumptions."
}
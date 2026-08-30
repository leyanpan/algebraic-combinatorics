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
  "justification": "The hidden formal setting is `{R : Type u} [CommRing R]`, matching the blueprint's coefficient set K as a commutative ring. The elaborated binders `{n : \u2115} (A : Matrix (Fin n) (Fin n) R) (x : R)` exactly answer the informal binders \u201cLet n\u2208\u2115. Let A\u2208K^{n\u00d7n} ... Let x\u2208K.\u201d In `det_charPoly_coeff`, the conclusion `(A + x \u2022 1).det = \u2211 P, (A.submatrix (P.orderEmbOfFin ...) (P.orderEmbOfFin ...)).det * x ^ (n - P.card)` matches \u201cdet(A + x I_n) = \u2211_{P\u2286[n]} det(sub_P^P A) \u00b7 x^{n-|P|}`: `Finset (Fin n)` represents subsets of `[n]`, `x \u2022 1` is the scalar multiple of the identity matrix, and both submatrix embeddings enumerate P in its natural order, as required by the blueprint definition `def.det.sub`. In `det_charPoly_coeff'`, the conclusion uses `\u2211 k \u2208 range (n + 1)`, exactly k from 0 through n, and the inner sum is filtered by `P.card = n - k`, matching \u201c\u2211_{k=0}^{n} (\u2211_{P\u2286[n]; |P|=n-k} det(sub_P^P A)) x^k.\u201d Thus the two declarations jointly give the two equalities in the informal chained equation, with no added mathematical hypothesis or narrowed quantifier."
}
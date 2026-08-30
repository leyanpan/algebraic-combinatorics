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
  "justification": "Taken together, the two declarations state exactly the two equalities in the blueprint chain. Their elaborated binders are `{R : Type u} [CommRing R] {n : \u2115} (A : Matrix (Fin n) (Fin n) R) (x : R)`, matching \u201cLet n\u2208\u2115. Let A\u2208K^{n\u00d7n} ... Let x\u2208K\u201d in the blueprint\u2019s commutative-ring setting, with no additional hypothesis. `det_charPoly_coeff` concludes `(A + x \u2022 1).det = \u2211 P, (A.submatrix (P.orderEmbOfFin rfl) (P.orderEmbOfFin rfl)).det * x^(n-P.card)`, which answers the first displayed equality `det(A+xI_n)=\u2211_{P\u2286[n]} det(sub_P^P A)\u00b7x^{n-|P|}`: `P : Finset (Fin n)` ranges over all subsets, and the blueprint definition `submatrixOfFinset A U V := A.submatrix (U.orderEmbOfFin rfl) (V.orderEmbOfFin rfl)` makes the principal submatrix expression definitionally the intended `sub_P^P A`. The matrix `x \u2022 1` is the scalar multiple of the identity matrix, hence `xI_n`. `det_charPoly_coeff'` concludes `(A + x \u2022 1).det = \u2211 k \u2208 range (n+1), (\u2211 P with P.card = n-k, (A.submatrix ... ...).det) * x^k`, exactly matching the second equality `\u2211_{k=0}^n (\u2211_{P\u2286[n]; |P|=n-k} det(sub_P^P A))x^k`, since `range (n+1)` is precisely `0,\u2026,n`. Because both declarations have the same universally quantified parameters and left-hand side, together they also imply equality of the two right-hand sums, and conversely the blueprint chain supplies each declaration."
}
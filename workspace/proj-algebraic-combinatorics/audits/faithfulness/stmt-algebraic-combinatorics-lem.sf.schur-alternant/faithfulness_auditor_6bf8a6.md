Declaration: AlgebraicCombinatorics.schurPoly_eq_alternant_div
Module: AlgebraicCombinatorics.SymmetricFunctions.LittlewoodRichardson

Statement id: stmt-algebraic-combinatorics-lem.sf.schur-alternant

## INFORMAL STATEMENT
Schur–alternant relation

\leanhelper  Let $\lambda $ be an $N$-partition. Then, 

\[  a_{\lambda + \rho } = a_{\rho } \cdot s_{\lambda }.  \]

 (This is Theorem~ \ref{thm.sf.schur-symm}~ \textbf{(b)}.)

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signature is `\u2200 {R : Type u} [CommRing R] {N : \u2115} (lam : Fin N \u2192 \u2115), IsNPartition lam \u2192 alternant (lam + rho N) = alternant (rho N) * schurPoly lam`, directly matching the blueprint\u2019s \u201cLet \u03bb be an N-partition\u201d and `a_{\u03bb+\u03c1} = a_\u03c1 \u00b7 s_\u03bb`. The hypothesis introduces no drift: `IsNPartition lam` unfolds to `\u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`, exactly the blueprint definition of a weakly decreasing N-tuple of nonnegative integers. Tuple addition is the pointwise `Pi` addition, matching the blueprint\u2019s entrywise addition, and `rho N i` is `N - 1 - i.val`, representing `(N-1,N-2,\u2026,0)`. The referenced `alternant` is `\u2211 \u03c3, sign \u03c3 \u2022 xPow (\u03b1 \u2218 \u03c3)`, and the proved characterization `alternant_eq_det` identifies it with the determinant of the matrix having entry `x_j^(\u03b1_i)`; that matrix is the transpose of the blueprint matrix `(x_i^(\u03b1_j))`, so its determinant is the same `a_\u03b1`. Finally, `schurPoly lam` unfolds to the sum of `xPow (contentTableau T)` over semistandard tableaux of shape `lam/0`, exactly the blueprint definition `s_\u03bb := \u2211_{T\u2208SSYT(\u03bb)} x_T`; the project also proves its equality over \u2124 with the canonical Schur definition. The hidden `[CommRing R]` is the coefficient-ring setting already carried by the blueprint\u2019s `P = K[x\u2081,\u2026,x_N]`, not an added mathematical hypothesis. Quantifying over every commutative ring, and also permitting the vacuous `N = 0` case, only makes the Lean theorem more general."
}
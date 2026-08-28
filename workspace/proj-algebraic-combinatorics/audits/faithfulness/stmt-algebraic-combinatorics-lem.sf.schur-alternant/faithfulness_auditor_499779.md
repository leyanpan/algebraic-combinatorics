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
  "justification": "Q1: yes. Q2: yes. The informal claim is exactly \"Let \u03bb be an N-partition\" and \"a_{\u03bb+\u03c1} = a_\u03c1 \u00b7 s_\u03bb\". The elaborated Lean signature is `{R : Type u} [CommRing R] {N : \u2115} (lam : Fin N \u2192 \u2115) (hlam : IsNPartition lam) : alternant (lam + rho N) = alternant (rho N) * schurPoly lam`. Its implicit ring and dimension binders match the source convention \"Fix a commutative ring K. Fix an N \u2208 \u2115\"; they are not added restrictions. `IsNPartition lam` is defined as `\u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`, exactly a weakly decreasing N-tuple of natural numbers. Addition on `Fin N \u2192 \u2115` is pointwise, matching the source's \"addition on \u2115^N is defined entrywise\", and `rho N` has body `fun i => N - 1 - i.val`, representing `(N-1,N-2,...,0)`. The referenced definitions also agree with the informal notation: `alternant \u03b1` is `\u2211 \u03c3, sign \u03c3 \u2022 xPow (\u03b1 \u2218 \u03c3)` and `alternant_eq_det` identifies it with the source determinant `det((x_i^{\u03b1_j}))` (the formal matrix is its transpose, which has the same determinant); `schurPoly lam` is the sum of `xPow (contentTableau T)` over semistandard tableaux of shape `lam/0`, matching `s_\u03bb := \u2211_{T\u2208SSYT(\u03bb)} x_T`. Thus neither direction introduces or omits a mathematical hypothesis, and both statements assert the same polynomial identity over the same arbitrary commutative-ring setting."
}
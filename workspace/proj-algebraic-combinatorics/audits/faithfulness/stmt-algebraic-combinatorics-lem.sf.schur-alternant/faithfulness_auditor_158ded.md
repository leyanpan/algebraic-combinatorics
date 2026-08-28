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
  "justification": "Q1: yes. Q2: yes. The informal claim is exactly \u201cLet \u03bb be an N-partition\u201d and \u201ca_{\u03bb+\u03c1} = a_\u03c1 \u00b7 s_\u03bb.\u201d The elaborated signature is `{R : Type} [CommRing R] {N : \u2115} (lam : Fin N \u2192 \u2115) (hlam : IsNPartition lam) : alternant (lam + rho N) = alternant (rho N) * schurPoly lam`. Its implicit parameters match the source\u2019s ambient convention: \u201cFix a commutative ring K. Fix an N \u2208 \u2115.\u201d The partition hypothesis also matches exactly: the source defines an N-partition as \u201ca weakly decreasing N-tuple of nonnegative integers,\u201d while `IsNPartition lam` unfolds to `\u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`. The referenced definitions preserve the intended objects: `rho N i := N - 1 - i.val` represents the source\u2019s `(N-1, N-2, \u2026, 0)`; tuple addition is pointwise; `alternant \u03b1` is proved equal to the determinant with entries `x_j ^ \u03b1_i`, whose transpose is the source determinant `(x_i ^ \u03b1_j)`; and `schurPoly lam := skewSchurPoly lam 0`, where `skewSchurPoly` is the sum of `xPow (contentTableau T)` over semistandard tableaux, matching the source definition `s_\u03bb := \u2211_{T \u2208 SSYT(\u03bb)} x_T`. The use of zero-based `Fin N` indices is only an encoding of the source\u2019s one-based indices. There is no added mathematical hypothesis or narrowed quantifier: both the source and Lean allow arbitrary natural `N`, including zero, and an arbitrary commutative coefficient ring."
}
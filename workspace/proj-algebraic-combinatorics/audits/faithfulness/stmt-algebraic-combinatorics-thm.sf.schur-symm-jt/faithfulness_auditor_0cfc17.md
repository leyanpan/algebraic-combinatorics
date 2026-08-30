Declaration: SymmetricFunctions.schur_isSymmetric_jacobiTrudi
Module: AlgebraicCombinatorics.SymmetricFunctions.PieriJacobiTrudi

Statement id: stmt-algebraic-combinatorics-thm.sf.schur-symm-jt

## INFORMAL STATEMENT
thm.sf.schur-symm-jt

\leanhelper  Schur polynomials are symmetric: for any partition $\lambda $, $s_\lambda $ is a symmetric polynomial. 

This is a corollary of Theorem~ \ref{thm.sf.skew-schur-symm-jt} with $\mu = 0$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The informal claim is: \u201cfor any partition \u03bb, s_\u03bb is a symmetric polynomial.\u201d The elaborated Lean signature is `\u2200 {N : \u2115} {R : Type} [CommRing R] (lam : Fin N \u2192 \u2115) (hlam : \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i), (schur \u27e8lam, hlam\u27e9).IsSymmetric`. The binder `hlam` is not an added mathematical restriction: together with `lam : Fin N \u2192 \u2115`, it is exactly the blueprint definition of an N-partition as a \u201cweakly decreasing N-tuple of nonnegative integers.\u201d The referenced `SymmetricFunctions.schur` has body `\u2211 T \u2208 ssytFinset lam, T.toMonomial`, matching the blueprint definition `s_\u03bb := \u2211_{T \u2208 SSYT(\u03bb)} x_T`. Finally, `MvPolynomial.IsSymmetric` elaborates to `\u2200 e : Equiv.Perm (Fin N), rename e \u03c6 = \u03c6`, exactly the blueprint condition that every permutation of the variables fixes the polynomial. The implicit `[CommRing R]` is the formal polynomial-ring setting already fixed by the blueprint definition of `P = K[x\u2081,\u2026,x_N]`, not an added hypothesis. Lean is slightly more general than the original integer-coefficient Schur definition because it proves the result over every commutative ring, and it also allows `N = 0`; specializing to the blueprint setting gives the stated theorem."
}
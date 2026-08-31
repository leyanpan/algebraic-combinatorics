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
  "justification": "The elaborated signature is `{N : \u2115} {R : Type u} [CommRing R] (lam : Fin N \u2192 \u2115) (hlam : \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i) : (schur \u27e8lam, hlam\u27e9).IsSymmetric`. This directly answers the blueprint\u2019s \u201cfor any partition \u03bb, s_\u03bb is a symmetric polynomial.\u201d The binder `hlam` is not an added mathematical hypothesis: the blueprint definition says an N-partition is \u201ca weakly decreasing N-tuple of nonnegative integers,\u201d and the local `NPartition` structure has exactly `parts : Fin N \u2192 \u2115` and `weaklyDecreasing : \u2200 i j, i \u2264 j \u2192 parts j \u2264 parts i`; thus `(lam, hlam)` ranges over precisely all N-partitions. The referenced definition is `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial`, matching the blueprint definition `s_\u03bb = \u2211_{T \u2208 SSYT(\u03bb)} x_T`; `ssytFinset` contains all tableaux with entries in `Fin N`, weakly increasing rows, and strictly increasing columns. Finally, Mathlib\u2019s `MvPolynomial.IsSymmetric` means invariance under every permutation of the variables by `rename`, exactly matching the blueprint definition of \u201csymmetric.\u201d The implicit `[CommRing R]` supplies the polynomial coefficient setting rather than restricting \u03bb, and permits the same commutative-ring setting used by the project\u2019s polynomial-ring definition."
}
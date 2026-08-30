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
  "justification": "The informal statement says, \"for any partition \u03bb, s_\u03bb is a symmetric polynomial.\" The elaborated declaration quantifies `\u2200 {N : \u2115} {R : Type u} [CommRing R] (lam : Fin N \u2192 \u2115) (hlam : \u2200 (i j : Fin N), i \u2264 j \u2192 lam j \u2264 lam i)` and concludes `(SymmetricFunctions.schur { parts := lam, weaklyDecreasing := hlam }).IsSymmetric`. The `hlam` binder is not an additional mathematical hypothesis: `SymmetricFunctions.NPartition N` is the structure with fields `parts : Fin N \u2192 \u2115` and `weaklyDecreasing : \u2200 i j, i \u2264 j \u2192 parts j \u2264 parts i`, exactly implementing the blueprint definition of an N-partition as a weakly decreasing N-tuple of nonnegative integers. Thus the two explicit binders merely unpack an arbitrary N-partition. The referenced definition is `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial`, matching the blueprint definition `s_\u03bb = \u2211_{T \u2208 SSYT(\u03bb)} x_T`. Finally, Mathlib defines `MvPolynomial.IsSymmetric \u03c6 := \u2200 (e : Equiv.Perm \u03c3), rename e \u03c6 = \u03c6`; the project's blueprint-facing `IsSymm` is definitionally `f.IsSymmetric`, and its permutation action is `permAction \u03c3 f := rename \u03c3 f`. Hence the conclusion is exactly invariance under every permutation of the N variables. The implicit `CommRing R` binder is inherited from the project's Schur-polynomial and polynomial-ring setting rather than narrowing the partitions quantified by the theorem."
}
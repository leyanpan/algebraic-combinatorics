Declaration: SymmetricFunctions.skewSchur_isSymmetric_jacobiTrudi
Module: AlgebraicCombinatorics.SymmetricFunctions.PieriJacobiTrudi

Statement id: stmt-algebraic-combinatorics-thm.sf.skew-schur-symm-jt

## INFORMAL STATEMENT
thm.sf.skew-schur-symm-jt

\leanhelper  Skew Schur polynomials are symmetric: for any partitions $\lambda \supseteq \mu $, $s_{\lambda /\mu }$ is a symmetric polynomial. 

This provides a proof of symmetry via the Jacobi–Trudi formula, without relying on the Bender–Knuth involution.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifies over \u201cany partitions \u03bb \u2287 \u03bc\u201d and concludes that \u201cs_{\u03bb/\u03bc} is a symmetric polynomial.\u201d The elaborated signature has `{N : \u2115} {R : Type u} [CommRing R] (lam mu : Fin N \u2192 \u2115)`, with `hlam : \u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i` and `hmu : \u2200 i j, i \u2264 j \u2192 mu j \u2264 mu i`; these are exactly the blueprint definition of N-partitions as weakly decreasing N-tuples of nonnegative integers. Its `hcontained : \u2200 i, mu i \u2264 lam i` is exactly componentwise `\u03bc \u2286 \u03bb`. The conclusion is `(SymmetricFunctions.skewSchur { outer := \u27e8lam, hlam\u27e9, inner := \u27e8mu, hmu\u27e9, contained := ... }).IsSymmetric`. Here `skewSchur s := \u2211 T \u2208 skewSSYTFinset s, T.toMonomial`, matching the definition `s_{\u03bb/\u03bc} = \u2211_{T \u2208 SSYT(\u03bb/\u03bc)} x_T`; `skewSSYTFinset` contains every dependent-type skew SSYT, and `SkewSSYT.toMonomial` is the product of the variables indexed by its entries. Mathlib elaborates `MvPolynomial.IsSymmetric \u03c6` as `\u2200 e : Equiv.Perm (Fin N), MvPolynomial.rename e \u03c6 = \u03c6`, exactly the blueprint definition of invariance under every variable permutation. The hidden `[CommRing R]` binder is the coefficient-ring setting supplied by the blueprint polynomial-ring definition, not an added mathematical hypothesis on \u03bb or \u03bc. Allowing `N = 0` is harmless extra generality. Finally, the proof really uses `jacobiTrudi_h` to rewrite the skew Schur polynomial as the Jacobi\u2013Trudi determinant and then applies `jacobiTrudiMatrixH_det_isSymmetric`, so the stated Jacobi\u2013Trudi proof route is also respected."
}
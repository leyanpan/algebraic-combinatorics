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
  "justification": "The informal claim is: \u201cfor any partitions \u03bb \u2287 \u03bc, s_{\u03bb/\u03bc} is a symmetric polynomial.\u201d The elaborated signature is `{N : \u2115} {R : Type u} [CommRing R] (lam mu : Fin N \u2192 \u2115) (hlam : \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i) (hmu : \u2200 i j : Fin N, i \u2264 j \u2192 mu j \u2264 mu i) (hcontained : \u2200 i : Fin N, mu i \u2264 lam i) : (skewSchur \u27e8\u27e8lam, hlam\u27e9, \u27e8mu, hmu\u27e9, ...\u27e9).IsSymmetric`. Thus `hlam` and `hmu` say exactly that \u03bb and \u03bc are weakly decreasing N-tuples of natural numbers, matching the blueprint definition of an N-partition, while `hcontained` is exactly the blueprint condition \u03bc \u2286 \u03bb, namely `\u03bc_i \u2264 \u03bb_i` for every i. The local `SkewPartition` body packages precisely two such partitions with that componentwise containment. The referenced `skewSchur` body is `\u2211 T \u2208 skewSSYTFinset s, T.toMonomial`; `skewSSYTFinset` contains all fillings with weakly increasing rows and strictly increasing columns, and `toMonomial` takes the product of variables indexed by the tableau entries, matching the blueprint definition of `s_{\u03bb/\u03bc}`. Finally, Mathlib\u2019s `MvPolynomial.IsSymmetric` unfolds to `\u2200 e : Perm (Fin N), rename e \u03c6 = \u03c6`, which is exactly the blueprint definition that every variable permutation fixes the polynomial. `[CommRing R]` is the coefficient-ring setting used by the blueprint\u2019s polynomial ring `K[x\u2081,\u2026,x_N]`, not an added mathematical restriction. Quantifying arbitrary `R` and allowing arbitrary `N`, including zero, is at least as general as the informal statement. The proof also follows the advertised route: it rewrites by `jacobiTrudi_h` and applies symmetry of the Jacobi\u2013Trudi determinant."
}
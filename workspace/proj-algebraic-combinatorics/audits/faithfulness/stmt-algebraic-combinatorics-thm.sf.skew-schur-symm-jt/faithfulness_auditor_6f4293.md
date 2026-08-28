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
  "justification": "Q1: yes. The formal conclusion `(skewSchur ...).IsSymmetric` says exactly that the skew Schur polynomial is invariant under every permutation of its variables: Mathlib documents `MvPolynomial.IsSymmetric` as \u201cinvariant under permutations of its variables by the `rename` operation.\u201d The definition `skewSchur` is `\u2211 T \u2208 skewSSYTFinset s, T.toMonomial`, matching the source definition of the skew Schur polynomial as a sum of tableau monomials. The binders `hlam : \u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i` and `hmu : \u2200 i j, i \u2264 j \u2192 mu j \u2264 mu i` encode precisely that `lam` and `mu` are partitions, while `hcontained : \u2200 i, mu i \u2264 lam i` is precisely the informal condition `\u03bb \u2287 \u03bc`; these are not added restrictions beyond the stated domain. Q2: yes. The informal assertion that, for such partitions, `s_{\u03bb/\u03bc}` is symmetric directly yields the formal conclusion under those encodings. The hidden section binders `{N : \u2115} {R : Type*} [CommRing R]` agree with the source convention \u201cFix a commutative ring K. Fix an N \u2208 \u2115\u201d and its polynomial ring `K[x\u2081,\u2026,x_N]`; `Fin N` is only the formal indexing of those N variables and N partition components. The methodological sentence is also accurately reflected by the implementation, whose proof rewrites with `jacobiTrudi_h` and applies `jacobiTrudiMatrixH_det_isSymmetric`, although proof provenance is not part of the theorem signature."
}
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
  "justification": "The informal claim is: \u201cfor any partitions \u03bb \u2287 \u03bc, s_{\u03bb/\u03bc} is a symmetric polynomial.\u201d The elaborated signature quantifies `{N : \u2115} {R : Type u} [CommRing R] (lam mu : Fin N \u2192 \u2115)` and assumes `hlam : \u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i`, `hmu : \u2200 i j, i \u2264 j \u2192 mu j \u2264 mu i`, and `hcontained : \u2200 i, mu i \u2264 lam i`. The first two assumptions exactly unpack the blueprint definition of an N-partition as a \u201cweakly decreasing N-tuple of nonnegative integers,\u201d while `hcontained` exactly expresses `\u03bb \u2287 \u03bc`; thus these are not added hypotheses. The conclusion is `(skewSchur (R := R) \u27e8\u27e8lam, hlam\u27e9, \u27e8mu, hmu\u27e9, ...\u27e9).IsSymmetric`. Here `SkewPartition` consists of `outer : NPartition N`, `inner : NPartition N`, and `contained : inner \u2264 outer`; `skewSchur` is definitionally `\u2211 T \u2208 skewSSYTFinset s, T.toMonomial`, matching the blueprint definition `s_{\u03bb/\u03bc} := \u2211_{T \u2208 SSYT(\u03bb/\u03bc)} x_T`. Mathlib defines `IsSymmetric \u03c6` as `\u2200 e : Equiv.Perm (Fin N), rename e \u03c6 = \u03c6`, which is precisely invariance under all permutations of the N variables required by the blueprint\u2019s definition of a symmetric polynomial. The implicit coefficient binder `[CommRing R]` realizes the blueprint polynomial ring over its commutative coefficient ring and does not restrict the claim. The proof also fulfills the stated methodological qualification: it rewrites by `jacobiTrudi_h` and applies `jacobiTrudiMatrixH_det_isSymmetric`, without invoking a Bender\u2013Knuth result."
}
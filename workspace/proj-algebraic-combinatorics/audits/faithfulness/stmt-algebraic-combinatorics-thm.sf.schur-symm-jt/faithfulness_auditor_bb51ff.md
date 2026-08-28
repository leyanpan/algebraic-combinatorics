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
  "justification": "Q1: Yes. The elaborated signature universally quantifies over `{N : \u2115}`, `{R : Type u} [CommRing R]`, `(lam : Fin N \u2192 \u2115)`, and `(hlam : \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i)`, and concludes `(schur \u27e8lam, hlam\u27e9).IsSymmetric`. The pair `\u27e8lam, hlam\u27e9` is exactly an `NPartition N`, whose fields are `parts : Fin N \u2192 \u2115` and the weak-decrease condition quoted above; thus `hlam` encodes being a partition rather than adding a hypothesis beyond the informal statement. The source context makes this explicit: \u201cLet \u03bb be an N-partition\u201d and \u201cThe polynomial s_\u03bb is symmetric.\u201d The project definition is also the intended Schur polynomial: `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial`, matching the source definition `s_\u03bb := \u2211_{T\u2208SSYT(\u03bb)} x_T`. Finally, Mathlib defines `IsSymmetric \u03c6` as `\u2200 (e : Equiv.Perm \u03c3), rename e \u03c6 = \u03c6`, matching the source definition \u201c\u03c3 \u00b7 f = f for all \u03c3 \u2208 S_N.\u201d Hence the Lean conclusion implies the informal claim. Q2: Yes. The source fixes \u201ca commutative ring K\u201d and \u201can N \u2208 \u2115\u201d, defines the polynomial ring in N variables, and quantifies over an N-partition \u03bb. These are precisely the implicit Lean binders `N`, `R`, `[CommRing R]` and the bundled data `\u27e8lam, hlam\u27e9`; indexing by `Fin N` rather than `[N] = {1,\u2026,N}` is an equivalent encoding. Therefore the informal theorem supplies the Lean conclusion for every choice of the elaborated binders. The proof route also agrees with the stated corollary: the declaration rewrites by `schur_eq_skewSchur_zero` and applies `skewSchur_isSymmetric_jacobiTrudi` with `mu := fun _ => 0`."
}
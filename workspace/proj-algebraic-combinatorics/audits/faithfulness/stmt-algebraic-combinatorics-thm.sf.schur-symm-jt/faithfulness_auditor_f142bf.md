Declaration: SymmetricFunctions.schur_isSymmetric_jacobiTrudi
Module: AlgebraicCombinatorics.SymmetricFunctions.PieriJacobiTrudi

Statement id: stmt-algebraic-combinatorics-thm.sf.schur-symm-jt

## INFORMAL STATEMENT
thm.sf.schur-symm-jt

\leanhelper  Schur polynomials are symmetric: for any partition $\lambda $, $s_\lambda $ is a symmetric polynomial. 

This is a corollary of Theorem~ \ref{thm.sf.skew-schur-symm-jt} with $\mu = 0$.

## VERDICT
{
  "verdict": "drift",
  "justification": "Q1: yes. The elaborated signature universally quantifies `{N : \u2115} {R : Type} [CommRing R]` and concludes `(schur (R := R) \u27e8lam, hlam\u27e9).IsSymmetric`; specializing to `R = \u2124` and positive `N` yields the informal claim. The partition binder also matches the source notion: `lam : Fin N \u2192 \u2115` with `hlam : \u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i` is precisely a weakly decreasing N-tuple. Moreover, Mathlib documents `MvPolynomial.IsSymmetric` as invariance under permutations of variables, matching \u201cis a symmetric polynomial.\u201d Q2: no as stated. The source context says, \u201cWe work over a fixed positive integer N and the polynomial ring P = \u2124[x_1, x_2, ..., x_N],\u201d whereas the declaration's folded section binders quantify over every natural `N`, including zero, and every coefficient type `R` satisfying `[CommRing R]`. Its referenced definition likewise has the genuinely coefficient-parametric body `noncomputable def schur ... : MvPolynomial (Fin N) R := \u2211 T \u2208 ssytFinset lam, T.toMonomial`. Thus the informal integer-coefficient, positive-dimensional assertion does not itself assert the declaration's additional cases over arbitrary commutative rings and `N = 0`. The difference enters at `SymmetricFunctions.schur_isSymmetric_jacobiTrudi` through the implicit binders `{N : \u2115}`, `{R : Type}`, and `[CommRing R]`, together with the `R` parameter in `SymmetricFunctions.schur`. To match the recorded source exactly, specialize the conclusion to `R := \u2124` and restrict `N` to the source's positive setting, for example with `[NeZero N]`; alternatively, revise the informal statement and its Schur-polynomial definition to explicitly quantify over arbitrary commutative coefficient rings and allow `N = 0`."
}
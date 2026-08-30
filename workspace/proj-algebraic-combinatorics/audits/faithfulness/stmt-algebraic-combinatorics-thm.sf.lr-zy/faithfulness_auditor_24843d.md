Declaration: AlgebraicCombinatorics.littlewoodRichardson
Module: AlgebraicCombinatorics.SymmetricFunctions.LittlewoodRichardson

Statement id: stmt-algebraic-combinatorics-thm.sf.lr-zy

## INFORMAL STATEMENT
Zelevinsky’s generalized Littlewood–Richardson rule, in Yamanouchi form

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\begin{equation}  s_{\nu }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}s_{\nu +\operatorname *{cont}T}. \end{equation}

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint\u2019s coefficient setting is fixed by the convention node as: \u201cWe fix a commutative ring K and a natural number N throughout,\u201d with the polynomial ring `P K N := MvPolynomial (Fin N) K`. The elaborated target instead begins `\u2200 {R : Type u} [CommRing R] {N : \u2115} [IsDomain R] (lam mu nu : Fin N \u2192 \u2115), ...`. Thus `[IsDomain R]` is an added hypothesis: it requires a nontrivial commutative ring without zero divisors and excludes commutative coefficient rings such as `ZMod 4`. This restriction is not needed to state the identity, tableaux, finite sums, or Schur polynomials. The remaining partition binders accurately encode \u201cLet \u03bb, \u03bc, \u03bd be three N-partitions\u201d: `IsNPartition lam \u2192 IsNPartition mu \u2192 IsNPartition nu`, where `IsNPartition lam := \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`. The conclusion also has the intended form: `schurPoly nu * skewSchurPoly lam mu = \u2211 T : {T : Tableau lam mu // IsYamanouchi nu T}, schurPoly (nu + contentTableau T.val)`, and `IsYamanouchi nu T` unfolds to semistandardness together with `\u2200 j > 0, IsNPartition (nu + contentColGeq T j)`. The drift enters directly through the target binder `[IsDomain R]`, inherited from the proof dependency `alternant_rho_isRegular [IsDomain R]`. To make the declaration faithful, remove `[IsDomain R]` from `littlewoodRichardson` and prove the polynomial identity for every `[CommRing R]`, for example by first proving the integral/combinatorial identity and transporting it to `R`, rather than relying on domain-only cancellation."
}
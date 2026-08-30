Declaration: tprod_rescale_substitution
Module: AlgebraicCombinatorics.FPS.InfiniteProducts2

Statement id: stmt-algebraic-combinatorics-prop.fps.subs.rule-infprod

## INFORMAL STATEMENT
prop.fps.subs.rule-infprod

If $\left( f_{i}\right) _{i\in I}\in K\left[ \left[ x\right] \right] ^{I}$ is a multipliable family of FPSs, and if $g\in K\left[ \left[ x\right] \right] $ is an FPS satisfying $\left[ x^{0}\right] g=0$, then the family $\left( f_{i}\circ g\right) _{i\in I}\in K\left[ \left[ x\right] \right] ^{I}$ is multipliable as well and we have $\left( \prod _{i\in I}f_{i}\right) \circ g=\prod _{i\in I}\left( f_{i}\circ g\right) $.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint quantifies an arbitrary zero-constant FPS: \u201cif g \u2208 K[[x]] is an FPS satisfying [x^0]g = 0,\u201d and concludes both that \u201cthe family (f_i \u2218 g) is multipliable\u201d and that \u201c(\u220f f_i) \u2218 g = \u220f (f_i \u2218 g).\u201d The elaborated Lean signature instead has binders `{K : Type} [CommRing K] [TopologicalSpace K] [IsTopologicalRing K] [T2Space K] {I : Type} (f : I \u2192 K\u27e6X\u27e7) (a : K) (hf : _root_.Multipliable f)` and conclusion `rescale a (\u220f' i, f i) = \u220f' i, rescale a (f i)`. The difference enters directly through `(a : K)` and `rescale a`: `PowerSeries.rescale` has body `fun f => PowerSeries.mk fun n => a ^ n * coeff n f` and means substitution only by `aX`. Thus the theorem covers only the special case `g = aX`, not arbitrary `g : K\u27e6X\u27e7` with `constantCoeff g = 0`. The project\u2019s blueprint substitution is expressible: `fps_comp (f g : K\u27e6X\u27e7) (_hg : constantCoeff g = 0) := PowerSeries.subst g f`. There is a second mismatch at `(hf : Multipliable f)`: elaboration resolves this to Mathlib\u2019s topological `_root_.Multipliable`, whose documented meaning is existence of a `HasProd`, whereas the blueprint definition node is `PowerSeries.Multipliable a := \u2200 n, CoeffFinitelyDeterminedInProd a n`. Correspondingly, `\u220f'` is Mathlib\u2019s topology-dependent unconditional product, not the product defined by the blueprint node from finitely determined coefficients. Finally, the Lean conclusion is only an equality; it does not assert that `(fun i => (f i).subst g)` is multipliable, even though that is an explicit part of the blueprint conclusion. To be faithful, this declaration must quantify `(g : K\u27e6X\u27e7)` and `(hg : constantCoeff g = 0)`, use `PowerSeries.subst g`, assume the project\u2019s coefficient-finite `PowerSeries.Multipliable f`, conclude `PowerSeries.Multipliable (fun i => (f i).subst g)`, and state the equality using the corresponding blueprint infinite-product definition."
}
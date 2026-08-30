Declaration: PowerSeries.comp_prod_multipliable
Module: AlgebraicCombinatorics.Details.InfiniteProducts2

Statement id: stmt-algebraic-combinatorics-prop.fps.subs.rule-infprod-mulable

## INFORMAL STATEMENT
prop.fps.subs.rule-infprod-mulable

\leanhelper  If $(f_i)_{i \in I}$ is multipliable and $[x^0]g = 0$, then $(f_i \circ g)_{i \in I}$ is multipliable.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The informal claim is: \u201cIf $(f_i)_{i \\in I}$ is multipliable and $[x^0]g = 0$, then $(f_i \\circ g)_{i \\in I}$ is multipliable.\u201d The elaborated signature has exactly the corresponding binders `f : I \u2192 PowerSeries K`, `g : PowerSeries K`, and `hg : constantCoeff g = 0`. Its hypothesis `hf_mulable : \u2200 n, \u2203 M : Finset I, \u2200 J : Finset I, M \u2286 J \u2192 coeff n (\u220f i \u2208 J, f i) = coeff n (\u220f i \u2208 M, f i)` is precisely the unfolded project definition `PowerSeries.Multipliable f`: `Multipliable a := \u2200 n, CoeffFinitelyDeterminedInProd a n`, where `CoeffFinitelyDeterminedInProd a n := \u2203 M, DeterminesCoeffInProd a M n` and `DeterminesCoeffInProd a M n := \u2200 J, M \u2286 J \u2192 coeff n (\u220f i \u2208 J, a i) = coeff n (\u220f i \u2208 M, a i)`. The conclusion repeats that same predicate for `fun i \u21a6 (f i).subst g`, and Mathlib\u2019s `f.subst g` is the composition $f \\circ g$ under the zero-constant-term hypothesis. The linked specialized definition `MultipliableFPS\u2081 f := PowerSeries.Multipliable (fun i \u21a6 (f i).val)` shows that the statement also implies the intended claim when \u201cmultipliable\u201d is read for families in $K[[x]]_1$; the Lean theorem is more general because it permits arbitrary power series satisfying the general finite-determination predicate. The hidden `[CommRing K]` matches the blueprint\u2019s formal-power-series setting, while `[DecidableEq I]` is only an encoding instance needed for `Finset` products and does not impose a mathematical restriction on the index type."
}
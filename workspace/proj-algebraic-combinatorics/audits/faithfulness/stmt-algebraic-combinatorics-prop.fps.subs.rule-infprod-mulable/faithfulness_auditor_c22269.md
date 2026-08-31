Declaration: PowerSeries.comp_prod_multipliable
Module: AlgebraicCombinatorics.Details.InfiniteProducts2

Statement id: stmt-algebraic-combinatorics-prop.fps.subs.rule-infprod-mulable

## INFORMAL STATEMENT
prop.fps.subs.rule-infprod-mulable

\leanhelper  If $(f_i)_{i \in I}$ is multipliable and $[x^0]g = 0$, then $(f_i \circ g)_{i \in I}$ is multipliable.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The informal statement says: \"If $(f_i)_{i \\in I}$ is multipliable and $[x^0]g = 0$, then $(f_i \\circ g)_{i \\in I}$ is multipliable.\" The elaborated Lean signature has arbitrary `{I : Type*}`, `f : I \u2192 PowerSeries K`, `g : PowerSeries K`, and exactly the zero-constant-term hypothesis `hg : constantCoeff g = 0`. Its hypothesis `hf_mulable : \u2200 n, \u2203 M : Finset I, \u2200 J : Finset I, M \u2286 J \u2192 coeff n (\u220f i \u2208 J, f i) = coeff n (\u220f i \u2208 M, f i)` is precisely the blueprint definition of multipliable: `Multipliable a := \u2200 n, CoeffFinitelyDeterminedInProd a n`, where `CoeffFinitelyDeterminedInProd a n := \u2203 M, DeterminesCoeffInProd a M n` and `DeterminesCoeffInProd a M n := \u2200 J, M \u2286 J \u2192 coeff n (\u220f i \u2208 J, a i) = coeff n (\u220f i \u2208 M, a i)`. The conclusion repeats this exact predicate for the family `i \u21a6 (f i).subst g`. The substitution definition node identifies `PowerSeries.subst g (f i)` with `f_i \u2218 g` when `[x^0]g = 0`, including the reversed Mathlib argument order. The hidden `[CommRing K]` is the blueprint's coefficient-ring setting, and `[DecidableEq I]` only supports `Finset` operations; it does not restrict the mathematical family because decidable equality can be supplied classically. Thus the formal hypothesis and conclusion match the blueprint statement coefficient-for-coefficient."
}
Declaration: PowerSeries.comp_prod_multipliable
Module: AlgebraicCombinatorics.Details.InfiniteProducts2

Statement id: stmt-algebraic-combinatorics-prop.fps.subs.rule-infprod-mulable

## INFORMAL STATEMENT
prop.fps.subs.rule-infprod-mulable

\leanhelper  If $(f_i)_{i \in I}$ is multipliable and $[x^0]g = 0$, then $(f_i \circ g)_{i \in I}$ is multipliable.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The informal hypothesis and conclusion are: \u201cIf $(f_i)_{i \\in I}$ is multipliable and $[x^0]g = 0$, then $(f_i \\circ g)_{i \\in I}$ is multipliable.\u201d The elaborated declaration has hidden setting binders `{K : Type*} [CommRing K] {I : Type*} [DecidableEq I]`, explicit hypotheses `(hg : constantCoeff g = 0)` and `(hf_mulable : \u2200 n, \u2203 M : Finset I, \u2200 J : Finset I, M \u2286 J \u2192 coeff n (\u220f i \u2208 J, f i) = coeff n (\u220f i \u2208 M, f i))`, and concludes `\u2200 n, \u2203 M : Finset I, \u2200 J : Finset I, M \u2286 J \u2192 coeff n (\u220f i \u2208 J, (f i).subst g) = coeff n (\u220f i \u2208 M, (f i).subst g)`. By the blueprint definition node, `PowerSeries.Multipliable a` unfolds to `\u2200 n, CoeffFinitelyDeterminedInProd a n`; that in turn unfolds to the existence of such an `M`, with `DeterminesCoeffInProd` exactly the displayed stabilization condition over every finite superset `J`. Thus `hf_mulable` is precisely that `(f_i)` is multipliable, and the conclusion is precisely that `((f i).subst g)` is multipliable. The composition definition node is also matched: `fps_comp f g hg` has body `PowerSeries.subst g f`, so `(f i).subst g` is the blueprint's `f_i \\circ g`, while `hg` exactly expresses `[x^0]g = 0`. `[DecidableEq I]` only supplies the decidability needed for the finite-set encoding and does not add a mathematical restriction. No substantive hypothesis or quantifier is added or omitted."
}
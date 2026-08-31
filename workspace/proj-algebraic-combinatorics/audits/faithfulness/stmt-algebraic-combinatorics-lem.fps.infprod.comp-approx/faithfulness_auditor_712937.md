Declaration: PowerSeries.comp_prod_approx_determines
Module: AlgebraicCombinatorics.Details.InfiniteProducts2

Statement id: stmt-algebraic-combinatorics-lem.fps.infprod.comp-approx

## INFORMAL STATEMENT
lem.fps.infprod.comp-approx

\leanhelper  If $M$ is an $x^n$-approximator for $(f_i)_{i \in I}$ (i.e., for all $k \leq n$ and $J \supseteq M$, $[x^k](\prod _{i \in J} f_i) = [x^k](\prod _{i \in M} f_i)$), and $[x^0]g = 0$, then for all $J \supseteq M$, $[x^n](\prod _{i \in J} (f_i \circ g)) = [x^n](\prod _{i \in M} (f_i \circ g))$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signature quantifies over `{K : Type} [CommRing K] {I : Type} [DecidableEq I]`, `f : I \u2192 PowerSeries K`, `g : PowerSeries K`, `n : \u2115`, and `M : Finset I`. Its hypothesis `hg : constantCoeff g = 0` exactly answers the blueprint's \u201c`[x^0]g = 0`.\u201d Its approximator hypothesis is `hM_approx : \u2200 k \u2264 n, \u2200 J : Finset I, M \u2286 J \u2192 coeff k (\u220f i \u2208 J, f i) = coeff k (\u220f i \u2208 M, f i)`, exactly the stated parenthetical \u201cfor all `k \u2264 n` and `J \u2287 M`, `[x^k](\u220f_{i\u2208J} f_i) = [x^k](\u220f_{i\u2208M} f_i)`.\u201d This also matches the blueprint definition of an `x^n`-approximator: `IsXnApproximator a M n := \u2200 m \u2264 n, DeterminesCoeffInProd a M m`, where `DeterminesCoeffInProd` quantifies over finite supersets `J : Finset I`. The conclusion `\u2200 J : Finset I, M \u2286 J \u2192 coeff n (\u220f i \u2208 J, (f i).subst g) = coeff n (\u220f i \u2208 M, (f i).subst g)` is precisely the requested equality for every finite `J \u2287 M`; `PowerSeries.subst g (f i)` is the formal composition `f_i \u2218 g` used by the blueprint's substitution definition. `[DecidableEq I]` only supplies the computational structure required for finite sets and finite products, so it is encoding rather than mathematical drift."
}
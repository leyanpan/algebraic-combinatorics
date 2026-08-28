Declaration: AlgebraicCombinatorics.FPS.binomialIdentity
Module: AlgebraicCombinatorics.FPS.NonIntegerPowers

Statement id: stmt-algebraic-combinatorics-prop.binom.nck-2i-qedmo.cn

## INFORMAL STATEMENT
prop.binom.nCk-2i-qedmo.CN

Let $n\in \mathbb {C}$ and $k\in \mathbb {N}$. Then,

\[  \sum _{i=0}^{k}\binom {n+i-1}{i}\binom {n}{k-2i}=\binom {n+k-1}{k}.  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "Q1 is yes: the elaborated signature is `\u2200 {K : Type u_1} [CommRing K] [Algebra \u211a K] [BinomialRing K] [CharZero K] (n : K) (k : \u2115), ...`, so specializing `K` to `\u2102` gives the informal claim for every `n \u2208 \u2102` and `k \u2208 \u2115`. Q2 is no: the informal statement quantifies only over `n \u2208 \u2102`, whereas the hidden section binder `{K : Type u_1}` makes the Lean declaration assert the identity in every commutative characteristic-zero \u211a-algebra equipped with a binomial-ring structure. The C-only statement does not itself assert that broader polymorphic claim; neither listed dependency changes the target's explicit domain from \u2102 to arbitrary K. This difference enters through the hidden binder `{K}` and its typeclass binders in `AlgebraicCombinatorics.FPS.binomialIdentity`, inherited from the module-level declarations `variable {K : Type*} [CommRing K] [Algebra \u211a K]`, `variable [BinomialRing K]`, and `variable [CharZero K]`. The summation-bound change is not the decisive drift: Lean uses `\u2211 i \u2208 range (k / 2 + 1)` instead of the informal `\u2211_{i=0}^{k}` because `Ring.choose` has a natural-number lower argument; this represents the conventional interpretation that terms with `k-2i < 0` are zero. Mathlib defines `Ring.choose r n` as the generalized descending-Pochhammer binomial coefficient, so it otherwise matches the intended complex binomial coefficient. To make the declaration faithful, specialize it to `(n : \u2102) (k : \u2115)` with the relevant instances inferred. Alternatively, broaden the informal target itself to quantify over every such `K`."
}
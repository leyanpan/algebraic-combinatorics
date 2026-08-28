Declaration: AlgebraicCombinatorics.FPS.binomialIdentity
Module: AlgebraicCombinatorics.FPS.NonIntegerPowers

Statement id: stmt-algebraic-combinatorics-prop.binom.nck-2i-qedmo.cn

## INFORMAL STATEMENT
prop.binom.nCk-2i-qedmo.CN

Let $n\in \mathbb {C}$ and $k\in \mathbb {N}$. Then,

\[  \sum _{i=0}^{k}\binom {n+i-1}{i}\binom {n}{k-2i}=\binom {n+k-1}{k}.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: yes. The elaborated signature is `binomialIdentity {K} [CommRing K] [Algebra \u211a K] [BinomialRing K] [CharZero K] (n : K) (k : \u2115)` with conclusion `\u2211 i \u2208 range (k / 2 + 1), Ring.choose (n + \u2191i - 1) i * Ring.choose n (k - 2 * i) = Ring.choose (n + \u2191k - 1) k`. Specializing `K` to `\u2102` gives the informal domain. Mathlib defines `Ring.choose` as the generalized binomial coefficient: `choose r n := multichoose (r - n + 1) n`, with `n! \u2022 choose r n` equal to the descending Pochhammer evaluation, matching the usual complex binomial coefficient. The formal range `range (k / 2 + 1)` is exactly `0 \u2264 i \u2264 \u230ak/2\u230b`. This is equivalent to the informal `\u2211_{i=0}^{k}` under the standard convention that a binomial coefficient with a negative lower index is zero; the omitted indices have `k-2i < 0`. Using Lean's natural subtraction over the full range would instead truncate `k-2i` to zero and incorrectly contribute `Ring.choose n 0 = 1`. Q2: yes. The formal generalization from `\u2102` to commutative characteristic-zero \u211a-algebras does not alter the identity: for fixed `k`, every `Ring.choose x j` is the rational descending-Pochhammer polynomial in `x`, so validity for every complex `n` forces the corresponding rational polynomial identity, which then evaluates identically in every such `K`. This broader setting is also carried by the declared dependency whose informal text says `Assume that K is a commutative \u211a-algebra`. Thus the generalized carrier and the shortened range are conservative encodings, not drift."
}
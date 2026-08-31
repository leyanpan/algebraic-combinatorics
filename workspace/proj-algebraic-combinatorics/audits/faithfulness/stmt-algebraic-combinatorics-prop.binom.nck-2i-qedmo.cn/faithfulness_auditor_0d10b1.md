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
  "justification": "The elaborated signature is `\u2200 {K : Type} [CommRing K] [Algebra \u211a K] [BinomialRing K] [CharZero K] (n : K) (k : \u2115), \u2211 i \u2208 Finset.range (k / 2 + 1), Ring.choose (n + \u2191i - 1) i * Ring.choose n (k - 2 * i) = Ring.choose (n + \u2191k - 1) k`. This specializes to the blueprint binders \u201cLet n \u2208 \u2102 and k \u2208 \u2115,\u201d since \u2102 satisfies these structures; quantification over suitable commutative \u211a-algebras is a strict generalization, not a restriction of the complex statement. The blueprint definition fixes `binom(n,j)` as the descending product divided by `j!` when `j \u2208 \u2115`, and as `0` otherwise. Mathlib's `Ring.choose r j` is the corresponding generalized binomial coefficient, defined from the uniquely factorial-divisible Pochhammer evaluation. The formal range `i \u2208 range (k / 2 + 1)`, namely `0 \u2264 i \u2264 floor(k/2)`, differs syntactically from the blueprint's `\u2211_{i=0}^{k}`, but not mathematically: for every omitted `i > floor(k/2)`, the lower argument `k - 2i` is a negative integer, so the blueprint definition makes `binom(n, k-2i) = 0`. Restricting the Lean sum avoids interpreting that subtraction as truncated natural subtraction. Thus the formal equality implies exactly the stated complex identity."
}
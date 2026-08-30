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
  "justification": "The informal binders are \u201cLet n\u2208\u2102 and k\u2208\u2115,\u201d while the elaborated declaration has `{K : Type} [CommRing K] [Algebra \u211a K] [BinomialRing K] [CharZero K] (n : K) (k : \u2115)`. Specializing `K` to `\u2102` gives exactly the required domain; the additional generality over suitable commutative \u211a-algebras strengthens rather than weakens the result. The formal conclusion is `\u2211 i \u2208 range (k / 2 + 1), Ring.choose (n + \u2191i - 1) i * Ring.choose n (k - 2 * i) = Ring.choose (n + \u2191k - 1) k`. Although the informal sum is written `\u2211_{i=0}^{k}`, the blueprint definition of `binom n j` makes it zero when the lower argument `j` is not a natural number. Thus every informal term with `i > \u230ak/2\u230b` has lower argument `k-2i < 0` and vanishes. Lean's `k - 2*i` is natural-number truncated subtraction, so restricting to `range (k / 2 + 1)`, namely `0 \u2264 i \u2264 \u230ak/2\u230b`, is the faithful encoding that avoids replacing a negative lower argument by zero. On `\u2102`, `Ring.choose` agrees with the blueprint coefficient `n(n-1)\u2026(n-k+1)/k!`, as captured by `binom_def_formula`. Therefore the formal equality specializes precisely to the stated complex identity."
}
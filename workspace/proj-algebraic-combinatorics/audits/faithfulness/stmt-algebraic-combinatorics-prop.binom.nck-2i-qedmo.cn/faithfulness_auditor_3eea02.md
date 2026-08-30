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
  "justification": "The blueprint states: \u201cLet n\u2208\u2102 and k\u2208\u2115\u201d and \u201c\u2211_{i=0}^{k} binom(n+i-1,i) binom(n,k-2i) = binom(n+k-1,k).\u201d The elaborated declaration is \u201c\u2200 {K : Type} [CommRing K] [Algebra \u211a K] [BinomialRing K] [CharZero K] (n : K) (k : \u2115), \u2211 i \u2208 Finset.range (k / 2 + 1), Ring.choose (n + \u2191i - 1) i * Ring.choose n (k - 2 * i) = Ring.choose (n + \u2191k - 1) k.\u201d This specializes directly to K = \u2102, for which all the displayed instances exist; quantifying over additional \u211a-algebras is a valid strengthening, not a restriction of the complex case. The blueprint definition of binomial coefficients says binom(r,j) is the descending-product quotient when j\u2208\u2115 and is zero otherwise. On a characteristic-zero field, AlgebraicCombinatorics.FPS.binom_def_formula establishes \u201cRing.choose r j = (descPochhammer \u2124 j).smeval r / j.factorial,\u201d so Ring.choose has the intended meaning over \u2102. Finally, Finset.range (k / 2 + 1) represents 0\u2264i\u2264\u230ak/2\u230b rather than the written 0\u2264i\u2264k. This is faithful because every omitted index has k-2i<0 as an integer and hence contributes zero under the blueprint's binomial definition; restricting the range also prevents Lean's natural-number subtraction from incorrectly truncating such negative indices to zero."
}
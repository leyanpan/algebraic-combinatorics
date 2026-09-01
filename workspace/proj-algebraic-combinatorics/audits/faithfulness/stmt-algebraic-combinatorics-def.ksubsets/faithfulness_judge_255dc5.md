## TARGET AlgebraicCombinatorics.SignedCounting.kSubsets (def) — ELABORATED SIGNATURE
ℕ → ℕ → Finset (Finset ℕ)

Body:
fun n k => Finset.powersetCard k (Finset.range n)

Docstring: The set of k-element subsets of [n]. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.powersetCard
{α : Type u_1} → ℕ → Finset α → Finset (Finset α)

Docstring: Given an integer `n` and a finset `s`, then `powersetCard n s` is the finset of subsets of `s`
of cardinality `n`. 

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## INFORMAL STATEMENT
def.kSubsets

\leanhelper  The set $\binom {[n]}{k}$ of $k$-element subsets of $\{ 0, \ldots , n-1\} $: 

\[  \binom {[n]}{k} := \bigl\{ S \subseteq \{ 0,\ldots ,n-1\}  : |S| = k\bigr\} .  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target defines `kSubsets n k` as `Finset.powersetCard k (Finset.range n)`. By the cited library definitions, `Finset.range n` is exactly the set of naturals less than `n`, i.e. `{0, \u2026, n-1}`, and `Finset.powersetCard k` returns exactly its subsets of cardinality `k`. Thus it matches `\\{S \\subseteq \\{0,\\ldots,n-1\\} : |S|=k\\}` with the same natural-number parameters `n` and `k`."
}
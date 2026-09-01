## TARGET AlgebraicCombinatorics.SignedCounting.partner (def) — ELABORATED SIGNATURE
Finset ℕ → Finset ℕ

Body:
fun I => symmDiff I {0}

Docstring: The partner of a finite set `I` is `I △ {0}` (symmetric difference with singleton 0).
If `0 ∈ I`, this removes 0; if `0 ∉ I`, this adds 0. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF symmDiff
{α : Type u_2} → [Max α] → [SDiff α] → α → α → α

Docstring: The symmetric difference operator on a type with `⊔` and `\` is `(A \ B) ⊔ (B \ A)`. 

## BASE-LIBRARY REF SemilatticeSup.toMax
{α : Type u} → [SemilatticeSup α] → Max α

## BASE-LIBRARY REF Lattice.toSemilatticeSup
{α : Type u} → [self : Lattice α] → SemilatticeSup α

## BASE-LIBRARY REF Finset.instLattice
{α : Type u_1} → [DecidableEq α] → Lattice (Finset α)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## INFORMAL STATEMENT
def.partner

\leanhelper  The \emph{partner} of a finite set $I$ of natural numbers is the symmetric difference $I' := I \bigtriangleup \{ 0\} $. If $0 \in I$, then $I' = I \setminus \{ 0\} $; if $0 \notin I$, then $I' = I \cup \{ 0\} $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint defines the partner of every \u201cfinite set $I$ of natural numbers\u201d as \u201c$I' := I \\bigtriangleup \\{0\\}$.\u201d The target has exactly the corresponding type and body: `Finset \u2115 \u2192 Finset \u2115` and `fun I => symmDiff I {0}`. Here `Finset \u2115` represents finite sets of natural numbers, `{0}` is the singleton finset containing natural-number zero, and `symmDiff` is symmetric difference. By its supplied definition `(I \\ {0}) \u2294 ({0} \\ I)`, this removes `0` when `0 \u2208 I` and adds it when `0 \u2209 I`, matching both explanatory cases. The `DecidableEq \u2115`, lattice, and set-difference instances are inferred implementation machinery and impose no additional mathematical hypothesis."
}
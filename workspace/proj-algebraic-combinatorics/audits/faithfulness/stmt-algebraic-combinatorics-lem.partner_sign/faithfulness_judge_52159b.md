## TARGET AlgebraicCombinatorics.SignedCounting.partner_sign (theorem) — ELABORATED SIGNATURE
∀ (I : Finset ℕ),
  AlgebraicCombinatorics.SignedCounting.setSign (AlgebraicCombinatorics.SignedCounting.partner I) =
    -AlgebraicCombinatorics.SignedCounting.setSign I

Docstring: The partner has opposite sign. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.setSign (def)
Finset ℕ → ℤ

Body:
fun I => (-1) ^ I.card

Docstring: The sign of a finite set is `(-1)^|I|`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.partner (def)
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


## BASE-LIBRARY REF Eq
{α : Sort u_1} → α → α → Prop

Docstring: The equality relation. It has one introduction rule, `Eq.refl`.
We use `a = b` as notation for `Eq a b`.
A fundamental property of equality is that it is an equivalence relation.
```
variable (α : Type) (a b c d : α)
variable (hab : a = b) (hcb : c = b) (hcd : c = d)

example : a = d :=
  Eq.trans (Eq.trans hab (Eq.symm hcb)) hcd
```
Equality is much more than an equivalence relation, however. It has the important property that every assertion
respects the equivalence, in the sense that we can substitute equal expressions without changing the truth value.
That is, given `h1 : a = b` and `h2 : p a`, we can construct a proof for `p b` using substitution: `Eq.subst h1 h2`.
Example:
```
example (α : Type) (a b : α) (p : α → Prop)
        (h1 : a = b) (h2 : p a) : p b :=
  Eq.subst h1 h2

example (α : Type) (a b : α) (p : α → Prop)
    (h1 : a = b) (h2 : p a) : p b :=
  h1 ▸ h2
```
The triangle in the second presentation is a macro built on top of `Eq.subst` and `Eq.symm`, and you can enter it by typing `\t`.
For more information: [Equality](https://lean-lang.org/theorem_proving_in_lean4/quantifiers_and_equality.html#equality)


Conventions for notations in identifiers:

 * The recommended spelling of `=` in identifiers is `eq`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

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


## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## INFORMAL STATEMENT
lem.partner_sign

\leanhelper  The partner reverses the sign: $\operatorname {sign}(I') = -\operatorname {sign}(I)$ for all finite sets $I$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.partner
def.partner

\leanhelper  The \emph{partner} of a finite set $I$ of natural numbers is the symmetric difference $I' := I \bigtriangleup \{ 0\} $. If $0 \in I$, then $I' = I \setminus \{ 0\} $; if $0 \notin I$, then $I' = I \cup \{ 0\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.setsign
def.setSign

\leanhelper  The \emph{sign} of a finite set $I$ of natural numbers is $\operatorname {sign}(I) := (-1)^{|I|}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over exactly the intended objects, `\u2200 (I : Finset \u2115)`, matching \u201cfor all finite sets I\u201d together with the definition\u2019s specification that I is a finite set of natural numbers. Its conclusion `setSign (partner I) = -setSign I` exactly matches `sign(I') = -sign(I)`. The dependency bodies also agree with the informal definitions: `partner I = symmDiff I {0}` matches `I' := I \u25b3 {0}`, and `setSign I = (-1) ^ I.card` over \u2124 matches `sign(I) := (-1)^{|I|}`. There are no added hypotheses or narrowed quantifiers."
}
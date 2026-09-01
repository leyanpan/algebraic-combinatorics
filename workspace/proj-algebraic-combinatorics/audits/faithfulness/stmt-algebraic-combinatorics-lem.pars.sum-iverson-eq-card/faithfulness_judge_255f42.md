## TARGET IversonBracket.sum_iverson_eq_card (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} (s : Finset α) (p : α → Prop) [inst : DecidablePred p],
  ∑ x ∈ s, IversonBracket.iverson (p x) = (Finset.filter p s).card

Docstring: Sum of Iverson brackets equals cardinality of the filtered set. 

## PROJECT DEPENDENCY IversonBracket.iverson (def)
(P : Prop) → [Decidable P] → {α : Type u_1} → [Zero α] → [One α] → α

Body:
fun P [Decidable P] {α} [Zero α] [One α] => if P then 1 else 0

Docstring: The Iverson bracket converts a proposition to its truth value (0 or 1).
(Definition \ref{def.pars.iverson})

This is the standard way to embed boolean values into a semiring:
- 1 if `P` is true
- 0 if `P` is false

In Mathlib, this is `if P then 1 else 0` or `(decide P).toNat` for naturals. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF DecidablePred
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: A decidable predicate.

A predicate is decidable if the corresponding proposition is `Decidable` for each possible argument.


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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Nat.instOne
One ℕ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## INFORMAL STATEMENT
lem.pars.sum-iverson-eq-card

\leanhelper  The sum of Iverson brackets equals the cardinality of the filtered set: $\sum _{x \in s} \left[ p(x) \right] = |s \cap \{ x : p(x)\} |$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.iverson
def.pars.iverson

We will use the \emph{Iverson bracket notation}: If $\mathcal{A}$ is a logical statement, then $\left[ \mathcal{A} \right]$ means the \emph{truth value} of $\mathcal{A}$; this is the integer $\begin{cases}  1, &  \text{if }\mathcal{A}\text{ is true};\\ 0, &  \text{if }\mathcal{A}\text{ is false}. \end{cases} $ 

Note that the Kronecker delta notation is a particular case of the Iverson bracket: We have 

\[  \delta _{i,j}=\left[ i=j \right]\  \  \  \  \  \  \  \  \  \  \text{for any objects }i\text{ and }j.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over exactly the relevant data, `\u2200 {\u03b1 : Type u_1} (s : Finset \u03b1) (p : \u03b1 \u2192 Prop)`, and states `\u2211 x \u2208 s, IversonBracket.iverson (p x) = (Finset.filter p s).card`. By the dependency body, `iverson (p x)` is `if p x then 1 else 0`, matching the informal bracket `[p(x)]`; its result is inferred as `\u2115` from the equality with `Finset.card`. By the library definition, `Finset.filter p s` is precisely the elements of `s` satisfying `p`, so its card is `|s \u2229 {x : p(x)}|`. The binder `[inst : DecidablePred p]` is computational encoding needed for the conditional and filter, not a mathematically contentful extra hypothesis. Although the informal definition calls the truth value an integer, using naturals for a sum of values in `{0,1}` and comparing it with a natural cardinality faithfully expresses the stated equality."
}
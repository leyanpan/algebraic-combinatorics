## TARGET AlgebraicCombinatorics.SubtractiveMethods.multiplicity (def) — ELABORATED SIGNATURE
{n d : ℕ} → (Fin n → Fin d) → Fin d → ℕ

Body:
fun {n d} x k => {i | x i = k}.card

Docstring: The multiplicity of element `k` in tuple `x` 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

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

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
def.cancel.multiplicity

\leanhelper  For an $n$-tuple $x : \operatorname {Fin} n \to \operatorname {Fin} d$ and $k \in \operatorname {Fin} d$, the \emph{multiplicity} of $k$ in $x$ is the number of all $i \in \operatorname {Fin} n$ satisfying $x(i) = k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal definition has binders `{n d : \u2115} \u2192 (Fin n \u2192 Fin d) \u2192 Fin d \u2192 \u2115`, exactly matching an `n`-tuple `x : Fin n \u2192 Fin d` and an element `k : Fin d`. Its body, `fun {n d} x k => {i | x i = k}.card`, is the cardinality of the finite set of all `i : Fin n` satisfying `x i = k`. This is precisely the informal definition: \u201cthe number of all `i \u2208 Fin n` satisfying `x(i) = k`.\u201d The implicit decidable equality and finite-universe machinery merely encode this finite counting operation and impose no additional mathematical hypothesis."
}
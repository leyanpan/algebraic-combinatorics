## TARGET AlgebraicCombinatorics.SubtractiveMethods.flipSign_ne_self (theorem) — ELABORATED SIGNATURE
∀ {d : ℕ} (k j : Fin d) (e : Fin d → ZMod 2), j ≠ k → AlgebraicCombinatorics.SubtractiveMethods.flipSign k e j = e j

Docstring: flipSign at position k leaves other positions unchanged 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.flipSign (def)
{d : ℕ} → Fin d → (Fin d → ZMod 2) → Fin d → ZMod 2

Body:
fun {d} k e => Function.update e k (e k + 1)

Docstring: The involution that flips the k-th sign: if `e_k = +1`, make it `-1`, and vice versa 

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


## BASE-LIBRARY REF ZMod
ℕ → Type

Docstring: The integers modulo `n : ℕ`. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

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

## BASE-LIBRARY REF Function.update
{α : Sort u} → {β : α → Sort v} → [DecidableEq α] → ((a : α) → β a) → (a' : α) → β a' → (a : α) → β a

Docstring: Replacing the value of a function at a given point by a given value. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Distrib.toAdd
{R : Type u_1} → [self : Distrib R] → Add R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF ZMod.commRing
(n : ℕ) → CommRing (ZMod n)

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF DivisionRing.toRing
{K : Type u_2} → [self : DivisionRing K] → Ring K

## BASE-LIBRARY REF Field.toDivisionRing
{K : Type u} → [self : Field K] → DivisionRing K

## BASE-LIBRARY REF ZMod.instField
(p : ℕ) → [hp : Fact (Nat.Prime p)] → Field (ZMod p)

Docstring: Field structure on `ZMod p` if `p` is prime. 

## BASE-LIBRARY REF Nat.fact_prime_two
Fact (Nat.Prime 2)

## INFORMAL STATEMENT
flipSign leaves other positions unchanged

\leanhelper  For any $k, j \in [d]$ with $j \neq k$ and $e \in \{ 1,-1\} ^d$, $(\operatorname {flipSign}_k(e))_j = e_j$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.flipsign
def.cancel.flipSign

\leanhelper  For $k \in [d]$, the map $\operatorname {flipSign}_k : \{ 1,-1\} ^d \to \{ 1,-1\} ^d$ sends a $d$-tuple $(e_1, \ldots , e_d)$ to the tuple obtained by flipping the sign of the $k$-th entry: i.e., replacing $e_k$ by $-e_k$ and leaving all other entries unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifies over \u201cany $k,j\\in[d]$ with $j\\ne k$ and $e\\in\\{1,-1\\}^d$\u201d and concludes $(\\operatorname{flipSign}_k(e))_j=e_j$. The elaborated signature matches this as `\u2200 {d : \u2115} (k j : Fin d) (e : Fin d \u2192 ZMod 2), j \u2260 k \u2192 flipSign k e j = e j`, using `Fin d` for positions and `ZMod 2` as the two-valued sign encoding. Moreover, `flipSign` is defined as `Function.update e k (e k + 1)`, so only position `k` is replaced; every `j \u2260 k` retains `e j`, exactly as claimed. There are no added mathematical hypotheses or narrowed quantifiers."
}
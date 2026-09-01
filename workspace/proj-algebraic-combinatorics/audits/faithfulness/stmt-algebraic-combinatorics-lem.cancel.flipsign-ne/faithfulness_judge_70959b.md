## TARGET AlgebraicCombinatorics.SubtractiveMethods.flipSign_ne (theorem) — ELABORATED SIGNATURE
∀ {d : ℕ} (k : Fin d) (e : Fin d → ZMod 2), AlgebraicCombinatorics.SubtractiveMethods.flipSign k e ≠ e

Docstring: flipSign produces a different tuple 

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
lem.cancel.flipSign-ne

\leanhelper  For any $k \in [d]$ and $e \in \{ 1,-1\} ^d$, we have $\operatorname {flipSign}_k(e) \neq e$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.flipsign
def.cancel.flipSign

\leanhelper  For $k \in [d]$, the map $\operatorname {flipSign}_k : \{ 1,-1\} ^d \to \{ 1,-1\} ^d$ sends a $d$-tuple $(e_1, \ldots , e_d)$ to the tuple obtained by flipping the sign of the $k$-th entry: i.e., replacing $e_k$ by $-e_k$ and leaving all other entries unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifies over \u201cany $k \\in [d]$ and $e \\in \\{1,-1\\}^d$\u201d and concludes $\\operatorname{flipSign}_k(e) \\neq e$. The elaborated signature has exactly the corresponding binders, `\u2200 {d : \u2115} (k : Fin d) (e : Fin d \u2192 ZMod 2)`, with `Fin d` representing `[d]` and `ZMod 2` serving as the two-element sign encoding. The dependency defines the operation as `Function.update e k (e k + 1)`: addition of `1` in `ZMod 2` toggles the two possible encoded values, while `Function.update` leaves every other coordinate unchanged. Thus the updated value at `k` differs, yielding precisely `flipSign k e \u2260 e`. There are no added hypotheses or narrowed quantifiers; when `d = 0`, the absence of any `k : Fin 0` correctly makes the statement vacuous."
}
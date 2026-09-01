## TARGET WeightedSet.prod (def) — ELABORATED SIGNATURE
{α : Type u_2} → {β : Type u_3} → WeightedSet α → WeightedSet β → WeightedSet (α × β)

Body:
fun {α} {β} W₁ W₂ =>
  {
    weight := fun x =>
      match x with
      | (a, b) => W₁.weight a + W₂.weight b }

Docstring: The product of two weighted sets, with weight defined as the sum of component weights.
(Definition \ref{def.gf-ws.prod}) 

## PROJECT DEPENDENCY WeightedSet (inductive)
Type u_2 → Type u_2

Body:
WeightedSet.mk : {α : Type u_2} → (α → ℕ) → WeightedSet α

Docstring: A weighted set is a type equipped with a weight function to ℕ.
(Definition \ref{def.gf-ws.weighted-sets}(a)) 

## PROJECT DEPENDENCY WeightedSet.mk (constructor)
{α : Type u_2} → (α → ℕ) → WeightedSet α

## PROJECT DEPENDENCY WeightedSet.weight (def)
{α : Type u_2} → WeightedSet α → α → ℕ

Body:
fun α self => self.1

Docstring: The weight function assigning a natural number to each element 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## INFORMAL STATEMENT
def.gf-ws.prod

Let $A$ and $B$ be two weighted sets. Then, the weighted set $A\times B$ is defined to be the Cartesian product of the sets $A$ and $B$ (that is, the set $\left\{  \left( a,b\right) \  \mid \  a\in A\text{ and }b\in B\right\}  $), with the weight function defined as follows: For any $\left( a,b\right) \in A\times B$, we set

\begin{equation}  \left\vert \left( a,b\right) \right\vert =\left\vert a\right\vert +\left\vert b\right\vert . \end{equation}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint defines the carrier as the Cartesian product and requires \u201cfor any (a,b) \u2208 A\u00d7B\u201d that \u201c|(a,b)| = |a| + |b|.\u201d The elaborated signature takes arbitrary weighted sets `W\u2081 : WeightedSet \u03b1` and `W\u2082 : WeightedSet \u03b2` and returns `WeightedSet (\u03b1 \u00d7 \u03b2)`, so its carrier is exactly the product type. Its body sets `weight := fun (a, b) => W\u2081.weight a + W\u2082.weight b`, exactly matching the prescribed componentwise sum. There are no added hypotheses or restricted quantifiers."
}
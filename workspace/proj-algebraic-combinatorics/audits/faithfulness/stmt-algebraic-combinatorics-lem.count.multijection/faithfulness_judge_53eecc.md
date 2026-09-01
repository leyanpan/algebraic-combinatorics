## TARGET AlgebraicCombinatorics.QBinomialRec.card_eq_mul_of_fibers (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_3} {B : Type u_4} [inst : Fintype A] [inst_1 : Fintype B] [inst_2 : DecidableEq B] (f : A → B) (m : ℕ),
  (∀ (b : B), Fintype.card { a // f a = b } = m) → Fintype.card A = m * Fintype.card B

Docstring: Lemma lem.count.multijection: Multijection principle.
If f : A → B is a map such that each b ∈ B has exactly m preimages, then |A| = m · |B|.

This is a fundamental counting principle used throughout combinatorics.
A map f satisfying this assumption is called an m-to-1 map.

The proof uses the fiber decomposition: |A| = Σ_{b ∈ B} |fiber(b)|,
where each fiber has cardinality m by assumption. 

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


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

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF Subtype.fintype
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → [Fintype α] → Fintype { x // p x }

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## INFORMAL STATEMENT
Multijection principle

Let $A$ and $B$ be two finite sets. Let $m\in \mathbb {N}$. Let $f:A\rightarrow B$ be any map. Assume that each $b\in B$ has exactly $m$ preimages under $f$ (that is, for each $b\in B$, there are exactly $m$ many elements $a\in A$ such that $f\left( a\right) =b$). Then, 

\[  \left\vert A\right\vert =m\cdot \left\vert B\right\vert .  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint assumes finite A and B, a map f : A \u2192 B, m \u2208 \u2115, and \u201cfor each b \u2208 B, there are exactly m many elements a \u2208 A such that f(a)=b.\u201d These correspond exactly to `[Fintype A] [Fintype B]`, `(f : A \u2192 B) (m : \u2115)`, and `(\u2200 b : B, Fintype.card { a // f a = b } = m)`. The conclusion `Fintype.card A = m * Fintype.card B` is precisely `|A| = m \u00b7 |B|`. The additional binder `[DecidableEq B]` supplies decidability needed to form/count the equality-defined fibers in Lean; it is computational encoding rather than a mathematically contentful restriction on a finite set."
}
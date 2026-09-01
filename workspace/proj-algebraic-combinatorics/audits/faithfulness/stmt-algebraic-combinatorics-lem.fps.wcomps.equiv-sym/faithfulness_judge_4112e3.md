## TARGET AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts'.equivSym (def) — ELABORATED SIGNATURE
(n k : ℕ) → AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts' n k ≃ Sym (Fin k) n

Body:
fun n k =>
  { toFun := AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts'.toSym n k,
    invFun := AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts'.fromSym n k, left_inv := ⋯, right_inv := ⋯ }

Docstring: Equivalence between `ofSizeIntoParts' n k` and `Sym (Fin k) n`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts' (def)
ℕ → ℕ → Type

Body:
fun n k => { f // ∑ i, f i = n }

Docstring: Alternative representation of weak compositions as functions `Fin k → ℕ`.
This is equivalent to `ofSizeIntoParts n k` but easier to work with for cardinality proofs.


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts'.toSym (def)
(n k : ℕ) → AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts' n k → Sym (Fin k) n

Body:
fun n k x =>
  match x with
  | ⟨f, hf⟩ => ⟨∑ i, Multiset.replicate (f i) i, ⋯⟩

Docstring: Bijection from `ofSizeIntoParts' n k` to `Sym (Fin k) n`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts'.fromSym (def)
(n k : ℕ) → Sym (Fin k) n → AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts' n k

Body:
fun n k s => ⟨fun i => Multiset.count i ↑s, ⋯⟩

Docstring: Bijection from `Sym (Fin k) n` to `ofSizeIntoParts' n k`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Sym
Type u_1 → ℕ → Type (max 0 u_1)

Docstring: The nth symmetric power is n-tuples up to permutation.  We define it
as a subtype of `Multiset` since these are well developed in the
library.  We also give a definition `Sym.sym'` in terms of vectors, and we
show these are equivalent in `Sym.symEquivSym'`.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF AddCancelCommMonoid.toAddCommMonoid
{M : Type u} → [self : AddCancelCommMonoid M] → AddCommMonoid M

## BASE-LIBRARY REF Multiset.instAddCancelCommMonoid
{α : Type u_1} → AddCancelCommMonoid (Multiset α)

## BASE-LIBRARY REF Multiset.replicate
{α : Type u_1} → ℕ → α → Multiset α

Docstring: `replicate n a` is the multiset containing only `a` with multiplicity `n`. 

## BASE-LIBRARY REF Multiset.count
{α : Type u_1} → [DecidableEq α] → α → Multiset α → ℕ

Docstring: `count a s` is the multiplicity of `a` in `s`. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## INFORMAL STATEMENT
lem.fps.wcomps.equiv-sym

\leanhelper  The function-based weak compositions of $n$ into $k$ parts are equivalent to multisets of size $n$ from a $k$-element alphabet.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.wcomps
def.fps.wcomps

\textbf{(a)} An \emph{(integer) weak composition} means a (finite) tuple of nonnegative integers. \medskip 

\textbf{(b)} The \emph{size} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{weak composition of }$n$ means a weak composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{weak composition of }$n$\emph{ into }$k$\emph{ parts} is a weak composition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over all naturals, `(n k : \u2115)`, and gives an equivalence `ofSizeIntoParts' n k \u2243 Sym (Fin k) n`. The dependency defines `ofSizeIntoParts' n k` as `{ f // \u2211 i, f i = n }`, i.e. functions `Fin k \u2192 \u2115` whose values sum to `n`, exactly the function-based representation of weak compositions of size `n` and length `k`. By the library definitions, `Fin k` is a `k`-element index/alphabet type and `Sym (Fin k) n` is the type of multisets of cardinality `n` over it. Thus the formal equivalence matches \u201cThe function-based weak compositions of n into k parts are equivalent to multisets of size n from a k-element alphabet,\u201d including the edge cases `n = 0` and `k = 0`, with no added mathematical hypotheses."
}
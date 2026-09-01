## TARGET AlgebraicCombinatorics.Determinants.sortEquivPQ (def) — ELABORATED SIGNATURE
{m : ℕ} → (P : Finset (Fin m)) → Fin P.card ⊕ Fin (m - P.card) ≃ Fin m

Body:
fun {m} P => finSumEquivOfFinset ⋯ ⋯

Docstring: Equivalence that sorts indices so that P elements come first (as Sum.inl)
and Pᶜ elements come second (as Sum.inr). This uses `finSumEquivOfFinset`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.submatrixDet (def)
{R : Type u_1} → [CommRing R] → {m : ℕ} → Matrix (Fin m) (Fin m) R → Finset (Fin m) → Finset (Fin m) → R

Body:
fun {R} [CommRing R] {m} A P Q =>
  if h : P.card = Q.card then (AlgebraicCombinatorics.Determinants.submatrixOfFinsets' A P Q ⋯ ⋯).det else 0

Docstring: The determinant of a submatrix corresponding to row set P and column set Q.
Returns 0 if |P| ≠ |Q|. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.submatrixOfFinsets' (def)
{R : Type u_1} →
  {m k : ℕ} → Matrix (Fin m) (Fin m) R → (P Q : Finset (Fin m)) → P.card = k → Q.card = k → Matrix (Fin k) (Fin k) R

Body:
fun {R} {m k} A P Q hP hQ =>
  A.submatrix ⇑(AlgebraicCombinatorics.Determinants.finsetToFin P hP)
    ⇑(AlgebraicCombinatorics.Determinants.finsetToFin Q hQ)

Docstring: The submatrix of A with rows from P and columns from Q (when |P| = |Q|).
This is the minor sub_P^Q(A) in the source notation. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.finsetToFin (def)
{m k : ℕ} → (S : Finset (Fin m)) → S.card = k → Fin k ↪ Fin m

Body:
fun {m k} S hk => (S.orderIsoOfFin hk).toEmbedding.trans (Function.Embedding.subtype fun x => x ∈ S)

Docstring: Helper: Given a finset of indices, produce an order-preserving embedding into Fin m.
This is used to extract submatrices corresponding to index subsets. 

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

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Sum
Type u → Type v → Type (max u v)

Docstring: The disjoint union of types `α` and `β`, ordinarily written `α ⊕ β`.

An element of `α ⊕ β` is either an `a : α` wrapped in `Sum.inl` or a `b : β` wrapped in `Sum.inr`.
`α ⊕ β` is not equivalent to the set-theoretic union of `α` and `β` because its values include an
indication of which of the two types was chosen. The union of a singleton set with itself contains
one element, while `Unit ⊕ Unit` contains distinct values `inl ()` and `inr ()`.


## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF finSumEquivOfFinset
{α : Type u_1} →
  [inst : DecidableEq α] →
    [inst_1 : Fintype α] → [LinearOrder α] → {m n : ℕ} → {s : Finset α} → s.card = m → sᶜ.card = n → Fin m ⊕ Fin n ≃ α

Docstring: If `α` is a linearly ordered fintype, `s : Finset α` has cardinality `m` and its complement has
cardinality `n`, then `Fin m ⊕ Fin n ≃ α`. The equivalence sends elements of `Fin m` to
elements of `s` and elements of `Fin n` to elements of `sᶜ` while preserving order on each
"half" of `Fin m ⊕ Fin n` (using `Set.orderIsoOfFin`). 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Fin.instLinearOrder
{n : ℕ} → LinearOrder (Fin n)

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


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

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Function.Embedding
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ↪ β` is a bundled injective function. 

## BASE-LIBRARY REF Function.instFunLikeEmbedding
{α : Sort u} → {β : Sort v} → FunLike (α ↪ β) α β

## BASE-LIBRARY REF Function.Embedding.trans
{α : Sort u_1} → {β : Sort u_2} → {γ : Sort u_3} → (α ↪ β) → (β ↪ γ) → α ↪ γ

Docstring: Composition of `f : α ↪ β` and `g : β ↪ γ`. 

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

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Equiv.toEmbedding
{α : Sort u} → {β : Sort v} → α ≃ β → α ↪ β

Docstring: Convert an `α ≃ β` to `α ↪ β`.

This is also available as a coercion `Equiv.coeEmbedding`.
The explicit `Equiv.toEmbedding` version is preferred though, since the coercion can have issues
inferring the type of the resulting embedding. For example:

```lean
-- Works:
example (s : Finset (Fin 3)) (f : Equiv.Perm (Fin 3)) : s.map f.toEmbedding = s.map f := by simp
-- Error, `f` has type `Fin 3 ≃ Fin 3` but is expected to have type `Fin 3 ↪ ?m_1 : Type ?`
example (s : Finset (Fin 3)) (f : Equiv.Perm (Fin 3)) : s.map f = s.map f.toEmbedding := by simp
```


## BASE-LIBRARY REF RelIso.toEquiv
{α : Type u_5} → {β : Type u_6} → {r : α → α → Prop} → {s : β → β → Prop} → r ≃r s → α ≃ β

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF Subtype.instLE
{α : Type u} → [LE α] → {P : α → Prop} → LE (Subtype P)

## BASE-LIBRARY REF Preorder.toLE
{α : Type u_2} → [self : Preorder α] → LE α

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF DistribLattice.toLattice
{α : Type u_1} → [self : DistribLattice α] → Lattice α

## BASE-LIBRARY REF instDistribLatticeOfLinearOrder
{α : Type u} → [LinearOrder α] → DistribLattice α

## BASE-LIBRARY REF Finset.orderIsoOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ≃o ↥s

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderIsoOfFin s h`
is the increasing bijection between `Fin k` and `s` as an `OrderIso`. Here, `h` is a proof that
the cardinality of `s` is `k`. We use this instead of an iso `Fin s.card ≃o s` to avoid
casting issues in further uses of this function. 

## BASE-LIBRARY REF Function.Embedding.subtype
{α : Sort u_1} → (p : α → Prop) → Subtype p ↪ α

Docstring: Embedding of a `Subtype`. 

## INFORMAL STATEMENT
def.det.sortEquivPQ

\leanhelper  Given a subset $P$ of $[m]$, the \emph{sorting equivalence} is a bijection 

\[  \{ 1, \ldots , |P|\}  \sqcup \{ 1, \ldots , m - |P|\}  \xrightarrow {\sim } [m]  \]

 that sends the $i$-th element of the left component to the $i$-th smallest element of $P$ and the $j$-th element of the right component to the $j$-th smallest element of $P^c$. This equivalence is used to decompose matrices into block form with respect to the partition $[m] = P \sqcup P^c$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint asks, for \u201ca subset P of [m],\u201d for a bijection from the two components of sizes |P| and m\u2212|P| to [m], ordered so that each component maps increasingly into P and P\u1d9c. The elaborated signature quantifies exactly `{m : \u2115} \u2192 (P : Finset (Fin m))` and returns `Fin P.card \u2295 Fin (m - P.card) \u2243 Fin m`, matching the stated 0-based `Fin` convention. Its body uses `finSumEquivOfFinset`, whose specification says that it sends the `Fin m` half to the finset and the other half to its complement \u201cwhile preserving order on each half.\u201d Thus the left and right indices map respectively to the corresponding smallest elements of `P` and `P\u1d9c`. There are no additional mathematically substantive hypotheses or narrowed quantifiers."
}
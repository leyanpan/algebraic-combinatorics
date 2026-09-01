## TARGET AlgebraicCombinatorics.CauchyBinet.extractAlpha_constructSigma (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (P Q : Finset (Fin n)) (hcard : P.card = Q.card) (α : Equiv.Perm (Fin P.card)) (β : Equiv.Perm (Fin Pᶜ.card))
  (hσ :
    AlgebraicCombinatorics.CauchyBinet.imageFinset (AlgebraicCombinatorics.CauchyBinet.constructSigma P Q hcard α β) P =
      Q),
  AlgebraicCombinatorics.CauchyBinet.extractAlpha P Q hcard
      (AlgebraicCombinatorics.CauchyBinet.constructSigma P Q hcard α β) hσ =
    α

Docstring: Round-trip lemma: extractAlpha of constructSigma equals the original α. 

## TARGET AlgebraicCombinatorics.CauchyBinet.constructSigma_extract (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (P Q : Finset (Fin n)) (hcard : P.card = Q.card) (σ : Equiv.Perm (Fin n))
  (hσ : AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q),
  AlgebraicCombinatorics.CauchyBinet.constructSigma P Q hcard
      (AlgebraicCombinatorics.CauchyBinet.extractAlpha P Q hcard σ hσ)
      (AlgebraicCombinatorics.CauchyBinet.extractBeta P Q hcard σ hσ) =
    σ

Docstring: Round-trip lemma: constructSigma of (extractAlpha, extractBeta) equals the original σ.
This is the other direction of the bijection, showing that extract ∘ construct = id. 

## TARGET AlgebraicCombinatorics.CauchyBinet.extractBeta_constructSigma (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (P Q : Finset (Fin n)) (hcard : P.card = Q.card) (α : Equiv.Perm (Fin P.card)) (β : Equiv.Perm (Fin Pᶜ.card))
  (hσ :
    AlgebraicCombinatorics.CauchyBinet.imageFinset (AlgebraicCombinatorics.CauchyBinet.constructSigma P Q hcard α β) P =
      Q),
  AlgebraicCombinatorics.CauchyBinet.extractBeta P Q hcard
      (AlgebraicCombinatorics.CauchyBinet.constructSigma P Q hcard α β) hσ =
    β

Docstring: Round-trip lemma: extractBeta of constructSigma equals the original β. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.imageFinset (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n) → Finset (Fin n)

Body:
fun {n} σ P => Finset.map { toFun := ⇑σ, inj' := ⋯ } P

Docstring: The image of a finset under a permutation.

This is definitionally equal to `PermFinset.imageFinset` (see `imageFinset_eq_permFinset`).
New code should prefer `PermFinset.imageFinset`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.constructSigma (def)
{n : ℕ} →
  (P Q : Finset (Fin n)) → P.card = Q.card → Equiv.Perm (Fin P.card) → Equiv.Perm (Fin Pᶜ.card) → Equiv.Perm (Fin n)

Body:
fun {n} P Q hcard α β =>
  have hcardC := ⋯;
  have pEmb := P.orderEmbOfFin ⋯;
  let qEmb := Q.orderEmbOfFin ⋯;
  have pCEmb := Pᶜ.orderEmbOfFin ⋯;
  let qCEmb := Qᶜ.orderEmbOfFin ⋯;
  let f := fun x =>
    if h : x ∈ P then qEmb (α ((P.orderIsoOfFin ⋯).symm ⟨x, h⟩)) else qCEmb (β ((Pᶜ.orderIsoOfFin ⋯).symm ⟨x, ⋯⟩));
  have hf_inj := ⋯;
  Equiv.ofBijective f ⋯

Docstring: Given α ∈ Perm(Fin |P|) and β ∈ Perm(Fin |Pᶜ|), construct σ ∈ Perm(Fin n) with σ(P) = Q.
This is the inverse of the (extractAlpha, extractBeta) bijection. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.extractAlpha (def)
{n : ℕ} →
  (P Q : Finset (Fin n)) →
    P.card = Q.card →
      (σ : Equiv.Perm (Fin n)) → AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → Equiv.Perm (Fin P.card)

Body:
fun {n} P Q hcard σ hσ =>
  let pEmb := P.orderEmbOfFin ⋯;
  have h := ⋯;
  let qIso := Q.orderIsoOfFin ⋯;
  let f := fun i => qIso.symm ⟨σ (pEmb i), ⋯⟩;
  have hf_inj := ⋯;
  have hf_surj := ⋯;
  Equiv.ofBijective f ⋯

Docstring: Extract α from σ: For σ with σ(P) = Q, extract the permutation α ∈ Perm(Fin |P|)
that describes how σ permutes the elements of P.

Specifically, if p₁ < p₂ < ... < pₖ are the elements of P and 
q₁ < q₂ < ... < qₖ are the elements of Q, then α is defined by
σ(pᵢ) = q_{α(i)}. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.extractBeta (def)
{n : ℕ} →
  (P Q : Finset (Fin n)) →
    P.card = Q.card →
      (σ : Equiv.Perm (Fin n)) → AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → Equiv.Perm (Fin Pᶜ.card)

Body:
fun {n} P Q hcard σ hσ =>
  have hcard' := ⋯;
  let pEmb := Pᶜ.orderEmbOfFin ⋯;
  have h := ⋯;
  let qIso := Qᶜ.orderIsoOfFin ⋯;
  let f := fun i => qIso.symm ⟨σ (pEmb i), ⋯⟩;
  have hf_inj := ⋯;
  have hf_surj := ⋯;
  Equiv.ofBijective f ⋯

Docstring: Extract β from σ: For σ with σ(P) = Q, extract the permutation β ∈ Perm(Fin |Pᶜ|)
that describes how σ permutes the elements of Pᶜ. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.submatrixOfFinset (def)
{R : Type u_1} →
  {n m : ℕ} →
    Matrix (Fin n) (Fin m) R → (U : Finset (Fin n)) → (V : Finset (Fin m)) → Matrix (Fin U.card) (Fin V.card) R

Body:
fun {R} {n m} A U V => A.submatrix ⇑(U.orderEmbOfFin ⋯) ⇑(V.orderEmbOfFin ⋯)

Docstring: The submatrix of A obtained by restricting to rows in U and columns in V.
This corresponds to `sub_U^V A` in the source (Definition def.det.sub).
Label: def.det.sub

## Mathematical Description

Let A be an n×m matrix. Let U ⊆ [n] and V ⊆ [m] be subsets.
Writing U = {u₁, u₂, ..., uₚ} with u₁ < u₂ < ... < uₚ
and V = {v₁, v₂, ..., vₚ} with v₁ < v₂ < ... < vₚ,
we define sub_U^V A := (A_{uᵢ,vⱼ})_{1≤i≤p, 1≤j≤q}.

This is the |U|×|V| matrix obtained from A by keeping only the rows
indexed by U and columns indexed by V, in increasing order.

## Terminology

- **Submatrix**: The matrix sub_U^V A
- **Minor**: When |U| = |V|, the determinant det(sub_U^V A) is called a minor of A
- **Principal minor**: When U = V, the minor det(sub_U^U A) is called a principal minor

## Implementation

In Mathlib, `Matrix.submatrix` takes functions for row and column selection.
For finite sets, we use the canonical order-preserving embedding `orderEmbOfFin`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.submatrixDet (def)
{R : Type u_1} → [CommRing R] → {n : ℕ} → Matrix (Fin n) (Fin n) R → (P Q : Finset (Fin n)) → P.card = Q.card → R

Body:
fun {R} [CommRing R] {n} A P Q h => (A.submatrix ⇑(P.orderEmbOfFin ⋯) ⇑(Q.orderEmbOfFin ⋯)).det

Docstring: Helper: Given P, Q with same cardinality, compute the determinant of the
submatrix of A restricted to rows P and columns Q. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.sigma_orderEmb_mem_of_imageFinset (theorem)
∀ {n : ℕ} (P Q : Finset (Fin n)) (σ : Equiv.Perm (Fin n)),
  AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → ∀ (i : Fin P.card), σ ((P.orderEmbOfFin ⋯) i) ∈ Q

Docstring: For σ with σ(P) = Q, the image of any element of P under σ lies in Q. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.sigma_orderEmb_compl_mem_of_imageFinset (theorem)
∀ {n : ℕ} (P Q : Finset (Fin n)) (σ : Equiv.Perm (Fin n)),
  AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → ∀ (i : Fin Pᶜ.card), σ ((Pᶜ.orderEmbOfFin ⋯) i) ∈ Qᶜ

Docstring: For σ with σ(P) = Q, the image of any element of Pᶜ under σ lies in Qᶜ. 

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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Compl.compl
{α : Type u_1} → [self : Compl α] → α → α

Docstring: Set / lattice complement 

Conventions for notations in identifiers:

 * The recommended spelling of `ᶜ` in identifiers is `compl`.

## BASE-LIBRARY REF BooleanAlgebra.toCompl
{α : Type u} → [self : BooleanAlgebra α] → Compl α

## BASE-LIBRARY REF Finset.booleanAlgebra
{α : Type u_1} → [Fintype α] → [DecidableEq α] → BooleanAlgebra (Finset α)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF OrderEmbedding
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Docstring: An order embedding is an embedding `f : α ↪ β` such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelEmbedding (≤) (≤)`. 

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

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

## BASE-LIBRARY REF Fin.instLinearOrder
{n : ℕ} → LinearOrder (Fin n)

## BASE-LIBRARY REF Finset.orderEmbOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ↪o α

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderEmbOfFin s h` is
the increasing bijection between `Fin k` and `s` as an order embedding into `α`. Here, `h` is a
proof that the cardinality of `s` is `k`. We use this instead of an embedding `Fin s.card ↪o α` to
avoid casting issues in further uses of this function. 

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


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Finset.decidableMem
{α : Type u_1} → [_h : DecidableEq α] → (a : α) → (s : Finset α) → Decidable (a ∈ s)

## BASE-LIBRARY REF instFunLikeOrderEmbedding
(α : Type u_6) → (β : Type u_7) → [inst : LE α] → [inst_1 : LE β] → FunLike (α ↪o β) α β

## BASE-LIBRARY REF OrderIso
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Docstring: An order isomorphism is an equivalence such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelIso (≤) (≤)`. 

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

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Subtype.instLE
{α : Type u} → [LE α] → {P : α → Prop} → LE (Subtype P)

## BASE-LIBRARY REF instFunLikeOrderIso
(α : Type u_6) → (β : Type u_7) → [inst : LE α] → [inst_1 : LE β] → FunLike (α ≃o β) α β

## BASE-LIBRARY REF OrderIso.symm
{α : Type u_2} → {β : Type u_3} → [inst : LE α] → [inst_1 : LE β] → α ≃o β → β ≃o α

Docstring: Inverse of an order isomorphism. 

## BASE-LIBRARY REF Finset.orderIsoOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ≃o ↥s

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderIsoOfFin s h`
is the increasing bijection between `Fin k` and `s` as an `OrderIso`. Here, `h` is a proof that
the cardinality of `s` is `k`. We use this instead of an iso `Fin s.card ≃o s` to avoid
casting issues in further uses of this function. 

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Function.Injective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called injective if `f x = f y` implies `x = y`. 

## BASE-LIBRARY REF Equiv.ofBijective
{α : Sort u} → {β : Sort v} → (f : α → β) → Function.Bijective f → α ≃ β

Docstring: If `f` is a bijective function, then its domain is equivalent to its codomain. 

## BASE-LIBRARY REF Function.Surjective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called surjective if every `b : β` is equal to `f a`
for some `a : α`. 

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF rfl
∀ {α : Sort u} {a : α}, a = a

Docstring: `rfl : a = a` is the unique constructor of the equality type. This is the
same as `Eq.refl` except that it takes `a` implicitly instead of explicitly.

This is a more powerful theorem than it may appear at first, because although
the statement of the theorem is `a = a`, Lean will allow anything that is
definitionally equal to that type. So, for instance, `2 + 2 = 4` is proven in
Lean by `rfl`, because both sides are the same up to definitional equality.


## INFORMAL STATEMENT
Round-trip properties

\leanhelper  The maps $\sigma \mapsto (\alpha _\sigma , \beta _\sigma )$ and $(\alpha ,\beta ) \mapsto \sigma _{(\alpha ,\beta )}$ are mutual inverses: 

\begin{enumerate} \item Extracting $\alpha $ from the permutation constructed from $(\alpha ,\beta )$ returns $\alpha $. 

\item Extracting $\beta $ from the permutation constructed from $(\alpha ,\beta )$ returns $\beta $. 

\item Constructing a permutation from the components $(\alpha _\sigma , \beta _\sigma )$ extracted from $\sigma $ returns $\sigma $. 

\end{enumerate}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.constructsigma
Construction of permutation from components

\leanhelper  Given $P,Q\subseteq [n]$ with $|P|=|Q|$ and permutations $\alpha \in S_k$, $\beta \in S_\ell $ (with $k=|P|$, $\ell =|\overline{P}|$), define $\sigma \in S_n$ by: 

\[  \sigma (p_i) = q_{\alpha (i)} \quad \text{and}\quad \sigma (p'_i) = q'_{\beta (i)}.  \]

 This is the inverse of the map $\sigma \mapsto (\alpha _\sigma ,\beta _\sigma )$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.imagefinset
def.det.imageFinset

\leanhelper  The \emph{image} of a finite subset $P \subseteq [n]$ under a permutation $\sigma \in S_n$ is $\sigma (P) = \{ \sigma (i) \mid i \in P\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.extract
Extraction of component permutations

\leanhelper  Let $P,Q\subseteq [n]$ with $|P|=|Q|=k$ and let $\sigma \in S_n$ satisfy $\sigma (P) = Q$. Write the elements of $P$ in increasing order as $p_1 < \cdots < p_k$, of $Q$ as $q_1 < \cdots < q_k$, of $\overline{P}$ as $p'_1 < \cdots < p'_\ell $, and of $\overline{Q}$ as $q'_1 < \cdots < q'_\ell $. 

Define $\alpha _\sigma \in S_k$ by $\sigma (p_i) = q_{\alpha _\sigma (i)}$ and $\beta _\sigma \in S_\ell $ by $\sigma (p'_i) = q'_{\beta _\sigma (i)}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.notations
def.perm.notations

Let $n \in \mathbb {N}$ and $\sigma \in S_n$. We introduce three notations for $\sigma $: 

\textbf{(a)} A \emph{two-line notation} of $\sigma $ means a $2 \times n$-array 

\[  \begin{pmatrix}  p_1 

&  p_2 

&  \cdots 

&  p_n 

\\ \sigma (p_1) 

&  \sigma (p_2) 

&  \cdots 

&  \sigma (p_n) 

\end{pmatrix},  \]

 where the entries $p_1, p_2, \ldots , p_n$ of the top row are the $n$ elements of $[n]$ in some order. Commonly, we pick $p_i = i$. 

\textbf{(b)} The \emph{one-line notation} (short, \emph{OLN}) of $\sigma $ means the $n$-tuple $(\sigma (1), \sigma (2), \ldots , \sigma (n))$. 

\textbf{(c)} The \emph{cycle digraph} of $\sigma $ is the directed graph with vertices $1, 2, \ldots , n$ and arcs $i \to \sigma (i)$ for all $i \in [n]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The three declarations exactly express the three listed round trips. `extractAlpha_constructSigma` concludes `extractAlpha ... (constructSigma ... \u03b1 \u03b2) h\u03c3 = \u03b1`; `extractBeta_constructSigma` analogously concludes equality with `\u03b2`; and `constructSigma_extract` concludes `constructSigma ... (extractAlpha ... \u03c3 h\u03c3) (extractBeta ... \u03c3 h\u03c3) = \u03c3`. Their binders match the informal setting: `P Q : Finset (Fin n)`, `hcard : P.card = Q.card`, component permutations on `Fin P.card` and `Fin P\u1d9c.card`, and, for extraction from an arbitrary `\u03c3`, the required condition `h\u03c3 : imageFinset \u03c3 P = Q`. The `h\u03c3` binders in the first two declarations are proof witnesses needed by the dependent signatures of `extractAlpha` and `extractBeta`; they do not impose a mathematically additional restriction, since `constructSigma` is defined by sending the ordered elements of `P` into `Q` via `\u03b1` and those of `P\u1d9c` into `Q\u1d9c` via `\u03b2`, exactly as in the informal construction. The use of `Fin n` rather than `[n]` is explicitly authorized by the informal convention."
}
## TARGET AlgebraicCombinatorics.FPS.essFinSum_add (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {ι : Type u_2} [DecidableEq ι] {f g : ι → R}
  (hf : AlgebraicCombinatorics.FPS.EssentiallyFinite f) (hg : AlgebraicCombinatorics.FPS.EssentiallyFinite g)
  (hfg : AlgebraicCombinatorics.FPS.EssentiallyFinite fun i => f i + g i),
  AlgebraicCombinatorics.FPS.essFinSum (fun i => f i + g i) hfg =
    AlgebraicCombinatorics.FPS.essFinSum f hf + AlgebraicCombinatorics.FPS.essFinSum g hg

Docstring: Additivity: the essentially finite sum of a sum is the sum of essentially finite sums 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.EssentiallyFinite (def)
{R : Type u_1} → [CommRing R] → {ι : Type u_2} → (ι → R) → Prop

Body:
fun {R} [CommRing R] {ι} f => EssentiallyFinite f

Docstring: A family is essentially finite if its support is finite.
(Definition def.infsum.essfin (a))

**This is an alias** for the canonical `EssentiallyFinite` defined in
`FPS/InfiniteProducts2.lean`. Both definitions are **definitionally equal**:
`{i | f i ≠ 0}.Finite` = `(Function.support f).Finite` by definition.

For the full API (including `_root_.EssentiallyFinite.add`, `_root_.EssentiallyFinite.neg`,
`_root_.EssentiallyFinite.toFinsupp`, etc.), see `FPS/InfiniteProducts2.lean`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.essFinSum (def)
{R : Type u_1} → [inst : CommRing R] → {ι : Type u_2} → (f : ι → R) → AlgebraicCombinatorics.FPS.EssentiallyFinite f → R

Body:
fun {R} [CommRing R] {ι} f hf => ∑ i ∈ Set.Finite.toFinset hf, f i

Docstring: The sum of an essentially finite family, defined as the finite sum over non-zero elements.
(Definition def.infsum.essfin (b)) 

## PROJECT DEPENDENCY EssentiallyFinite (def)
{I : Type u_2} → {M : Type u_3} → [Zero M] → (I → M) → Prop

Body:
fun {I} {M} [Zero M] f => (Function.support f).Finite

Docstring: A family `f : I → M` is essentially finite if all but finitely many values are zero.
This is equivalent to `f` having finite support.

(Definition def.fps.prodrule.ess-fin)

**Canonical definition**: This is the canonical, most general definition of `EssentiallyFinite`.
It is **definitionally equal** to:
- `AlgebraicCombinatorics.FPS.EssentiallyFinite` in `FPSDefinition.lean`
- `PowerSeries.EssentiallyFinite` in `Details/InfiniteProducts2.lean`

All use `{i | f i ≠ 0}.Finite` which equals `(Function.support f).Finite` by definition.
This version has the richest API in the `EssentiallyFinite` namespace. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


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

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## BASE-LIBRARY REF Function.support
{ι : Type u_1} → {M : Type u_3} → [Zero M] → (ι → M) → Set ι

Docstring: `support` of a function is the set of points `x` such that `f x ≠ 0`. 

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## INFORMAL STATEMENT
lem.fps.essFinSum.add

\leanhelper  The essentially finite sum distributes over addition: if $(a_i)_{i\in I}$ and $(b_i)_{i\in I}$ are essentially finite families, then $\sum _{i\in I}(a_i + b_i) = \sum _{i\in I} a_i + \sum _{i\in I} b_i$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint quantifies over essentially finite families in an arbitrary index set: \u201cif $(a_i)_{i\\in I}$ and $(b_i)_{i\\in I}$ are essentially finite families,\u201d with no decidable-equality restriction on $I$ and no commutative-ring hypothesis on $K$. The elaborated target instead has the added binders `[inst : CommRing R]` and `[DecidableEq \u03b9]`. In particular, `[DecidableEq \u03b9]` is not required by either referenced definition: `EssentiallyFinite` is `(Function.support f).Finite`, and `essFinSum` itself has no `DecidableEq` binder. It therefore genuinely narrows the index types rather than merely encoding the statement. The `CommRing R` restriction enters through both project dependencies `AlgebraicCombinatorics.FPS.EssentiallyFinite` and `essFinSum`; the additivity statement and finite sums only require suitable additive commutative-monoid structure, which is strictly weaker than a commutative ring and is all that the displayed blueprint operations demand. The extra `hfg : EssentiallyFinite (fun i => f i + g i)` is a redundant proof argument needed to feed the dependent definition of `essFinSum`; it follows from `hf` and `hg` and is not the decisive drift. To make the formalization faithful, remove `[DecidableEq \u03b9]` and generalize the two FPS dependencies (or use the root `EssentiallyFinite` and a correspondingly generalized sum) from `CommRing` to the additive structure required for finite sums."
}
## TARGET AlgebraicCombinatorics.FPS.essentiallyFinite_sub (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {ι : Type u_2} {f g : ι → R},
  AlgebraicCombinatorics.FPS.EssentiallyFinite f →
    AlgebraicCombinatorics.FPS.EssentiallyFinite g → AlgebraicCombinatorics.FPS.EssentiallyFinite fun i => f i - g i

Docstring: Subtraction of two essentially finite families is essentially finite.
(Delegates to `_root_.EssentiallyFinite.sub`) 

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

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF SubNegMonoid.toSub
{G : Type u} → [self : SubNegMonoid G] → Sub G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

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

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Function.support
{ι : Type u_1} → {M : Type u_3} → [Zero M] → (ι → M) → Set ι

Docstring: `support` of a function is the set of points `x` such that `f x ≠ 0`. 

## INFORMAL STATEMENT
lem.fps.essfin.sub

\leanhelper  The difference of two essentially finite families is essentially finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.essfinite
def.fps.infprod.essFinite

\leanhelper  A family $(k_i)_{i \in I}$ of natural numbers is \emph{essentially finite} if all but finitely many entries equal $0$, i.e., the set $\{ i \in I : k_i \neq 0\} $ is finite. This corresponds to $S^I_{\mathrm{fin}}$ in the source.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.sfini
def.fps.infprod.SfinI

\leanhelper  The set $S^I_{\mathrm{fin}}$ of \emph{essentially finite families} in $\prod _{i \in I} S_i$ is the set of all families $(k_i)_{i \in I}$ such that $k_i \in S_i$ for all $i$ and the family $(k_i)$ is essentially finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.prodrule.ess-fin
def.fps.prodrule.ess-fin

\textbf{(a)} A sequence $\left( k_{1},k_{2},k_{3},\ldots \right) $ is said to be \emph{essentially finite} if all but finitely many $i\in \left\{  1,2,3,\ldots \right\}  $ satisfy $k_{i}=0$. \medskip 

\textbf{(b)} A family $\left( k_{i}\right) _{i\in I}$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $k_{i}=0$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint definition fixes an essentially finite family here as \u201ca family $(k_i)_{i\\in I}$ of natural numbers\u201d whose nonzero support is finite. The target instead quantifies `\u2200 {R : Type u_1} [inst : CommRing R] ... {f g : \u03b9 \u2192 R}`. This does not cover the blueprint\u2019s natural-number families, since `\u2115` is not a `CommRing`; thus it is not merely a more general theorem. The restriction enters both through the target binder `[CommRing R]` and through the project alias `AlgebraicCombinatorics.FPS.EssentiallyFinite`, whose signature also requires `[CommRing R]`, despite the canonical `EssentiallyFinite` body needing only `[Zero M]`. To be faithful, the declaration could specialize to `f g : \u03b9 \u2192 \u2115` and use the canonical `EssentiallyFinite`, proving closure under natural-number subtraction; alternatively, its dependencies and algebraic assumptions could be generalized enough to include `\u2115`."
}
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

## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF SubNegMonoid
Type u → Type u

Docstring: A `SubNegMonoid` is an `AddMonoid` with unary `-` and binary `-` operations
satisfying `sub_eq_add_neg : ∀ a b, a - b = a + -b`.

The default for `sub` is such that `a - b = a + -b` holds by definition.

Adding `sub` as a field rather than defining `a - b := a + -b` allows us to
avoid certain classes of unification failures, for example:
Let `foo X` be a type with a `∀ X, Sub (Foo X)` instance but no
`∀ X, Neg (Foo X)`. Suppose we also have an instance
`∀ X [Cromulent X], AddGroup (Foo X)`. Then the `(-)` coming from
`AddGroup.sub` cannot be definitionally equal to the `(-)` coming from
`Foo.Sub`.

In the same way, adding a `zsmul` field makes it possible to avoid definitional failures
in diamonds. See the definition of `AddMonoid` and Note [forgetful inheritance] for more
explanations on this.


## BASE-LIBRARY REF AddGroup
Type u → Type u

Docstring: An `AddGroup` is an `AddMonoid` with a unary `-` satisfying `-a + a = 0`.

There is also a binary operation `-` such that `a - b = a + -b`,
with a default so that `a - b = a + -b` holds by definition.

Use `AddGroup.ofLeftAxioms` or `AddGroup.ofRightAxioms` to define an
additive group structure on a type with the minimum proof obligations.


## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocRing
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative ring. 

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF NonUnitalNonAssocRing.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocRing.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocCommRing
Type u → Type u

Docstring: A non-unital non-associative commutative ring is a `NonUnitalNonAssocRing` with commutative
multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing
Type u → Type u

Docstring: A non-unital commutative ring is a `NonUnitalRing` with commutative multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing.mul_comm
∀ {α : Type u} [self : NonUnitalCommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_1
∀ {α : Type u_1} [s : CommRing α] (a b : α), a - b = a + -b

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_2
∀ {α : Type u_1} [s : CommRing α] (a : α), Ring.zsmul 0 a = 0

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_3
∀ {α : Type u_1} [s : CommRing α] (n : ℕ) (a : α), Ring.zsmul (↑n.succ) a = Ring.zsmul (↑n) a + a

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_4
∀ {α : Type u_1} [s : CommRing α] (n : ℕ) (a : α), Ring.zsmul (Int.negSucc n) a = -Ring.zsmul (↑n.succ) a

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_5
∀ {α : Type u_1} [s : CommRing α] (a : α), -a + a = 0

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Body:
fun {α} s => Finite ↑s

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Function.support
{ι : Type u_1} → {M : Type u_3} → [Zero M] → (ι → M) → Set ι

Body:
fun {ι} {M} [Zero M] f => {x | f x ≠ 0}

Docstring: `support` of a function is the set of points `x` such that `f x ≠ 0`. 

## INFORMAL STATEMENT
lem.fps.essfin.sub

\leanhelper  The difference of two essentially finite families is essentially finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.prodrule.ess-fin
def.fps.prodrule.ess-fin

\textbf{(a)} A sequence $\left( k_{1},k_{2},k_{3},\ldots \right) $ is said to be \emph{essentially finite} if all but finitely many $i\in \left\{  1,2,3,\ldots \right\}  $ satisfy $k_{i}=0$. \medskip 

\textbf{(b)} A family $\left( k_{i}\right) _{i\in I}$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $k_{i}=0$.

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "[inst : CommRing R]",
      "severity": "minor",
      "bridge": "Generalize the coefficient type from a commutative ring to an additive group (or another structure whose subtraction has the usual zero law). The same finite-support argument applies: the support of i \u21a6 f i - g i is contained in the union of the finite supports of f and g. This is routine and essentially the same one-line use of the canonical `EssentiallyFinite.sub` lemma."
    }
  ],
  "justification": "The blueprint claims without a coefficient-ring restriction that \u201cThe difference of two essentially finite families is essentially finite,\u201d and its definition only characterizes essential finiteness by having finitely many nonzero entries. The formal signature instead begins `\u2200 {R : Type u_1} [inst : CommRing R] ...`, so it proves the result only for commutative-ring-valued families. After unfolding `AlgebraicCombinatorics.FPS.EssentiallyFinite`, the conclusion correctly says that `Function.support (fun i => f i - g i)` is finite. Thus the support notion and conclusion match exactly, but the unnecessary `CommRing` restriction prevents the theorem itself from covering the blueprint\u2019s unrestricted additive setting."
}
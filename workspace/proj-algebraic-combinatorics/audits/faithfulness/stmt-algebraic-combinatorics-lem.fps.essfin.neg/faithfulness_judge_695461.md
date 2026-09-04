## TARGET AlgebraicCombinatorics.FPS.essentiallyFinite_neg (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {ι : Type u_2} {f : ι → R},
  AlgebraicCombinatorics.FPS.EssentiallyFinite f → AlgebraicCombinatorics.FPS.EssentiallyFinite fun i => -f i

Docstring: Negation of an essentially finite family is essentially finite.
(Delegates to `_root_.EssentiallyFinite.neg`) 

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

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass
Type u_2 → Type u_2

Docstring: Typeclass for expressing that `-0 = 0`. 

## BASE-LIBRARY REF SubNegZeroMonoid
Type u_2 → Type u_2

Docstring: A `SubNegMonoid` where `-0 = 0`. 

## BASE-LIBRARY REF SubNegZeroMonoid.neg_zero
∀ {G : Type u_2} [self : SubNegZeroMonoid G], -0 = 0

## BASE-LIBRARY REF SubtractionMonoid
Type u → Type u

Docstring: A `SubtractionMonoid` is a `SubNegMonoid` with involutive negation and such that
`-(a + b) = -b + -a` and `a + b = 0 → -a = b`. 

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


## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid._proof_1
∀ {α : Type u_1} [inst : SubtractionMonoid α], -0 = 0

## BASE-LIBRARY REF SubtractionCommMonoid
Type u → Type u

Docstring: Commutative `SubtractionMonoid`. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF SubtractionMonoid.neg_neg
∀ {G : Type u} [self : SubtractionMonoid G] (x : G), - -x = x

## BASE-LIBRARY REF SubtractionMonoid.neg_add_rev
∀ {G : Type u} [self : SubtractionMonoid G] (a b : G), -(a + b) = -b + -a

## BASE-LIBRARY REF SubtractionMonoid.neg_eq_of_add
∀ {G : Type u} [self : SubtractionMonoid G] (a b : G), a + b = 0 → -a = b

Docstring: Despite the asymmetry of `neg_eq_of_add`, the symmetric version is true thanks to the
involutivity of negation. 

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF LieRing
Type v → Type v

Docstring: A Lie ring is an additive group with compatible product, known as the bracket, satisfying the
Jacobi identity. 

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Body:
fun {A} [inst : Ring A] =>
  { toAddCommGroup := inst.toAddCommGroup, toBracket := Ring.instBracket, add_lie := ⋯, lie_add := ⋯, lie_self := ⋯,
    leibniz_lie := ⋯ }

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

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
lem.fps.essfin.neg

\leanhelper  The negation of an essentially finite family is essentially finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "significant_divergence",
  "discrepancies": [
    {
      "root": "[inst : CommRing R]",
      "severity": "significant",
      "bridge": "The formal theorem only handles families valued in a commutative ring. To recover the unrestricted blueprint wording, one would need to prove the result for every value type K on which zero and unary negation are available. That is not derivable and is false without axioms relating negation to zero: if -0 \u2260 0, an identically zero family over an infinite index type has finite (empty) support, while its pointwise negation can have infinite support."
    }
  ],
  "justification": "The formal signature quantifies `\u2200 {R : Type u_1} [inst : CommRing R] ...`, whereas the blueprint says only, \u201cThe negation of an essentially finite family is essentially finite,\u201d and its definition describes a family in `K^I` without imposing any algebraic structure on `K`. The available library references confirm that `Neg` alone is merely an operator and that `-0 = 0` requires additional structure such as `NegZeroClass`. Thus the commutative-ring restriction is substantive rather than merely notational, and the theorem does not certify the claim at the generality fixed by the supplied informal material."
}
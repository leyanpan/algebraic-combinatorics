## TARGET AlgebraicCombinatorics.FPS.essFinSum_smul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {ι : Type u_2} {f : ι → R} (c : R)
  (hf : AlgebraicCombinatorics.FPS.EssentiallyFinite f)
  (hcf : AlgebraicCombinatorics.FPS.EssentiallyFinite fun i => c * f i),
  AlgebraicCombinatorics.FPS.essFinSum (fun i => c * f i) hcf = c * AlgebraicCombinatorics.FPS.essFinSum f hf

Docstring: Scalar multiplication: c * (∑ aᵢ) = ∑ (c * aᵢ) 

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

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Distrib
Type u_1 → Type u_1

Docstring: A typeclass stating that multiplication is left and right distributive
over addition. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

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

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Body:
fun {α} {s} h => s.toFinset

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## BASE-LIBRARY REF Function.support
{ι : Type u_1} → {M : Type u_3} → [Zero M] → (ι → M) → Set ι

Body:
fun {ι} {M} [Zero M] f => {x | f x ≠ 0}

Docstring: `support` of a function is the set of points `x` such that `f x ≠ 0`. 

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Body:
fun {α} s => Finite ↑s

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## INFORMAL STATEMENT
lem.fps.essFinSum.smul

\leanhelper  For a scalar $c\in K$ and an essentially finite family $(a_i)_{i\in I}$, $\sum _{i\in I} c\,  a_i = c\cdot \sum _{i\in I} a_i$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "(hcf : AlgebraicCombinatorics.FPS.EssentiallyFinite fun i => c * f i)",
      "severity": "minor",
      "bridge": "From `hf`, derive `hcf` routinely: if `f i = 0`, then `c * f i = c * 0 = 0`, so `Function.support (fun i => c * f i) \u2286 Function.support f`. A subset of the finite support supplied by `hf` is finite. Instantiate the formal theorem with this derived proof."
    }
  ],
  "justification": "The blueprint assumes only \u201can essentially finite family `(a_i)`,\u201d whereas the elaborated signature additionally requires `(hcf : ... EssentiallyFinite fun i => c * f i)`. After unfolding `EssentiallyFinite` as `(Function.support f).Finite`, this extra condition follows immediately from `hf` and multiplication by zero in a `CommRing`. The conclusion `essFinSum (fun i => c * f i) hcf = c * essFinSum f hf`, with `essFinSum` unfolded as the finite sum over the support, is exactly the claimed `\u2211 c a_i = c \u00b7 \u2211 a_i`."
}
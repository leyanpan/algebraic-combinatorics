## TARGET SymmetricFunctions.hsymmAlgHom (def) — ELABORATED SIGNATURE
(σ : Type u_1) →
  [Fintype σ] →
    [DecidableEq σ] →
      (R : Type u_2) →
        [inst : CommRing R] → (n : ℕ) → MvPolynomial (Fin n) R →ₐ[R] ↥(MvPolynomial.symmetricSubalgebra σ R)

Body:
fun σ [Fintype σ] [DecidableEq σ] R [CommRing R] n => MvPolynomial.aeval fun i => ⟨MvPolynomial.hsymm σ R (↑i + 1), ⋯⟩

Docstring: The `R`-algebra homomorphism from $R[x_1,\dots,x_n]$ to the symmetric subalgebra of
$R[\{x_i \mid i ∈ σ\}]$ sending $x_i$ to the $(i+1)$-th complete homogeneous symmetric polynomial.

This is analogous to `MvPolynomial.esymmAlgHom` which sends $x_i$ to $e_{i+1}$. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isAlgebra' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → Algebra K (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

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


## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF Subalgebra
(R : Type u) → (A : Type v) → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → Type v

Docstring: A subalgebra is a sub(semi)ring that includes the range of `algebraMap`. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF MvPolynomial.algebra
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → [Algebra R S₁] → Algebra R (MvPolynomial σ S₁)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Subalgebra.instSetLike
{R : Type u} →
  {A : Type v} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → SetLike (Subalgebra R A) A

## BASE-LIBRARY REF MvPolynomial.symmetricSubalgebra
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → Subalgebra R (MvPolynomial σ R)

Docstring: The subalgebra of symmetric `MvPolynomial`s. 

## BASE-LIBRARY REF Subalgebra.toSemiring
{R : Type u_1} →
  {A : Type u_2} →
    [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → (S : Subalgebra R A) → Semiring ↥S

## BASE-LIBRARY REF Subalgebra.algebra
{R : Type u} →
  {A : Type v} →
    [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → (S : Subalgebra R A) → Algebra R ↥S

## BASE-LIBRARY REF MvPolynomial.aeval
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring S₁] → [inst_2 : Algebra R S₁] → (σ → S₁) → MvPolynomial σ R →ₐ[R] S₁

Docstring: A map `σ → S₁` where `S₁` is an algebra over `R` generates an `R`-algebra homomorphism
from multivariate polynomials over `σ` to `S₁`. 

## BASE-LIBRARY REF Subalgebra.toCommSemiring
{R : Type u_1} →
  {A : Type u_2} →
    [inst : CommSemiring R] →
      [inst_1 : CommSemiring A] → [inst_2 : Algebra R A] → (S : Subalgebra R A) → CommSemiring ↥S

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF MvPolynomial.hsymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → [DecidableEq σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th complete homogeneous symmetric `MvPolynomial σ R`.
It is the sum over all the degree n monomials in `MvPolynomial σ R`. 

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

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## INFORMAL STATEMENT
def.sf.hsymm-alg-hom

\leanhelper  The $R$-algebra homomorphism from $R[x_1, \ldots , x_n]$ to the symmetric subalgebra sending $x_i$ to $h_{i+1}$. This is the analogous construction to the elementary symmetric algebra homomorphism (which sends $x_i$ to $e_{i+1}$), using complete homogeneous instead of elementary symmetric polynomials.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target has domain `MvPolynomial (Fin n) R`, which is the formal polynomial ring in `n` variables corresponding to informal `R[x_1, \\ldots, x_n]`, and codomain `\u21a5(MvPolynomial.symmetricSubalgebra \u03c3 R)`, exactly a symmetric subalgebra. Its body is `MvPolynomial.aeval fun i => \u27e8MvPolynomial.hsymm \u03c3 R (\u2191i + 1), \u22ef\u27e9`, so the variable indexed by `i : Fin n` is sent to the complete homogeneous symmetric polynomial `h_{i+1}`, matching \u201csending $x_i$ to $h_{i+1}$.\u201d The binders `[Fintype \u03c3]` and `[DecidableEq \u03c3]` are required by the supplied definition of `MvPolynomial.hsymm`, whose signature includes both; finiteness is also inherent in representing the stated complete homogeneous polynomial as the finite sum described by its docstring, while decidable equality is implementation-level encoding. The `[CommRing R]` setting agrees with the supplied project polynomial-ring definition `P`, which likewise assumes `[CommRing K]`. Thus these binders do not introduce a conflicting mathematical claim."
}
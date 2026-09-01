## TARGET SymmetricFunctions.omegaInvolution_det_hsymm (theorem) — ELABORATED SIGNATURE
∀ {σ : Type u_1} [inst : Fintype σ] [inst_1 : DecidableEq σ] {R : Type u_2} [inst_2 : CommRing R] {n m : ℕ}
  (hn : Fintype.card σ = n) (M : Matrix (Fin m) (Fin m) ↥(MvPolynomial.symmetricSubalgebra σ R)),
  (SymmetricFunctions.omegaInvolution hn) M.det = (M.map ⇑(SymmetricFunctions.omegaInvolution hn)).det

Docstring: The ω-involution applied to a determinant of h-entries gives a determinant of e-entries.

This is a key step in the proof of the second Jacobi-Trudi formula:
ω(det(h_{λᵢ - μⱼ - i + j})) = det(e_{λᵢ - μⱼ - i + j})

Note: This requires showing that ω commutes with taking determinants,
which follows from ω being an algebra homomorphism. 

## PROJECT DEPENDENCY SymmetricFunctions.omegaInvolution (def)
{σ : Type u_1} →
  [inst : Fintype σ] →
    [DecidableEq σ] →
      {R : Type u_2} →
        [inst_2 : CommRing R] →
          {n : ℕ} →
            Fintype.card σ = n → ↥(MvPolynomial.symmetricSubalgebra σ R) →ₐ[R] ↥(MvPolynomial.symmetricSubalgebra σ R)

Body:
fun {σ} [Fintype σ] [DecidableEq σ] {R} [CommRing R] {n} hn =>
  (SymmetricFunctions.hsymmAlgHom σ R n).comp ↑(MvPolynomial.esymmAlgEquiv σ R hn).symm

Docstring: The ω-involution on symmetric polynomials.

This is an algebra endomorphism of the symmetric subalgebra that swaps
elementary and complete homogeneous symmetric polynomials:
- ω(e_n) = h_n
- ω(h_n) = e_n

The definition uses the fundamental theorem of symmetric polynomials:
since the e_k generate the symmetric subalgebra, we define ω by
specifying ω(e_k) = h_k and extending algebraically.

Note: For this definition to work, we need `Fintype.card σ = n`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isAlgebra' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → Algebra K (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.hsymmAlgHom (def)
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

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF Subalgebra.toSemiring
{R : Type u_1} →
  {A : Type u_2} →
    [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → (S : Subalgebra R A) → Semiring ↥S

## BASE-LIBRARY REF Subalgebra.algebra
{R : Type u} →
  {A : Type v} →
    [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → (S : Subalgebra R A) → Algebra R ↥S

## BASE-LIBRARY REF AlgHom.funLike
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Semiring B] → [inst_3 : Algebra R A] → [inst_4 : Algebra R B] → FunLike (A →ₐ[R] B) A B

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Subalgebra.toCommRing
{R : Type u_1} →
  {A : Type u_2} →
    [inst : CommRing R] → [inst_1 : CommRing A] → [inst_2 : Algebra R A] → (S : Subalgebra R A) → CommRing ↥S

## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

## BASE-LIBRARY REF Matrix.map
{m : Type u_2} → {n : Type u_3} → {α : Type v} → {β : Type w} → Matrix m n α → (α → β) → Matrix m n β

Docstring: `M.map f` is the matrix obtained by applying `f` to each entry of the matrix `M`.

This is available in bundled forms as:
* `AddMonoidHom.mapMatrix`
* `LinearMap.mapMatrix`
* `RingHom.mapMatrix`
* `AlgHom.mapMatrix`
* `Equiv.mapMatrix`
* `AddEquiv.mapMatrix`
* `LinearEquiv.mapMatrix`
* `RingEquiv.mapMatrix`
* `AlgEquiv.mapMatrix`


## BASE-LIBRARY REF AlgHom.comp
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      {C : Type u₁} →
        [inst : CommSemiring R] →
          [inst_1 : Semiring A] →
            [inst_2 : Semiring B] →
              [inst_3 : Semiring C] →
                [inst_4 : Algebra R A] →
                  [inst_5 : Algebra R B] → [inst_6 : Algebra R C] → (B →ₐ[R] C) → (A →ₐ[R] B) → A →ₐ[R] C

Docstring: If `φ₁` and `φ₂` are `R`-algebra homomorphisms with the
domain of `φ₁` equal to the codomain of `φ₂`, then
`φ₁.comp φ₂` is the algebra homomorphism `x ↦ φ₁ (φ₂ x)`.


## BASE-LIBRARY REF AlgEquiv.toAlgHom
{R : Type uR} →
  {A₁ : Type uA₁} →
    {A₂ : Type uA₂} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A₁] →
          [inst_2 : Semiring A₂] → [inst_3 : Algebra R A₁] → [inst_4 : Algebra R A₂] → (A₁ ≃ₐ[R] A₂) → A₁ →ₐ[R] A₂

Docstring: Interpret an algebra equivalence as an algebra homomorphism.

This definition is included for symmetry with the other `to*Hom` projections.
The `simp` normal form is to use the coercion of the `AlgHomClass.coeTC` instance. 

## BASE-LIBRARY REF AlgEquiv.symm
{R : Type uR} →
  {A₁ : Type uA₁} →
    {A₂ : Type uA₂} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A₁] →
          [inst_2 : Semiring A₂] → [inst_3 : Algebra R A₁] → [inst_4 : Algebra R A₂] → (A₁ ≃ₐ[R] A₂) → A₂ ≃ₐ[R] A₁

Docstring: Algebra equivalences are symmetric. 

## BASE-LIBRARY REF MvPolynomial.esymmAlgEquiv
(σ : Type u_1) →
  (R : Type u_3) →
    {n : ℕ} →
      [inst : Fintype σ] →
        [inst_1 : CommRing R] →
          Fintype.card σ = n → MvPolynomial (Fin n) R ≃ₐ[R] ↥(MvPolynomial.symmetricSubalgebra σ R)

Docstring: If the cardinality of `σ` is `n`, then `esymmAlgHom σ R n` is an isomorphism. 

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

## INFORMAL STATEMENT
lem.sf.omega-det-hsymm

\leanhelper  The $\omega $-involution commutes with determinants: for any matrix $M$ over the symmetric subalgebra, $\omega (\det (M)) = \det (\omega (M))$, where $\omega (M)$ applies $\omega $ entry-wise. This is because $\omega $ is an algebra homomorphism, and $\det $ is a polynomial expression in the entries (involving only addition, multiplication, and negation).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.sf.kn
conv.sf.KN

Fix a commutative ring $K$. Fix an $N\in \mathbb {N}$. Throughout this chapter, we will keep $K$ and $N$ fixed. Let $S_N$ denote the symmetric group, i.e., the group of all permutations of $[N] := \{ 1,2,\ldots ,N\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.commring
def.alg.commring

A \emph{commutative ring} means a set $K$ equipped with three maps

\begin{align*}  \oplus &  :K\times K\rightarrow K,\\ \ominus &  :K\times K\rightarrow K,\\ \odot &  :K\times K\rightarrow K \end{align*}

 and two elements $\mathbf{0}\in K$ and $\mathbf{1}\in K$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in K$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in K$. 

\item \emph{Neutrality of zero:} We have $a\oplus \mathbf{0}=\mathbf{0}\oplus a=a$ for all $a\in K$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in K$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Commutativity of multiplication:} We have $a\odot b=b\odot a$ for all $a,b\in K$. 

\item \emph{Associativity of multiplication:} We have $a\odot \left( b\odot c\right) =\left( a\odot b\right) \odot c$ for all $a,b,c\in K$. 

\item \emph{Distributivity:} We have

\[  a\odot \left( b\oplus c\right) =\left( a\odot b\right) \oplus \left( a\odot c\right) \  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \left( a\oplus b\right) \odot c=\left( a\odot c\right) \oplus \left( b\odot c\right)  \]

 for all $a,b,c\in K$. 

\item \emph{Neutrality of one:} We have $a\odot \mathbf{1}=\mathbf{1}\odot a=a$ for all $a\in K$. 

\item \emph{Annihilation:} We have $a\odot \mathbf{0}=\mathbf{0}\odot a=\mathbf{0}$ for all $a\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\odot $ are called the \emph{addition}, the \emph{subtraction} and the \emph{multiplication} of the ring $K$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\odot $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\odot b=a\cdot b$ by $ab$. 

The elements $\mathbf{0}$ and $\mathbf{1}$ are called the \emph{zero} and the \emph{unity} (or the \emph{one}) of the ring $K$. We will simply call these elements $0$ and $1$ when confusion with the corresponding numbers is unlikely. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\odot $. These imply that the operation $\odot $ has higher precedence than $\oplus $ and $\ominus $, while the operations $\oplus $ and $\ominus $ are left-associative.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ps
def.sf.PS

\textbf{(a)} Let $\mathcal{P}$ be the polynomial ring $K[x_1, x_2, \ldots , x_N]$ in $N$ variables over $K$. This is not just a ring; it is a commutative $K$-algebra. \medskip 

\textbf{(b)} The symmetric group $S_N$ acts on the set $\mathcal{P}$ according to the formula 

\[  \sigma \cdot f = f[x_{\sigma (1)}, x_{\sigma (2)}, \ldots , x_{\sigma (N)}] \quad \text{for any } \sigma \in S_N \text{ and any } f \in \mathcal{P}.  \]

 Here, $f[a_1, a_2, \ldots , a_N]$ means the result of substituting $a_1, a_2, \ldots , a_N$ for the indeterminates $x_1, x_2, \ldots , x_N$ in a polynomial $f \in \mathcal{P}$. 

Roughly speaking, the group $S_N$ is thus acting on $\mathcal{P}$ by permuting variables: A permutation $\sigma \in S_N$ transforms a polynomial $f$ by substituting $x_{\sigma (i)}$ for each $x_i$. 

Note that this action of $S_N$ on $\mathcal{P}$ is a well-defined group action (as we will see in Proposition~ \ref{prop.sf.SN-acts} below). \medskip 

\textbf{(c)} A polynomial $f \in \mathcal{P}$ is said to be \emph{symmetric} if it satisfies 

\[  \sigma \cdot f = f \quad \text{for all } \sigma \in S_N.  \]

\textbf{(d)} We let $\mathcal{S}$ be the set of all symmetric polynomials $f \in \mathcal{P}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal conclusion exactly expresses entrywise commutation with determinant: ` (omegaInvolution hn) M.det = (M.map \u21d1(omegaInvolution hn)).det`, matching \u201c`\u03c9(det(M)) = det(\u03c9(M))`, where `\u03c9(M)` applies `\u03c9` entry-wise.\u201d The matrix binder `M : Matrix (Fin m) (Fin m) \u21a5(MvPolynomial.symmetricSubalgebra \u03c3 R)` ranges over arbitrary square matrices of arbitrary natural size `m` over the symmetric subalgebra. The assumptions `[CommRing R]`, `[Fintype \u03c3]`, and `hn : Fintype.card \u03c3 = n` supply the blueprint\u2019s commutative coefficient ring and finite number of variables; `[DecidableEq \u03c3]` is an implementation requirement for the supplied definition of complete homogeneous symmetric polynomials, not a substantive mathematical restriction. Moreover, `omegaInvolution hn` is an `R`-algebra endomorphism by its declared type, consistent with the stated reason that \u03c9 preserves the ring operations used by the determinant. Quantifying over arbitrary `R`, `\u03c3`, `n`, and `m` is at least as general as the blueprint\u2019s fixed `K` and `N` setting."
}
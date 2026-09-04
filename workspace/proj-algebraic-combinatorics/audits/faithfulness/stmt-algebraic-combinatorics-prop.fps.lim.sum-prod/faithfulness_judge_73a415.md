## TARGET PowerSeries.coeffStabilizesTo_mul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {f g : ℕ → PowerSeries K} {lf lg : PowerSeries K},
  PowerSeries.CoeffStabilizesTo f lf →
    PowerSeries.CoeffStabilizesTo g lg → PowerSeries.CoeffStabilizesTo (fun i => f i * g i) (lf * lg)

Docstring: Limits respect multiplication.
(Proposition 7.5.5, label: prop.fps.lim.sum-prod) 

## TARGET PowerSeries.coeffStabilizesTo_add (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {f g : ℕ → PowerSeries K} {lf lg : PowerSeries K},
  PowerSeries.CoeffStabilizesTo f lf →
    PowerSeries.CoeffStabilizesTo g lg → PowerSeries.CoeffStabilizesTo (fun i => f i + g i) (lf + lg)

Docstring: Limits respect addition.
(Proposition 7.5.5, label: prop.fps.lim.sum-prod) 

## PROJECT DEPENDENCY PowerSeries.CoeffStabilizesTo (def)
{K : Type u_1} → [CommRing K] → (ℕ → PowerSeries K) → PowerSeries K → Prop

Body:
fun {K} [CommRing K] f lim =>
  ∀ (n : ℕ), Seq.StabilizesTo (fun i => (PowerSeries.coeff n) (f i)) ((PowerSeries.coeff n) lim)

Docstring: A sequence of FPSs `(f_i)_{i ∈ ℕ}` coefficientwise stabilizes to `f` if for each `n ∈ ℕ`,
the sequence `([x^n] f_i)_{i ∈ ℕ}` stabilizes to `[x^n] f`.

This is the notion of convergence in the product topology where each factor `K`
has the discrete topology.
(Definition 7.5.2, label: def.fps.lim.coeff-stab) 

## PROJECT DEPENDENCY Seq.StabilizesTo (def)
{K : Type u_1} → (ℕ → K) → K → Prop

Body:
fun {K} a lim => ∃ N, ∀ i ≥ N, a i = lim

Docstring: A sequence `(a_i)_{i ∈ ℕ}` stabilizes to `a` if there exists `N` such that
for all `i ≥ N`, we have `a_i = a`.

This is the notion of convergence in the discrete topology.
(Definition 7.5.1, label: def.fps.lim.stab) 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF MvPowerSeries.instMul
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → Mul (MvPowerSeries σ R)

Body:
fun {σ} {R} [Semiring R] =>
  { mul := fun φ ψ n => ∑ p ∈ Finset.antidiagonal n, (MvPowerSeries.coeff p.1) φ * (MvPowerSeries.coeff p.2) ψ }

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

Body:
{ toMul := instMulNat, toZero := Nat.instAddMonoid.toAddZeroClass.toZero, zero_mul := Nat.zero_mul,
  mul_zero := Nat.mul_zero }

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset.HasAntidiagonal.antidiagonal
{A : Type u_1} → {inst : AddMonoid A} → [self : Finset.HasAntidiagonal A] → A → Finset (A × A)

Body:
fun A {inst} [self : Finset.HasAntidiagonal A] => self.1

Docstring: The antidiagonal of an element `n` is the finset of pairs `(i, j)` such that `i + j = n`. 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

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

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_1
∀ {α : Type u_1} [s : CommRing α] (a b : α), a - b = a + -b

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

Body:
fun {R} [CommRing R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries.instCommRing
{σ : Type u_1} → {R : Type u_2} → [CommRing R] → CommRing (MvPowerSeries σ R)

Body:
fun {σ} {R} [CommRing R] =>
  let __src := inferInstanceAs (CommSemiring (MvPowerSeries σ R));
  let __src_1 := inferInstanceAs (AddCommGroup (MvPowerSeries σ R));
  { toSemiring := __src.toSemiring, toNeg := __src_1.toNeg, toSub := __src_1.toSub, sub_eq_add_neg := ⋯,
    zsmul := SubNegMonoid.zsmul, zsmul_zero' := ⋯, zsmul_succ' := ⋯, zsmul_neg' := ⋯, neg_add_cancel := ⋯,
    toIntCast := MvPowerSeries.instRing.toAddGroupWithOne.toIntCast, intCast_ofNat := ⋯, intCast_negSucc := ⋯,
    mul_comm := ⋯ }

## BASE-LIBRARY REF LinearMap
{R : Type u_14} →
  {S : Type u_15} →
    [inst : Semiring R] →
      [inst_1 : Semiring S] →
        (R →+* S) →
          (M : Type u_16) →
            (M₂ : Type u_17) →
              [inst_2 : AddCommMonoid M] →
                [inst_3 : AddCommMonoid M₂] → [_root_.Module R M] → [_root_.Module S M₂] → Type (max u_16 u_17)

Docstring: A map `f` between an `R`-module and an `S`-module over a ring homomorphism `σ : R →+* S`
is semilinear if it satisfies the two properties `f (x + y) = f x + f y` and
`f (c • x) = (σ c) • f x`. Elements of `LinearMap σ M M₂` (available under the notation
`M →ₛₗ[σ] M₂`) are bundled versions of such maps. For plain linear maps (i.e. for which
`σ = RingHom.id R`), the notation `M →ₗ[R] M₂` is available. An unbundled version of plain linear
maps is available with the predicate `IsLinearMap`, but it should be avoided most of the time. 

## BASE-LIBRARY REF RingHom.id
(α : Type u_5) → [inst : NonAssocSemiring α] → α →+* α

Body:
fun α [NonAssocSemiring α] => { toFun := id, map_one' := ⋯, map_mul' := ⋯, map_zero' := ⋯, map_add' := ⋯ }

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

Body:
fun {R} [AddCommMonoid R] => id inferInstance

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF MvPowerSeries.instAddCommMonoid
{σ : Type u_1} → {R : Type u_2} → [AddCommMonoid R] → AddCommMonoid (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddCommMonoid R] => Pi.addCommMonoid

## BASE-LIBRARY REF PowerSeries.instModule
{R : Type u_1} →
  {A : Type u_2} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (PowerSeries A)

Body:
fun {R} {A} [Semiring R] [AddCommMonoid A] [_root_.Module R A] => id inferInstance

## BASE-LIBRARY REF Module
(R : Type u) → (M : Type v) → [Semiring R] → [AddCommMonoid M] → Type (max u v)

Docstring: A module is a generalization of vector spaces to a scalar semiring.
It consists of a scalar semiring `R` and an additive monoid of "vectors" `M`,
connected by a "scalar multiplication" operation `r • x : M`
(where `r : R` and `x : M`) with some natural associativity and
distributivity axioms similar to those on a ring. 

## BASE-LIBRARY REF MvPowerSeries.instModule
{σ : Type u_1} →
  {R : Type u_2} →
    {A : Type u_3} →
      [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (MvPowerSeries σ A)

Body:
fun {σ} {R} {A} [Semiring R] [AddCommMonoid A] [_root_.Module R A] => Pi.module (σ →₀ ℕ) (fun a => A) R

## BASE-LIBRARY REF Semiring.toModule._proof_1
∀ {R : Type u_1} [inst : Semiring R] (a : R), a * 0 = 0

## BASE-LIBRARY REF Semiring.toModule._proof_2
∀ {R : Type u_1} [inst : Semiring R] (a b c : R), a * (b + c) = a * b + a * c

## BASE-LIBRARY REF Semiring.toModule._proof_3
∀ {R : Type u_1} [inst : Semiring R] (a b c : R), (a + b) * c = a * c + b * c

## BASE-LIBRARY REF Semiring.toModule._proof_4
∀ {R : Type u_1} [inst : Semiring R] (a : R), 0 * a = 0

## BASE-LIBRARY REF LinearMap.instFunLike
{R : Type u_1} →
  {S : Type u_5} →
    {M : Type u_8} →
      {M₃ : Type u_11} →
        [inst : Semiring R] →
          [inst_1 : Semiring S] →
            [inst_2 : AddCommMonoid M] →
              [inst_3 : AddCommMonoid M₃] →
                [inst_4 : _root_.Module R M] →
                  [inst_5 : _root_.Module S M₃] → {σ : R →+* S} → FunLike (M →ₛₗ[σ] M₃) M M₃

Body:
fun {R} {S} {M} {M₃} [Semiring R] [Semiring S] [AddCommMonoid M] [AddCommMonoid M₃] [_root_.Module R M]
    [_root_.Module S M₃] {σ} =>
  { coe := fun f => f.toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF LinearMap.instFunLike._proof_1
∀ {R : Type u_3} {S : Type u_4} {M : Type u_2} {M₃ : Type u_1} [inst : Semiring R] [inst_1 : Semiring S]
  [inst_2 : AddCommMonoid M] [inst_3 : AddCommMonoid M₃] [inst_4 : _root_.Module R M] [inst_5 : _root_.Module S M₃]
  {σ : R →+* S} (f g : M →ₛₗ[σ] M₃), (fun f => f.toFun) f = (fun f => f.toFun) g → f = g

## BASE-LIBRARY REF PowerSeries.coeff
{R : Type u_1} → [inst : Semiring R] → ℕ → PowerSeries R →ₗ[R] R

Body:
fun {R} [Semiring R] n => MvPowerSeries.coeff fun₀ | () => n

Docstring: The `n`th coefficient of a formal power series. 

## BASE-LIBRARY REF Exists
{α : Sort u} → (α → Prop) → Prop

Docstring: Existential quantification. If `p : α → Prop` is a predicate, then `∃ x : α, p x`
asserts that there is some `x` of type `α` such that `p x` holds.
To create an existential proof, use the `exists` tactic,
or the anonymous constructor notation `⟨x, h⟩`.
To unpack an existential, use `cases h` where `h` is a proof of `∃ x : α, p x`,
or `let ⟨x, hx⟩ := h` where `.

Because Lean has proof irrelevance, any two proofs of an existential are
definitionally equal. One consequence of this is that it is impossible to recover the
witness of an existential from the mere fact of its existence.
For example, the following does not compile:
```
example (h : ∃ x : Nat, x = x) : Nat :=
  let ⟨x, _⟩ := h  -- fail, because the goal is `Nat : Type`
  x
```
The error message `recursor 'Exists.casesOn' can only eliminate into Prop` means
that this only works when the current goal is another proposition:
```
example (h : ∃ x : Nat, x = x) : True :=
  let ⟨x, _⟩ := h  -- ok, because the goal is `True : Prop`
  trivial
```


## BASE-LIBRARY REF Nat.le
ℕ → ℕ → Prop

Docstring: Non-strict, or weak, inequality of natural numbers, usually accessed via the `≤` operator.


## INFORMAL STATEMENT
prop.fps.lim.sum-prod

Assume that $\left( f_{i}\right) _{i\in \mathbb {N}}$ and $\left( g_{i}\right) _{i\in \mathbb {N}}$ are two sequences of FPSs, and that $f$ and $g$ are two FPSs such that

\[  \lim \limits _{i\rightarrow \infty }f_{i}=f\  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \lim \limits _{i\rightarrow \infty }g_{i}=g.  \]

 Then, 

\[  \lim \limits _{i\rightarrow \infty }\left( f_{i}+g_{i}\right) =f+g\  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \lim \limits _{i\rightarrow \infty }\left( f_{i}g_{i}\right) =fg.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.coeff-stab
def.fps.lim.coeff-stab

Let $\left( f_{i}\right) _{i\in \mathbb {N}}\in K\left[ \left[ x\right] \right] ^{\mathbb {N}}$ be a sequence of FPSs over $K$. Let $f\in K\left[ \left[ x\right] \right] $ be an FPS. 

We say that $\left( f_{i}\right) _{i\in \mathbb {N}}$ \emph{coefficientwise stabilizes to }$f$ if for each $n\in \mathbb {N}$,

\[  \text{the sequence }\left( \left[ x^{n}\right] f_{i}\right) _{i\in \mathbb {N}}\text{ stabilizes to }\left[ x^{n}\right] f.  \]

If $f_{i}$ coefficientwise stabilizes to $f$ as $i\rightarrow \infty $, then we write $\lim \limits _{i\rightarrow \infty }f_{i}=f$ and say that $f$ is the \emph{limit} of $\left( f_{i}\right) _{i\in \mathbb {N}}$. This is legitimate, because $f$ is uniquely determined by the sequence $\left( f_{i}\right) _{i\in \mathbb {N}}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.stab
def.fps.lim.stab

Let $\left( a_{i}\right) _{i\in \mathbb {N}}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K^{\mathbb {N}}$ be a sequence of elements of $K$. Let $a\in K$. 

We say that the sequence $\left( a_{i}\right) _{i\in \mathbb {N}}$ \emph{stabilizes to }$a$ if there exists some $N\in \mathbb {N}$ such that

\[  \text{all integers }i\geq N\text{ satisfy }a_{i}=a.  \]

If $a_{i}$ stabilizes to $a$ as $i\rightarrow \infty $, then we write $\lim \limits _{i\rightarrow \infty }a_{i}=a$ and say that $a$ is the \emph{limit} (or \emph{eventual value}) of $\left( a_{i}\right) _{i\in \mathbb {N}}$. This is legitimate, since $a$ is uniquely determined by the sequence $\left( a_{i}\right) _{i\in \mathbb {N}}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.ops
def.fps.ops

\textbf{(a)} The \emph{sum} of two FPSs $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}+b_{0},\  \  a_{1}+b_{1},\  \  a_{2}+b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}+\mathbf{b}$. \medskip 

\textbf{(b)} The \emph{difference} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}-b_{0},\  \  a_{1}-b_{1},\  \  a_{2}-b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}-\mathbf{b}$. \medskip 

\textbf{(c)} If $\lambda \in K$ and if $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ is an FPS, then we define an FPS 

\[  \lambda \mathbf{a}:=\left(\lambda a_{0},\lambda a_{1},\lambda a_{2},\ldots \right).  \]

\textbf{(d)} The \emph{product} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS $\left(c_{0},c_{1},c_{2},\ldots \right)$, where 

\begin{align*}  c_{n} &  =\sum _{i=0}^{n}a_{i}b_{n-i}=\sum _{\substack {\left(i,j\right) \in \mathbb {N}^{2};\\ \begin{bgroup} i+j=n

\end{bgroup}}}a_{i}b_{j}\\ &  =a_{0}b_{n}+a_{1}b_{n-1}+a_{2}b_{n-2}+\cdots +a_{n}b_{0}\  \  \  \  \  \  \  \  \  \  \text{for each }n\in \mathbb {N}. \end{align*}

 This product is denoted by $\mathbf{a}\cdot \mathbf{b}$ or just by $\mathbf{ab}$. \medskip 

\textbf{(e)} For each $a\in K$, we define $\underline{a}$ to be the FPS $\left(a,0,0,0,\ldots \right)$. An FPS of the form $\underline{a}$ for some $a\in K$ (that is, an FPS $\left(a_{0},a_{1},a_{2},\ldots \right)$ satisfying $a_{1}=a_{2}=a_{3}=\cdots =0$) is said to be \emph{constant}. \medskip 

\textbf{(f)} The set of all FPSs (in $1$ indeterminate over $K$) is denoted $K\left[\left[x\right]\right]$.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The two declarations collectively assert exactly the two conclusions of the blueprint. Both assume `PowerSeries.CoeffStabilizesTo f lf` and `PowerSeries.CoeffStabilizesTo g lg`, matching \u201clim f_i = f\u201d and \u201clim g_i = g\u201d. The addition theorem concludes `PowerSeries.CoeffStabilizesTo (fun i => f i + g i) (lf + lg)`, matching \u201clim (f_i + g_i) = f + g\u201d; the multiplication theorem analogously concludes `PowerSeries.CoeffStabilizesTo (fun i => f i * g i) (lf * lg)`, matching \u201clim (f_i g_i) = fg\u201d. Unfolding `PowerSeries.CoeffStabilizesTo` and `Seq.StabilizesTo` gives precisely eventual stabilization of every coefficient as specified informally. Lean\u2019s `PowerSeries K = MvPowerSeries Unit K` is a faithful encoding of sequences indexed by \u2115, addition is coefficientwise, and the multiplication body sums over the antidiagonal, matching the informal Cauchy product over pairs with indices summing to n. Splitting the informal conjunction into two theorems does not weaken it."
}
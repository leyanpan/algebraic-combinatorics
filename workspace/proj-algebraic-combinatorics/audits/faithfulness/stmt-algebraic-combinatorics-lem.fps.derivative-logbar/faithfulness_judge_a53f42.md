## TARGET PowerSeries.derivative_logbar (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] [inst_1 : Algebra ℚ K],
  (PowerSeries.derivative K) (PowerSeries.logbar K) = PowerSeries.invOnePlusX K

Docstring: The derivative of `logbar` is `invOnePlusX`. This is part of the proof of
Proposition 7.8.3 (prop.fps.exp-log-der). 

## PROJECT DEPENDENCY PowerSeries.logbar (def)
(K : Type u_1) → [inst : CommRing K] → [Algebra ℚ K] → PowerSeries K

Body:
fun K [CommRing K] [Algebra ℚ K] => PowerSeries.mk fun n => if n = 0 then 0 else (algebraMap ℚ K) ((-1) ^ (n - 1) / ↑n)

Docstring: The logarithm series `logbar = ∑_{n≥1} (-1)^{n-1}/n · x^n`, which is the Mercator series
for `log(1+x)`. This is `\overline{\log}` in Definition 7.8.2 (def.fps.exp-log). 

## PROJECT DEPENDENCY PowerSeries.invOnePlusX (def)
(K : Type u_1) → [inst : CommRing K] → [Algebra ℚ K] → PowerSeries K

Body:
fun K [CommRing K] [Algebra ℚ K] => PowerSeries.mk fun n => (algebraMap ℚ K) ((-1) ^ n)

Docstring: The series `(1+x)⁻¹ = ∑_{n≥0} (-1)^n x^n`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF Rat
Type

Docstring: Rational numbers, implemented as a pair of integers `num / den` such that the
denominator is positive and the numerator and denominator are coprime.


## BASE-LIBRARY REF Rat.commSemiring
CommSemiring ℚ

Body:
inferInstance

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Rat.commRing
CommRing ℚ

Body:
let __spread.0 := Rat.addCommGroup;
let __spread.1 := Rat.commMonoid;
{ toAddMonoid := __spread.0.toAddMonoid, add_comm := ⋯, toMul := __spread.1.toMul, left_distrib := Rat.mul_add,
  right_distrib := Rat.add_mul, zero_mul := Rat.zero_mul, mul_zero := Rat.mul_zero, mul_assoc := Rat.commRing._proof_1,
  toOne := __spread.1.toOne, one_mul := Rat.commRing._proof_5, mul_one := Rat.commRing._proof_6,
  natCast := fun n => ↑↑n, natCast_zero := Rat.commRing._proof_7, natCast_succ := ⋯, npow := Monoid.npow,
  npow_zero := Rat.commRing._proof_8, npow_succ := Rat.commRing._proof_9, toNeg := __spread.0.t …

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Derivation
(R : Type u_1) →
  (A : Type u_2) →
    (M : Type u_3) →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring A] →
          [inst_2 : AddCommMonoid M] → [Algebra R A] → [_root_.Module A M] → [_root_.Module R M] → Type (max u_2 u_3)

Docstring: `D : Derivation R A M` is an `R`-linear map from `A` to `M` that satisfies the `leibniz`
equality. We also require that `D 1 = 0`. See `Derivation.mk'` for a constructor that deduces this
assumption from the Leibniz rule when `M` is cancellative.

TODO: update this when bimodules are defined. 

## BASE-LIBRARY REF PowerSeries.instCommSemiring
{R : Type u_1} → [CommSemiring R] → CommSemiring (PowerSeries R)

Body:
fun {R} [CommSemiring R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.instCommSemiring
{σ : Type u_1} → {R : Type u_2} → [CommSemiring R] → CommSemiring (MvPowerSeries σ R)

Body:
fun {σ} {R} [CommSemiring R] =>
  let __src :=
    have this := inferInstance;
    this;
  { toSemiring := __src, mul_comm := ⋯ }

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonAssocSemiring
Type u → Type u

Docstring: A unital but not-necessarily-associative semiring. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF PowerSeries.instAlgebra
{R : Type u_1} →
  {A : Type u_2} → [inst : Semiring A] → [inst_1 : CommSemiring R] → [Algebra R A] → Algebra R (PowerSeries A)

Body:
fun {R} {A} [Semiring A] [CommSemiring R] [Algebra R A] => id inferInstance

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

Body:
fun {R} [Semiring R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries.instAlgebra
{σ : Type u_1} →
  {R : Type u_2} →
    {A : Type u_3} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → Algebra R (MvPowerSeries σ A)

Body:
fun {σ} {R} {A} [CommSemiring R] [Semiring A] [Algebra R A] =>
  { toSMul := DistribMulAction.toDistribSMul.toSMul,
    algebraMap := (MvPowerSeries.map (algebraMap R A)).comp MvPowerSeries.C, commutes' := ⋯, smul_def' := ⋯ }

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF Semiring.toModule._proof_1
∀ {R : Type u_1} [inst : Semiring R] (a : R), a * 0 = 0

## BASE-LIBRARY REF Semiring.toModule._proof_2
∀ {R : Type u_1} [inst : Semiring R] (a b c : R), a * (b + c) = a * b + a * c

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

## BASE-LIBRARY REF Derivation.instFunLike
{R : Type u_1} →
  {A : Type u_2} →
    {M : Type u_4} →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring A] →
          [inst_2 : AddCommMonoid M] →
            [inst_3 : Algebra R A] →
              [inst_4 : _root_.Module A M] → [inst_5 : _root_.Module R M] → FunLike (Derivation R A M) A M

Body:
fun {R} {A} {M} [CommSemiring R] [CommSemiring A] [AddCommMonoid M] [Algebra R A] [_root_.Module A M]
    [_root_.Module R M] =>
  { coe := fun D => (↑D).toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF RingHom.id
(α : Type u_5) → [inst : NonAssocSemiring α] → α →+* α

Body:
fun α [NonAssocSemiring α] => { toFun := id, map_one' := ⋯, map_mul' := ⋯, map_zero' := ⋯, map_add' := ⋯ }

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF Derivation.instFunLike._proof_1
∀ {R : Type u_3} {A : Type u_1} {M : Type u_2} [inst : CommSemiring R] [inst_1 : CommSemiring A]
  [inst_2 : AddCommMonoid M] [inst_3 : Algebra R A] [inst_4 : _root_.Module A M] [inst_5 : _root_.Module R M]
  (D1 D2 : Derivation R A M), (fun D => (↑D).toFun) D1 = (fun D => (↑D).toFun) D2 → D1 = D2

## BASE-LIBRARY REF PowerSeries.derivative
(R : Type u_1) → [inst : CommSemiring R] → Derivation R (PowerSeries R) (PowerSeries R)

Body:
fun R [CommSemiring R] =>
  { toFun := PowerSeries.derivativeFun, map_add' := ⋯, map_smul' := ⋯, map_one_eq_zero' := ⋯, leibniz' := ⋯ }

Docstring: The formal derivative of a formal power series 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Body:
fun {α} c [h : Decidable c] t e => Decidable.casesOn h (fun x => e) fun x => t

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Nat.decEq
(n m : ℕ) → Decidable (n = m)

Body:
fun n m =>
  match h : n.beq m with
  | true => isTrue ⋯
  | false => isFalse ⋯

Docstring: A decision procedure for equality of natural numbers, usually accessed via the `DecidableEq Nat`
instance.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
 * `Nat.decEq 5 5 = isTrue rfl`
 * `(if 3 = 4 then "yes" else "no") = "no"`
 * `show 12 = 12 by decide`


## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.zero
{α : Type u} → [self : Zero α] → α

Body:
fun α [self : Zero α] => self.1

Docstring: The zero element of the type. 

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

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

Body:
fun {α} {β} {x} {x_1} => { coe := fun f => (↑↑f).toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF RingHom.instFunLike._proof_1
∀ {α : Type u_1} {β : Type u_2} {x : NonAssocSemiring α} {x_1 : NonAssocSemiring β} (f g : α →+* β),
  (fun f => (↑↑f).toFun) f = (fun f => (↑↑f).toFun) g → f = g

## BASE-LIBRARY REF algebraMap
(R : Type u) → (A : Type v) → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → R →+* A

Body:
fun R A [CommSemiring R] [Semiring A] [Algebra R A] => Algebra.algebraMap

Docstring: Embedding `R →+* A` given by `Algebra` structure. 

## BASE-LIBRARY REF Div
Type u → Type u

Docstring: The homogeneous version of `HDiv`: `a / b : α` where `a b : α`. 

## BASE-LIBRARY REF Div.div
{α : Type u} → [self : Div α] → α → α → α

Body:
fun α [self : Div α] => self.1

Docstring: `a / b` computes the result of dividing `a` by `b`. See `HDiv`. 

## BASE-LIBRARY REF Rat.instDiv
Div ℚ

Body:
{ div := Rat.div }

Docstring: Division of rational numbers. Note: `div a 0 = 0`.  Written with a separate function `Rat.div`
as a wrapper so that the definition is not unfolded at `.instance` transparency. 

## BASE-LIBRARY REF Pow
Type u → Type v → Type (max u v)

Docstring: The homogeneous version of `HPow`: `a ^ b : α` where `a : α`, `b : β`.
(The right argument is not the same as the left since we often want this even
in the homogeneous case.)

Types can choose to subscribe to particular defaulting behavior by providing
an instance to either `NatPow` or `HomogeneousPow`:
- `NatPow` is for types whose exponents is preferentially a `Nat`.
- `HomogeneousPow` is for types whose base and exponent are preferentially the same.


## BASE-LIBRARY REF Pow.pow
{α : Type u} → {β : Type v} → [self : Pow α β] → α → β → α

Body:
fun α β [self : Pow α β] => self.1

Docstring: `a ^ b` computes `a` to the power of `b`. See `HPow`. 

## BASE-LIBRARY REF Rat.instPowNat
Pow ℚ ℕ

Body:
{ pow := Rat.pow }

## BASE-LIBRARY REF Rat.pow
ℚ → ℕ → ℚ

Body:
fun q n => { num := q.num ^ n, den := q.den ^ n, den_nz := ⋯, reduced := ⋯ }

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Rat.instNeg
Neg ℚ

Body:
{ neg := Rat.neg }

## BASE-LIBRARY REF Rat.neg
ℚ → ℚ

Body:
fun a => { num := -a.num, den := a.den, den_nz := ⋯, reduced := ⋯ }

Docstring: Negation of rational numbers. 

## BASE-LIBRARY REF Rat.instOfNat
{n : ℕ} → OfNat ℚ n

Body:
fun {n} => { ofNat := ↑n }

## BASE-LIBRARY REF Rat.instNatCast
NatCast ℚ

Body:
{ natCast := fun n => Rat.ofInt ↑n }

## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF instSubNat
Sub ℕ

Body:
{ sub := Nat.sub }

Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Nat.sub
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, 0 => fun x => a
        | a, b.succ => fun x => (x.1 a).pred)
        f)
    x

Docstring: Subtraction of natural numbers, truncated at `0`. Usually used via the `-` operator.

If a result would be less than zero, then the result is zero.

This definition is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
* `5 - 3 = 2`
* `8 - 2 = 6`
* `8 - 8 = 0`
* `8 - 20 = 0`


Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## INFORMAL STATEMENT
Derivative of

\leanhelper  We have $\overline{\log }' = \iota = (1+x)^{-1}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.issummable
def.fps.lim.isSummable

\leanhelper  A family $(f_n)_{n \in \mathbb {N}}$ of FPSs is \emph{summable} if for each $n \in \mathbb {N}$, the set $\{ i \in \mathbb {N} : [x^n] f_i \neq 0\} $ is finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.tsum
def.fps.lim.tsum

\leanhelper  The \emph{infinite sum} of a summable family $(f_n)_{n \in \mathbb {N}}$ is the FPS $\sum _{n \in \mathbb {N}} f_n$ whose $n$-th coefficient is $\sum _{i \in S_n} [x^n] f_i$, where $S_n = \{ i : [x^n] f_i \neq 0\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.logseries
def.fps.logSeries

\leanhelper  The \emph{logarithm series} (or $\overline{\log }$) is the FPS 

\[  \overline{\log } := \sum _{n\geq 1} \frac{(-1)^{n-1}}{n} x^n = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots \in K[[x]].  \]

 Its constant term is~ $0$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "the body of `PowerSeries.invOnePlusX`",
      "severity": "minor",
      "bridge": "Unfolding gives the FPS with coefficient `(-1)^n`, whereas the blueprint explicitly calls the right-hand side `\u03b9 = (1+x)\u207b\u00b9`. To recover that characterization, verify by the Cauchy product that `(1+x) \u00b7 \u2211_{n\u22650} (-1)^n x^n = 1`: the constant coefficient is `1`, and every positive coefficient is `(-1)^n + (-1)^(n-1) = 0`. Thus the defined series is the multiplicative inverse of `1+x`, and it can be identified with the blueprint's `\u03b9`."
    }
  ],
  "justification": "The derivative portion matches: the target states `(PowerSeries.derivative K) (PowerSeries.logbar K) = PowerSeries.invOnePlusX K`, and `PowerSeries.logbar` has coefficients `0` at `n = 0` and `algebraMap \u211a K ((-1)^(n-1) / n)` otherwise, exactly matching the blueprint's `overline{log} := \u2211_{n\u22651} (-1)^{n-1}/n x^n`. The only gap is that the blueprint concludes `overline{log}' = \u03b9 = (1+x)^{-1}`, while unfolding the formal right side yields only `PowerSeries.mk fun n => algebraMap \u211a K ((-1)^n)`. Its inverse characterization is routine but is not itself asserted by the target."
}
## TARGET AlgebraicCombinatorics.one_sub_X_pow_isUnit (theorem) — ELABORATED SIGNATURE
∀ (K : Type u_1) [inst : CommRing K] (i : ℕ), 0 < i → IsUnit (1 - PowerSeries.X ^ i)

Docstring: For any positive integer i, the power series 1 - x^i is invertible in K[[x]]
and hence also in K((x)). This allows the computation in the proof of
Theorem `thm.fps.laure.balanced-tern-rep-uniq`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat.lt
ℕ → ℕ → Prop

Body:
fun n m => n.succ.le m

Docstring: Strict inequality of natural numbers, usually accessed via the `<` operator.

It is defined as `n < m = n + 1 ≤ m`.


## BASE-LIBRARY REF IsUnit
{M : Type u_1} → [Monoid M] → M → Prop

Body:
fun {M} [Monoid M] a => ∃ u, ↑u = a

Docstring: An element `a : M` of a `Monoid` is a unit if it has a two-sided inverse.
The actual definition says that `a` is equal to some `u : Mˣ`, where
`Mˣ` is a bundled version of `IsUnit`. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF MonoidWithZero
Type u → Type u

Docstring: A type `M₀` is a “monoid with zero” if it is a monoid with zero element, and `0` is left
and right absorbing. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

Body:
fun {R} [Semiring R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.instSemiring
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → Semiring (MvPowerSeries σ R)

Body:
fun {σ} {R} [Semiring R] =>
  let __src := inferInstanceAs (AddMonoidWithOne (MvPowerSeries σ R));
  let __src_1 := inferInstanceAs (Mul (MvPowerSeries σ R));
  have __src_2 := inferInstanceAs (AddCommMonoid (MvPowerSeries σ R));
  { toAddMonoid := __src.toAddMonoid, add_comm := ⋯, toMul := __src_1, left_distrib := ⋯, right_distrib := ⋯,
    zero_mul := ⋯, mul_zero := ⋯, mul_assoc := ⋯, toOne := __src.toOne, one_mul := ⋯, mul_one := ⋯,
    toNatCast := __src.toNatCast, natCast_zero := ⋯, natCast_succ := ⋯, npow := npowRecAuto, npow_zero := ⋯,
    npow_succ := ⋯ }

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

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


## BASE-LIBRARY REF PowerSeries.instAddGroup
{R : Type u_1} → [AddGroup R] → AddGroup (PowerSeries R)

Body:
fun {R} [AddGroup R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries.instAddGroup
{σ : Type u_1} → {R : Type u_2} → [AddGroup R] → AddGroup (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddGroup R] => Pi.addGroup

## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF One.one
{α : Type u} → [self : One α] → α

Body:
fun α [self : One α] => self.1

Docstring: The "one" element of the type. 

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

Body:
fun {σ} {R} [Semiring R] => { one := (MvPowerSeries.monomial 0) 1 }

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

## BASE-LIBRARY REF MvPowerSeries.instAddCommMonoid
{σ : Type u_1} → {R : Type u_2} → [AddCommMonoid R] → AddCommMonoid (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddCommMonoid R] => Pi.addCommMonoid

## BASE-LIBRARY REF MvPowerSeries.instModule
{σ : Type u_1} →
  {R : Type u_2} →
    {A : Type u_3} →
      [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (MvPowerSeries σ A)

Body:
fun {σ} {R} {A} [Semiring R] [AddCommMonoid A] [_root_.Module R A] => Pi.module (σ →₀ ℕ) (fun a => A) R

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

## BASE-LIBRARY REF MvPowerSeries.monomial
{σ : Type u_1} → {R : Type u_2} → [inst : Semiring R] → (σ →₀ ℕ) → R →ₗ[R] MvPowerSeries σ R

Body:
fun {σ} {R} [Semiring R] n => LinearMap.single R (fun x => R) n

Docstring: The `n`th monomial as multivariate formal power series:
it is defined as the `R`-linear map from `R` to the semiring
of multivariate formal power series associating to each `a`
the map sending `n : σ →₀ ℕ` to the value `a`
and sending all other `x : σ →₀ ℕ` different from `n` to `0`. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

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

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Body:
fun {R} [Semiring R] => MvPowerSeries.X ()

Docstring: The variable of the formal power series ring. 

## INFORMAL STATEMENT
Invertibility of 1 - xi for i > 0

\leanhelper  For any positive integer $i$, the power series $1 - x^i$ is invertible in $K\left[\left[x\right]\right]$ and hence also in $K\left(\left(x\right)\right)$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.module
def.alg.module

Let $K$ be a commutative ring. 

A $K$\emph{-module} means a set $M$ equipped with three maps 

\begin{align*}  \oplus &  :M\times M\rightarrow M,\\ \ominus &  :M\times M\rightarrow M,\\ \rightharpoonup &  :K\times M\rightarrow M \end{align*}

 (notice that the third map has domain $K\times M$, not $M\times M$) and an element $\overrightarrow {0}\in M$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in M$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in M$. 

\item \emph{Neutrality of zero:} We have $a\oplus \overrightarrow {0}=\overrightarrow {0}\oplus a=a$ for all $a\in M$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in M$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Associativity of scaling:} We have $u\rightharpoonup \left( v\rightharpoonup a\right) =\left( uv\right) \rightharpoonup a$ for all $u,v\in K$ and $a\in M$. 

\item \emph{Left distributivity:} We have $u\rightharpoonup \left( a\oplus b\right) =\left( u\rightharpoonup a\right) \oplus \left( u\rightharpoonup b\right) $ for all $u\in K$ and $a,b\in M$. 

\item \emph{Right distributivity:} We have $\left( u+v\right) \rightharpoonup a=\left( u\rightharpoonup a\right) \oplus \left( v\rightharpoonup a\right) $ for all $u,v\in K$ and $a\in M$. 

\item \emph{Neutrality of one:} We have $1\rightharpoonup a=a$ for all $a\in M$. 

\item \emph{Left annihilation:} We have $0\rightharpoonup a=\overrightarrow {0}$ for all $a\in M$. 

\item \emph{Right annihilation:} We have $u\rightharpoonup \overrightarrow {0}=\overrightarrow {0}$ for all $u\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\rightharpoonup $ are called the \emph{addition}, the \emph{subtraction} and the \emph{scaling} (or the $K$\emph{-action}) of the $K$-module $M$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\rightharpoonup $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\rightharpoonup b=a\cdot b$ by $ab$. 

The element $\overrightarrow {0}$ is called the \emph{zero} (or the \emph{zero vector}) of the $K$-module $M$. We will usually just call it $0$. 

When $M$ is a $K$-module, the elements of $M$ are called \emph{vectors}, while the elements of $K$ are called \emph{scalars}. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\rightharpoonup $, with the operation $\rightharpoonup $ having higher precedence than $\oplus $ and $\ominus $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.invertible
def.commring.invertible

\leanhelper  An element $a \in L$ is \emph{invertible} if there exists $b \in L$ such that $a \cdot b = 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.double
def.fps.laure.double

Let $K\left[ \left[ x^{\pm }\right] \right] $ be the $K$-module $K^{\mathbb {Z}}$ of all families $\left( a_{n}\right) _{n\in \mathbb {Z}}=\left( \ldots ,a_{-2},a_{-1},a_{0},a_{1},a_{2},\ldots \right) $ of elements of $K$. Its addition and its scaling are defined entrywise:

\begin{align*}  \left( a_{n}\right) _{n\in \mathbb {Z}}+\left( b_{n}\right) _{n\in \mathbb {Z}} &  =\left( a_{n}+b_{n}\right) _{n\in \mathbb {Z}};\\ \lambda \left( a_{n}\right) _{n\in \mathbb {Z}} &  =\left( \lambda a_{n}\right) _{n\in \mathbb {Z}}\  \  \  \  \  \  \  \  \  \  \text{for each }\lambda \in K. \end{align*}

 An element of $K\left[ \left[ x^{\pm }\right] \right] $ will be called a \emph{doubly infinite power series}. We use the notation $\sum _{n\in \mathbb {Z}}a_{n}x^{n}$ for a family $\left( a_{n}\right) _{n\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.lauser
def.fps.laure.lauser

We let $K\left( \left( x\right) \right) $ be the subset of $K\left[ \left[ x^{\pm }\right] \right] $ consisting of all families $\left( a_{i}\right) _{i\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $ such that the sequence $\left( a_{-1},a_{-2},a_{-3},\ldots \right) $ is essentially finite – i.e., such that all sufficiently low $i\in \mathbb {Z}$ satisfy $a_{i}=0$. 

The elements of $K\left( \left( x\right) \right) $ are called \emph{Laurent series} in one indeterminate $x$ over $K$. 

In Mathlib, Laurent series are implemented as Hahn series over $\mathbb {Z}$ with coefficients in $K$, which are functions $\mathbb {Z} \to K$ whose support is well-founded (equivalently, bounded below). The formalization also provides a predicate on doubly infinite power series that captures this textbook definition.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "the conclusion of `AlgebraicCombinatorics.one_sub_X_pow_isUnit`",
      "severity": "minor",
      "bridge": "Apply the canonical unital ring embedding from `K[[x]]` into `K((x))`. A unital ring homomorphism sends units to units, and it sends `1 - X ^ i` to the corresponding Laurent series `1 - x^i`. Thus the asserted power-series unit yields the omitted Laurent-series invertibility. This is a routine consequence rather than a new substantive proof."
    }
  ],
  "justification": "The formal conclusion is only `IsUnit (1 - PowerSeries.X ^ i)`, whereas the blueprint claims that `1 - x^i` \u201cis invertible in K[[x]] and hence also in K((x))\u201d. The first claim is certified: `PowerSeries K` is `K[[x]]`, and `IsUnit` is stronger than the blueprint\u2019s one-sided inverse definition. The Laurent-series conclusion is absent from the signature, though it follows immediately by mapping the unit along the standard inclusion into Laurent series."
}
## TARGET AlgebraicCombinatorics.FPS.xnEquiv_finprod (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {ι : Type u_2} {n : ℕ} {V : Finset ι} {c d : ι → PowerSeries K},
  (∀ v ∈ V, c v ≡[x^n] d v) → ∏ v ∈ V, c v ≡[x^n] ∏ v ∈ V, d v

Docstring: Finite products preserve x^n-equivalence.
(Lemma lem.fps.prods-mulable-rules.SW1.lem1)
Label: lem.fps.prods-mulable-rules.SW1.lem1 

## PROJECT DEPENDENCY PowerSeries.XnEquiv (def)
{R : Type u_1} → [CommSemiring R] → ℕ → PowerSeries R → PowerSeries R → Prop

Body:
fun {R} [CommSemiring R] n f g => ∀ m ≤ n, (PowerSeries.coeff m) f = (PowerSeries.coeff m) g

Docstring: Two formal power series are x^n-equivalent if their first n+1 coefficients agree.
This corresponds to Definition `def.fps.xneq` in the source text.

We say `XnEquiv n f g` to mean that for all m ∈ {0, 1, ..., n},
we have `[x^m] f = [x^m] g`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Multiset
Type u → Type u

Body:
fun α => Quotient (List.isSetoid α)

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Body:
fun α self => self.1

Docstring: The underlying multiset 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [CommMonoid M] s f => (Multiset.map f s.val).prod

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

Body:
fun {R} [CommRing R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

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

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Nat.le
ℕ → ℕ → Prop

Docstring: Non-strict, or weak, inequality of natural numbers, usually accessed via the `≤` operator.


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

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

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

## INFORMAL STATEMENT
lem.fps.prods-mulable-rules.SW1.lem1

Let $n\in \mathbb {N}$ and let $V$ be a finite set. Let $c,d : V \to K[[x]]$ be two families of FPSs such that $c_v \overset {x^n}{\equiv } d_v$ for each $v\in V$. Then 

\[  \prod _{v\in V} c_v \overset {x^n}{\equiv } \prod _{v\in V} d_v.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.xneq
def.fps.xneq

Let $n\in \mathbb {N}$. Let $f,g\in K\left[\left[x\right]\right]$ be two FPSs. We write $f\overset {x^{n}}{\equiv }g$ if and only if 

\[  \text{each }m\in \left\{ 0,1,\ldots ,n\right\} \text{ satisfies } \left[x^{m}\right]f=\left[x^{m}\right]g.  \]

Thus, we have defined a binary relation $\overset {x^{n}}{\equiv }$ on the set $K\left[\left[x\right]\right]$. We say that an FPS $f$ is $x^{n}$\emph{-equivalent} to an FPS $g$ if and only if $f\overset {x^{n}}{\equiv }g$.

## VERDICT
{
  "verdict": "significant_divergence",
  "discrepancies": [
    {
      "root": "[inst : CommRing K]",
      "severity": "significant",
      "bridge": "The formal theorem can recover the blueprint only after supplying a `CommRing K` instance. The blueprint package never states that `K` is a commutative ring, and its definitions alone do not establish the commutative-ring laws. To cover every coefficient type permitted by the blueprint as written, one would have to add the missing assumption to the blueprint or prove an appropriately generalized product-preservation theorem under whatever weaker algebraic structure makes its FPS operations meaningful; that cannot be derived from this theorem merely by instantiation."
    }
  ],
  "justification": "The elaborated signature explicitly assumes `\u2200 {K : Type u_1} [inst : CommRing K]`, whereas the informal statement only says `c,d : V \u2192 K[[x]]` and none of the supplied informal definitions declares that `K` is a commutative ring. Thus the formal theorem covers only an unstated subclass of the blueprint's coefficient settings. Apart from this restriction, `PowerSeries.XnEquiv` unfolds to `\u2200 m \u2264 n, coeff m f = coeff m g`, exactly matching agreement for `m \u2208 {0,1,\u2026,n}`, and `Finset.prod` faithfully represents the finite products over `V`."
}
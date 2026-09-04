## TARGET T'n_finite_of_discrete (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] [inst_1 : TopologicalSpace K] [DiscreteTopology K] {I : Type u_2}
  {S : I → Type u_3} [inst_3 : (i : I) → Zero (S i)] [(i : I) → DecidableEq (S i)] (p : (i : I) → S i → PowerSeries K),
  (Summable fun ik => p ik.fst ↑ik.snd) → ∀ (n : ℕ), {ik | ∃ m ≤ n, (PowerSeries.coeff m) (p ik.fst ↑ik.snd) ≠ 0}.Finite

Docstring: For discrete K, T'_n = {(i,k) : k ≠ 0, ∃ m ≤ n, coeff m (p i k) ≠ 0} is finite.
This follows from coefficient-wise summability. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF TopologicalSpace
Type u → Type u

Docstring: A topology on `X`. 

## BASE-LIBRARY REF DiscreteTopology
(α : Type u_2) → [t : TopologicalSpace α] → Prop

Docstring: A topological space is discrete if every set is open, that is,
its topology equals the discrete topology `⊥`. 

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Summable
{α : Type u_1} →
  {β : Type u_2} →
    [AddCommMonoid α] →
      [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → Prop

Body:
fun {α} {β} [AddCommMonoid α] [TopologicalSpace α] f L => ∃ a, HasSum f a L

Docstring: `Summable f` means that `f` has some (infinite) sum with respect to `L`. Use `tsum` to get the
value. 

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


## BASE-LIBRARY REF Zero.zero
{α : Type u} → [self : Zero α] → α

Body:
fun α [self : Zero α] => self.1

Docstring: The zero element of the type. 

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

Body:
fun {R} [AddCommMonoid R] => id inferInstance

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.instAddCommMonoid
{σ : Type u_1} → {R : Type u_2} → [AddCommMonoid R] → AddCommMonoid (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddCommMonoid R] => Pi.addCommMonoid

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

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

## BASE-LIBRARY REF PowerSeries.WithPiTopology.instTopologicalSpace
(R : Type u_1) → [TopologicalSpace R] → TopologicalSpace (PowerSeries R)

Body:
fun R [TopologicalSpace R] => Pi.topologicalSpace

Docstring: The pointwise topology on `PowerSeries` 

## BASE-LIBRARY REF Sigma.fst
{α : Type u} → {β : α → Type v} → Sigma β → α

Body:
fun α β self => self.1

Docstring: The first component of a dependent pair.


## BASE-LIBRARY REF Sigma.snd
{α : Type u} → {β : α → Type v} → (self : Sigma β) → β self.fst

Body:
fun α β self => self.2

Docstring: The second component of a dependent pair. Its type depends on the first component.


## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Body:
fun β => { filter := Filter.atTop }

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Body:
fun {α} s => Finite ↑s

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

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

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

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

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

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

## BASE-LIBRARY REF Semiring.toModule._proof_3
∀ {R : Type u_1} [inst : Semiring R] (a b c : R), (a + b) * c = a * c + b * c

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## INFORMAL STATEMENT
lem.fps.T'n-finite-discrete

\leanhelper  \textbf{(Finiteness of $T'_n$.)} Under the assumptions of Proposition \ref{prop.fps.prodrule-inf-inf} (with discrete $K$), define $T'_n = \{ (i,k)\in \overline{S} \mid \exists m\le n,\,  [x^m](p_{i,k})\ne 0\} $. Then $T'_n$ is a finite set.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.coeffsupportset
def.fps.infprod.coeffSupportSet

\leanhelper  For a family $(p_{i,k})$ of FPSs, the \emph{coefficient support set} $T_m$ at degree $m$ is the set $\{ (i,k) : k \neq 0 \text{ and } [x^m] p_{i,k} \neq 0\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.coeffsupportsetunion
def.fps.infprod.coeffSupportSetUnion

\leanhelper  The \emph{coefficient support union} $T'_n = T_0 \cup T_1 \cup \cdots \cup T_n$ is the union of coefficient support sets up to degree $n$.

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

## INFORMAL CONTEXT stmt-algebraic-combinatorics-prop.fps.prodrule-inf-inf
prop.fps.prodrule-inf-inf

Let $I$ be a set. For any $i\in I$, let $S_{i}$ be a set that contains the number $0$. Set

\[  \overline{S}=\left\{  \left( i,k\right) \  \mid \  i\in I\text{ and }k\in S_{i}\text{ and }k\neq 0\right\}  .  \]

For any $i\in I$ and any $k\in S_{i}$, let $p_{i,k}$ be an element of $K\left[ \left[ x\right] \right] $. Assume that 

\begin{equation}  p_{i,0}=1\  \  \  \  \  \  \  \  \  \  \text{for any }i\in I. \end{equation}

 Assume further that the family $\left( p_{i,k}\right) _{\left( i,k\right) \in \overline{S}}$ is summable. Then, the product $\prod _{i\in I}\  \  \sum _{k\in S_{i}}p_{i,k}$ is well-defined (i.e., the family $\left( p_{i,k}\right) _{k\in S_{i}}$ is summable for each $i\in I$, and the family $\left( \sum _{k\in S_{i}}p_{i,k}\right) _{i\in I}$ is multipliable), and we have

\begin{equation}  \prod _{i\in I}\  \  \sum _{k\in S_{i}}p_{i,k}=\sum _{\substack {\left( k_{i}\right) _{i\in I}\in \prod _{i\in I}S_{i}\\ \text{is essentially finite}}}\  \  \prod _{i\in I}p_{i,k_{i}}. \end{equation}

 In particular, the family $\left( \prod _{i\in I}p_{i,k_{i}}\right) _{\left( k_{i}\right) _{i\in I}\in \prod _{i\in I}S_{i}\text{ is essentially finite}}$ is summable.

## VERDICT
{
  "verdict": "significant_divergence",
  "discrepancies": [
    {
      "root": "(Summable fun ik => p ik.fst \u2191ik.snd)",
      "severity": "significant",
      "bridge": "The blueprint assumes summability only for the family indexed by \\(\\overline S=\\{(i,k):k\\ne0\\}\\), whereas the formal premise requires summability over every dependent pair, including every \\((i,0)\\). The blueprint also assumes \\(p_{i,0}=1\\), so extending the family by the zero-index terms generally adds one copy of the constant series 1 for every \\(i\\). For infinite \\(I\\) over a nontrivial discrete ring, that enlarged family need not be summable. Thus the formal theorem cannot in general be applied under the blueprint assumptions; proving its premise is not a routine bridge and is generally false."
    }
  ],
  "justification": "The informal context says \u201cSet \\(\\overline S=\\{(i,k)\\mid k\\ne0\\}\\)\u201d and assumes \u201cthe family \\((p_{i,k})_{(i,k)\\in\\overline S}\\) is summable,\u201d together with \u201c\\(p_{i,0}=1\\).\u201d In contrast, the elaborated signature assumes `(Summable fun ik => p ik.fst \u2191ik.snd)` with `ik` ranging over the full `Sigma S`, without a condition `ik.snd \u2260 0`. Although the formal conclusion likewise ranges over the larger set and is therefore stronger once its premise holds, that does not repair the stronger, generally unavailable summability premise."
}
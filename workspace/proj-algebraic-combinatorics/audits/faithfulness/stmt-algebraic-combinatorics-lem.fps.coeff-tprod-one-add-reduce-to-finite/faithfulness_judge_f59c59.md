## TARGET coeff_tprod_one_add_eq_coeff_prod_of_high_order' (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] [inst_1 : TopologicalSpace K] [DiscreteTopology K] {I : Type u_2}
  (g : I → PowerSeries K) (I_n : Set I) (hI_n : I_n.Finite),
  (Multipliable fun x => 1 + g x) →
    ∀ (n : ℕ),
      (∀ i ∉ I_n, ∀ m ≤ n, (PowerSeries.coeff m) (g i) = 0) →
        (PowerSeries.coeff n) (∏' (i : I), (1 + g i)) = (PowerSeries.coeff n) (∏ i ∈ hI_n.toFinset, (1 + g i))

Docstring: For infinite products, if `g i` has high order for `i ∉ I_n`,
then `coeff n` of the tprod equals `coeff n` of the finite product over `I_n`.

This is the key lemma for reducing infinite products to finite products
when computing individual coefficients. It implements Claim 10 from the tex proof. 

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

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Multipliable
{α : Type u_1} →
  {β : Type u_2} →
    [CommMonoid α] →
      [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → Prop

Docstring: `Multipliable f` means that `f` has some (infinite) product with respect to `L`. Use `tprod` to
get the value. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.WithPiTopology.instTopologicalSpace
(R : Type u_1) → [TopologicalSpace R] → TopologicalSpace (PowerSeries R)

Docstring: The pointwise topology on `PowerSeries` 

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Distrib.toAdd
{R : Type u_1} → [self : Distrib R] → Add R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

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

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instModule
{R : Type u_1} →
  {A : Type u_2} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (PowerSeries A)

## BASE-LIBRARY REF Semiring.toModule
{R : Type u_1} → [inst : Semiring R] → _root_.Module R R

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

## BASE-LIBRARY REF PowerSeries.coeff
{R : Type u_1} → [inst : Semiring R] → ℕ → PowerSeries R →ₗ[R] R

Docstring: The `n`th coefficient of a formal power series. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF tprod
{α : Type u_4} →
  {β : Type u_5} →
    [CommMonoid α] → [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → α

Docstring: `∏' i, f i` is the unconditional product of `f`, if it exists, or 1 otherwise.

More generally, if `L` is a `SummationFilter`, `∏'[L] i, f i` is the product of `f` with respect to
`L` if it exists, and `1` otherwise.

(Note that even if the unconditional product exists, it might not be unique if the topology is not
separated. When the multiplicative support of `f` is finite, we make the most reasonable choice,
to use the product over the multiplicative support. Otherwise, we choose arbitrarily an `a`
satisfying `HasProd f a`. Similar remarks apply to more general summation filters.) 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## INFORMAL STATEMENT
lem.fps.coeff-tprod-one-add-reduce-to-finite

\leanhelper  \textbf{(Infinite irrelevance: reduction to finite product.)} Assume $K$ has the discrete topology. Let $(g_i)_{i\in I}$ be a family such that $(1+g_i)_{i\in I}$ is multipliable, and let $I_n\subseteq I$ be a finite set such that $[x^m](g_i) = 0$ for all $i\notin I_n$ and all $m\le n$. Then 

\[  [x^n]\! \left(\prod _{i\in I}(1+g_i)\right) = [x^n]\! \left(\prod _{i\in I_n}(1+g_i)\right).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.determines-xn-coeff
def.fps.determines-xn-coeff

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a (possibly infinite) family of FPSs. Let $n\in \mathbb {N}$. Let $M$ be a finite subset of $I$. 

\textbf{(a)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the sum of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\sum _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\sum _{i\in M}\mathbf{a}_{i}\right).  \]

\textbf{(b)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the product of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\prod _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\prod _{i\in M}\mathbf{a}_{i}\right).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.multipliable
def.fps.multipliable

Let $\left(\mathbf{a}_{i}\right)_{i\in I}$ be a (possibly infinite) family of FPSs. Then: 

\textbf{(a)} The family $\left(\mathbf{a}_{i}\right)_{i\in I}$ is said to be \emph{multipliable} if and only if each coefficient in its product is finitely determined. 

\textbf{(b)} If the family $\left(\mathbf{a}_{i}\right)_{i\in I}$ is multipliable, then its \emph{product} $\prod _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS whose $x^{n}$-coefficient (for any $n\in \mathbb {N}$) can be computed as follows: If $n\in \mathbb {N}$, and if $M$ is a finite subset of $I$ that determines the $x^{n}$-coefficient in the product of $\left( \mathbf{a}_{i}\right)_{i\in I}$, then 

\[  \left[x^{n}\right]\left(\prod _{i\in I}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\prod _{i\in M}\mathbf{a}_{i}\right).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable
def.fps.summable

A (possibly infinite) family $\left(\mathbf{a}_{i}\right)_{i\in I}$ of FPSs is said to be \emph{summable} (or \emph{entrywise essentially finite}) if 

\[  \text{for each }n\in \mathbb {N}\text{, all but finitely many }i\in I\text{ satisfy }\left[x^{n}\right]\mathbf{a}_{i}=0.  \]

 In this case, the sum $\sum _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS with 

\[  \left[x^{n}\right]\left(\sum _{i\in I}\mathbf{a}_{i}\right) =\underbrace{\sum _{i\in I}\left[x^{n}\right]\mathbf{a}_{i}}_{\substack {\text{an essentially}\\ \text{finite sum}}} \  \  \  \  \  \  \  \  \  \  \text{for all }n\in \mathbb {N}\text{.}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.xn-coeff-fin-determined
def.fps.xn-coeff-fin-determined

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a (possibly infinite) family of FPSs. Let $n\in \mathbb {N}$. 

\textbf{(a)} We say that \emph{the $x^{n}$-coefficient in the sum of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ \emph{is finitely determined} if there is a finite subset $M$ of $I$ that determines the $x^{n}$-coefficient in the sum of $\left(\mathbf{a}_{i}\right)_{i\in I}$. 

\textbf{(b)} We say that \emph{the $x^{n}$-coefficient in the product of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ \emph{is finitely determined} if there is a finite subset $M$ of $I$ that determines the $x^{n}$-coefficient in the product of $\left(\mathbf{a}_{i}\right)_{i\in I}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The hypotheses and conclusion match. The blueprint assumes \u201cK has the discrete topology,\u201d a multipliable family `(1+g_i)`, a finite `I_n`, and vanishing `[x^m](g_i)=0` for `i\u2209I_n` and `m\u2264n`; Lean has `[TopologicalSpace K] [DiscreteTopology K]`, `hI_n : I_n.Finite`, `(Multipliable fun x => 1 + g x)`, and `(\u2200 i \u2209 I_n, \u2200 m \u2264 n, (PowerSeries.coeff m) (g i) = 0)`. Its conclusion equates `PowerSeries.coeff n` of `\u220f' i, (1+g i)` with that of the finite product over `hI_n.toFinset`, exactly corresponding to the two displayed coefficients. Under the pointwise topology on `PowerSeries K` and a discrete topology on `K`, topological multipliability expresses eventual stabilization of each coefficient over finite partial products, which is the informal definition of multipliability by finite determination. The `CommRing K` binder supplies the algebraic setting needed for the stated FPS operations and unordered products rather than adding a separate theorem hypothesis. Quantifying `n` after choosing `I_n` does not narrow the statement: the theorem applies to every pair of `n` and finite `I_n` satisfying the stated vanishing condition."
}
## TARGET AlgebraicCombinatorics.FPS.xnApproximator_inter (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {ι : Type u_2} [DecidableEq ι] {a : ι → PowerSeries K} {n : ℕ} {U J : Finset ι},
  AlgebraicCombinatorics.FPS.IsXnApproximator a n U →
    (∀ (i : ι), IsUnit (PowerSeries.constantCoeff (a i))) →
      ∃ M, AlgebraicCombinatorics.FPS.IsXnApproximator (fun i => a ↑i) n M

Docstring: The intersection of an approximator with a subset gives an approximator for the subfamily.
(Lemma lem.fps.prods-mulable-subfams-appr)
Label: lem.fps.prods-mulable-subfams-appr

Given `U` an x^n-approximator for `(aᵢ)_{i∈I}` and `J ⊆ I` (as a Finset),
there exists an x^n-approximator for `(aᵢ)_{i∈J}` derived from `U ∩ J`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.IsXnApproximator (def)
{K : Type u_1} → [CommRing K] → {ι : Type u_2} → (ι → PowerSeries K) → ℕ → Finset ι → Prop

Body:
fun {K} [CommRing K] {ι} a n U => PowerSeries.IsXnApproximator a U n

Docstring: Alias for `PowerSeries.IsXnApproximator` with swapped argument order.
A finite subset `U ⊆ I` is an x^n-approximator for `(aᵢ)_{i∈I}` if it determines
the first `n+1` coefficients in the product.
(Definition def.fps.xnappr)
Label: def.fps.xnappr 

## PROJECT DEPENDENCY PowerSeries.IsXnApproximator (def)
{R : Type u_1} → [CommRing R] → {I : Type u_2} → (I → PowerSeries R) → Finset I → ℕ → Prop

Body:
fun {R} [CommRing R] {I} a M n => ∀ m ≤ n, PowerSeries.DeterminesCoeffInProd a M m

Docstring: A finite subset `M` is an `x^n`-approximator for a family `(a_i)_{i ∈ I}`
if it determines the first `n+1` coefficients (i.e., `x^0, x^1, ..., x^n`)
in the product.
(Label: def.fps.infprod-approx) 

## PROJECT DEPENDENCY PowerSeries.DeterminesCoeffInProd (def)
{R : Type u_1} → [CommRing R] → {I : Type u_2} → (I → PowerSeries R) → Finset I → ℕ → Prop

Body:
fun {R} [CommRing R] {I} a M n =>
  ∀ (J : Finset I), M ⊆ J → (PowerSeries.coeff n) (∏ i ∈ J, a i) = (PowerSeries.coeff n) (∏ i ∈ M, a i)

Docstring: A finite subset `M` of `I` determines the `x^n`-coefficient in the product of
a family `(a_i)_{i ∈ I}` if for every finite superset `J` of `M`, the `x^n`-coefficient
of `∏_{i ∈ J} a_i` equals that of `∏_{i ∈ M} a_i`.
(Label: def.fps.determines-xn-coeff part (b)) 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF IsUnit
{M : Type u_1} → [Monoid M] → M → Prop

Docstring: An element `a : M` of a `Monoid` is a unit if it has a two-sided inverse.
The actual definition says that `a` is equal to some `u : Mˣ`, where
`Mˣ` is a bundled version of `IsUnit`. 

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.constantCoeff
{R : Type u_1} → [inst : Semiring R] → PowerSeries R →+* R

Docstring: The constant coefficient of a formal power series. 

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

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

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

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## INFORMAL STATEMENT
lem.fps.prods-mulable-subfams-appr

\leanhelper  Let $\left(\mathbf{a}_{i}\right)_{i\in I}$ be a family of invertible FPSs. Let $U$ be an $x^n$-approximator for $\left(\mathbf{a}_{i}\right)_{i\in I}$. Let $J\subseteq I$. Then $U\cap J$ (viewed as a subset of $J$) is an $x^n$-approximator for the subfamily $\left(\mathbf{a}_{i}\right)_{i\in J}$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod-approx
def.fps.infprod-approx

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a family of FPSs. Let $n\in \mathbb {N}$. An $x^{n}$\emph{-approximator} for $\left(\mathbf{a}_{i}\right)_{i\in I}$ means a finite subset $M$ of $I$ that determines the first $n+1$ coefficients in the product of $\left(\mathbf{a}_{i}\right)_{i\in I}$. (In other words, $M$ has to determine the $x^{m}$-coefficient in the product of $\left(\mathbf{a}_{i}\right)_{i\in I}$ for each $m\in \left\{ 0,1,\ldots ,n\right\} $.)

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
  "verdict": "drift",
  "justification": "The blueprint concludes that the specific finite set \u201c$U\\cap J$ (viewed as a subset of $J$) is an $x^n$-approximator.\u201d The target instead concludes only `\u2203 M, AlgebraicCombinatorics.FPS.IsXnApproximator (fun i => a \u2191i) n M`. This existential binder imposes no condition that `M` be the subset of `J` represented by `U \u2229 J`; indeed, `U` does not occur in the conclusion at all. Thus the formal conclusion is strictly weaker than the specified one. The difference enters in the TARGET\u2019s existential binder `\u2203 M`. To be faithful, the conclusion should directly assert `IsXnApproximator` for the finset of the subtype `J` whose underlying elements are exactly `U \u2229 J` (or existentially quantify `M` together with an equality identifying its underlying set with `U \u2229 J`). The `DecidableEq \u03b9` binder merely supports `Finset` operations, and the constant-coefficient unit hypothesis is the usual FPS formulation of the blueprint\u2019s invertibility assumption; neither repairs the weakened conclusion."
}
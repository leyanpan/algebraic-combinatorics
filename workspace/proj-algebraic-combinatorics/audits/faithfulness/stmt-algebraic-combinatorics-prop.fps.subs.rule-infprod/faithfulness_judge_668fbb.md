## TARGET tprod_rescale_substitution (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] [inst_1 : TopologicalSpace K] [IsTopologicalRing K] [T2Space K] {I : Type u_2}
  (f : I → PowerSeries K) (a : K),
  Multipliable f → (PowerSeries.rescale a) (∏' (i : I), f i) = ∏' (i : I), (PowerSeries.rescale a) (f i)

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF TopologicalSpace
Type u → Type u

Docstring: A topology on `X`. 

## BASE-LIBRARY REF IsTopologicalRing
(R : Type u_1) → [TopologicalSpace R] → [NonUnitalNonAssocRing R] → Prop

Docstring: A topological ring is a ring `R` where addition, multiplication and negation are continuous.

If `R` is a (unital) ring, then continuity of negation can be derived from continuity of
multiplication as it is multiplication with `-1`. (See
`IsTopologicalSemiring.continuousNeg_of_mul` and
`topological_semiring.to_topological_add_group`) 

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF T2Space
(X : Type u) → [TopologicalSpace X] → Prop

Docstring: A T₂ space, also known as a Hausdorff space, is one in which for every
`x ≠ y` there exists disjoint open sets around `x` and `y`. This is
the most widely used of the separation axioms. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

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

## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

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

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.rescale
{R : Type u_1} → [inst : CommSemiring R] → R → PowerSeries R →+* PowerSeries R

Docstring: The ring homomorphism taking a power series `f(X)` to `f(aX)`. 

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

## INFORMAL STATEMENT
prop.fps.subs.rule-infprod

If $\left( f_{i}\right) _{i\in I}\in K\left[ \left[ x\right] \right] ^{I}$ is a multipliable family of FPSs, and if $g\in K\left[ \left[ x\right] \right] $ is an FPS satisfying $\left[ x^{0}\right] g=0$, then the family $\left( f_{i}\circ g\right) _{i\in I}\in K\left[ \left[ x\right] \right] ^{I}$ is multipliable as well and we have $\left( \prod _{i\in I}f_{i}\right) \circ g=\prod _{i\in I}\left( f_{i}\circ g\right) $.

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
  "verdict": "drift",
  "justification": "The formal theorem quantifies only `(a : K)` and applies `PowerSeries.rescale a`, whose docstring says it sends `f(X)` to `f(aX)`. Thus it covers substitution only by the special FPS `g = aX`, whereas the blueprint quantifies over every FPS `g` satisfying `[x^0] g = 0`. This narrowing enters through the target binder `(a : K)` and the use of `PowerSeries.rescale a`; it should instead bind `(g : PowerSeries K)` with a zero-constant-coefficient hypothesis and use general FPS composition. The formal conclusion is also only the equality `(PowerSeries.rescale a) (\u220f' i, f i) = \u220f' i, (PowerSeries.rescale a) (f i)`, while the blueprint additionally asserts that `(f_i \u2218 g)_{i\u2208I}` \u201cis multipliable as well\u201d; that conclusion is absent and must be added. Moreover, the hypothesis `Multipliable f` and product `\u220f'` use topological unconditional convergence (`Multipliable`/`tprod`), while the blueprint defines multipliability coefficientwise by finite determination. The added binders `[TopologicalSpace K] [IsTopologicalRing K] [T2Space K]` therefore participate in a different, mathematically contentful notion rather than merely encoding the stated algebraic setting. A faithful version would use a predicate and infinite product matching the blueprint\u2019s finite-determination definitions (or establish an exact equivalence under justified assumptions), quantify over arbitrary zero-constant-term `g`, and conclude both preservation of multipliability and the substitution/product identity."
}
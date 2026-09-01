## TARGET AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism (def) — ELABORATED SIGNATURE
{K : Type u_1} →
  [inst : CommRing K] →
    {N : ℕ} →
      Equiv.Perm (Fin N) →
        AlgebraicCombinatorics.SymmetricPolynomials.P K N ≃ₐ[K] AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} σ => MvPolynomial.renameEquiv K σ

Docstring: The K-algebra automorphism of P induced by a permutation σ.
This is the main object of Proposition prop.sf.SN-acts-by-alg-auts:
for each σ ∈ S_N, the map f ↦ σ · f is a K-algebra automorphism.
Label: prop.sf.SN-acts-by-alg-auts 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphismHom (def) — ELABORATED SIGNATURE
{K : Type u_1} →
  [inst : CommRing K] →
    {N : ℕ} →
      Equiv.Perm (Fin N) →*
        AlgebraicCombinatorics.SymmetricPolynomials.P K N ≃ₐ[K] AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} =>
  { toFun := fun σ => AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism σ, map_one' := ⋯, map_mul' := ⋯ }

Docstring: The map from S_N to Aut_K(P) is a group homomorphism.
This is the full content of Proposition prop.sf.SN-acts-by-alg-auts:
S_N acts on P by K-algebra automorphisms.
Label: prop.sf.SN-acts-by-alg-auts 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isAlgebra' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → Algebra K (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism_id (theorem)
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ},
  AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism 1 = AlgEquiv.refl

Docstring: The identity permutation gives the identity automorphism.
Label: prop.sf.SN-acts-by-alg-auts 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism_mul_perm (theorem)
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} (σ τ : Equiv.Perm (Fin N)),
  AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism (σ * τ) =
    AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism σ *
      AlgebraicCombinatorics.SymmetricPolynomials.permAutomorphism τ

Docstring: Composition of permutation automorphisms: (σ * τ) acts as τ then σ.
Note: In AlgEquiv, f * g = g.trans f (apply g first, then f).
Label: prop.sf.SN-acts-by-alg-auts 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF AlgEquiv
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: An equivalence of algebras (denoted as `A ≃ₐ[R] B`)
is an equivalence of rings commuting with the actions of scalars. 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF MvPolynomial.renameEquiv
{σ : Type u_1} →
  {τ : Type u_2} → (R : Type u_4) → [inst : CommSemiring R] → σ ≃ τ → MvPolynomial σ R ≃ₐ[R] MvPolynomial τ R

Docstring: `MvPolynomial.rename e` is an equivalence when `e` is. 

## BASE-LIBRARY REF MonoidHom
(M : Type u_10) → (N : Type u_11) → [MulOne M] → [MulOne N] → Type (max u_10 u_11)

Docstring: `M →* N` is the type of functions `M → N` that preserve the `MulOne` structure.
`MonoidHom` is used for both monoid and group homomorphisms.

When possible, instead of parametrizing results over `(f : M →* N)`,
you should parametrize over `(F : Type*) [MonoidHomClass F M N] (f : F)`.

When you extend this structure, make sure to extend `MonoidHomClass`.


## BASE-LIBRARY REF MulOneClass.toMulOne
{M : Type u} → [self : MulOneClass M] → MulOne M

## BASE-LIBRARY REF Monoid.toMulOneClass
{M : Type u} → [self : Monoid M] → MulOneClass M

## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

## BASE-LIBRARY REF AlgEquiv.aut
{R : Type uR} →
  {A₁ : Type uA₁} → [inst : CommSemiring R] → [inst_1 : Semiring A₁] → [inst_2 : Algebra R A₁] → Group (A₁ ≃ₐ[R] A₁)

Docstring: [Stacks Tag 09HR](https://stacks.math.columbia.edu/tag/09HR)

## BASE-LIBRARY REF MonoidHom.mk
{M : Type u_10} →
  {N : Type u_11} →
    [inst : MulOne M] →
      [inst_1 : MulOne N] →
        (toOneHom : OneHom M N) → (∀ (x y : M), toOneHom.toFun (x * y) = toOneHom.toFun x * toOneHom.toFun y) → M →* N

## BASE-LIBRARY REF OneHom.mk
{M : Type u_10} → {N : Type u_11} → [inst : One M] → [inst_1 : One N] → (toFun : M → N) → toFun 1 = 1 → OneHom M N

## BASE-LIBRARY REF MulOne.toOne
{M : Type u_2} → [self : MulOne M] → One M

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

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


## BASE-LIBRARY REF MvPolynomial.algebra
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → [Algebra R S₁] → Algebra R (MvPolynomial σ S₁)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

## BASE-LIBRARY REF AlgEquiv.refl
{R : Type uR} →
  {A₁ : Type uA₁} → [inst : CommSemiring R] → [inst_1 : Semiring A₁] → [inst_2 : Algebra R A₁] → A₁ ≃ₐ[R] A₁

Docstring: Algebra equivalences are reflexive. 

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

## BASE-LIBRARY REF MulOne.toMul
{M : Type u_2} → [self : MulOne M] → Mul M

## INFORMAL STATEMENT
prop.sf.SN-acts-by-alg-auts

The group $S_N$ acts on $\mathcal{P}$ by $K$-algebra automorphisms. In other words, for each $\sigma \in S_N$, the map 

\begin{align*}  \mathcal{P} & \to \mathcal{P}, \\ f & \mapsto \sigma \cdot f \end{align*}

 is a $K$-algebra automorphism of $\mathcal{P}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

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

## VERDICT
{
  "verdict": "faithful",
  "justification": "Together the two declarations formalize both parts of the blueprint. `permAutomorphism` has binders `{K : Type u_1} \u2192 [CommRing K] \u2192 {N : \u2115} \u2192 Equiv.Perm (Fin N) \u2192 P K N \u2243\u2090[K] P K N`, so for every `\u03c3 \u2208 S_N` it supplies exactly the claimed \u201c`K`-algebra automorphism of `\ud835\udcab`.\u201d Its body is `MvPolynomial.renameEquiv K \u03c3`, with `P K N` defined as `MvPolynomial (Fin N) K`. The use of `Fin N` and `Equiv.Perm (Fin N)` is explicitly licensed by `conv-2eb59533`. Moreover, `permAutomorphismHom` has type `Equiv.Perm (Fin N) \u2192* (P K N \u2243\u2090[K] P K N)`, which expresses the first sentence, \u201cThe group `S_N` acts on `\ud835\udcab` by `K`-algebra automorphisms,\u201d including compatibility with identity and multiplication. The dependency equation `permAutomorphism (\u03c3 * \u03c4) = permAutomorphism \u03c3 * permAutomorphism \u03c4` agrees with the stated composition convention that `\u03c3 * \u03c4` sends `x` to `\u03c3 (\u03c4 x)`. No mathematically substantive extra hypothesis is added: `[CommRing K]` matches the supplied definition of the coefficient ring."
}
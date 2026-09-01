## TARGET AlgebraicCombinatorics.CycleDecomposition.sign_eq_neg_one_pow_sum_cycle_lengths_minus_one (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)), Equiv.Perm.sign σ = (-1) ^ (σ.cycleType.sum - σ.cycleType.card)

Docstring: The sign of a permutation can also be expressed as `(-1)^(Σ(m_i - 1))` where
m_i are the cycle lengths (of length ≥ 2). 

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

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

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

## BASE-LIBRARY REF Units.instMulOneClass
{α : Type u} → [inst : Monoid α] → MulOneClass αˣ

Docstring: Units of a monoid have a multiplication and multiplicative identity. 

## BASE-LIBRARY REF MonoidHom.instFunLike
{M : Type u_4} → {N : Type u_5} → [inst : MulOne M] → [inst_1 : MulOne N] → FunLike (M →* N) M N

## BASE-LIBRARY REF Equiv.Perm.sign
{α : Type u} → [DecidableEq α] → [Fintype α] → Equiv.Perm α →* ℤˣ

Docstring: `SignType.sign` of a permutation returns the signature or parity of a permutation, `1` for even
permutations, `-1` for odd permutations. It is the unique surjective group homomorphism from
`Perm α` to the group with two elements. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Int.instUnitsPow
{R : Type u_1} → [inst : CommSemiring R] → [_root_.Module R (Additive ℤˣ)] → Pow ℤˣ R

Docstring: There is a canonical power operation on `ℤˣ` by `R` if `Additive ℤˣ` is an `R`-module.

In lemma names, this operation is called `uzpow` to match `zpow`.

Notably this is satisfied by `R ∈ {ℕ, ℤ, ZMod 2}`. 

## BASE-LIBRARY REF Nat.instCommSemiring
CommSemiring ℕ

## BASE-LIBRARY REF AddCommMonoid.toNatModule
{M : Type u_3} → [inst : AddCommMonoid M] → _root_.Module ℕ M

## BASE-LIBRARY REF Additive
Type u_1 → Type u_1

Docstring: If `α` carries some multiplicative structure, then `Additive α` carries the corresponding
additive structure. 

## BASE-LIBRARY REF Additive.addCommMonoid
{α : Type u} → [CommMonoid α] → AddCommMonoid (Additive α)

## BASE-LIBRARY REF CommGroup.toCommMonoid
{G : Type u} → [self : CommGroup G] → CommMonoid G

## BASE-LIBRARY REF Units.instCommGroupUnits
{α : Type u_1} → [inst : CommMonoid α] → CommGroup αˣ

Docstring: Units of a commutative monoid form a commutative group. 

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Units.instNeg
{α : Type u} → [inst : Monoid α] → [HasDistribNeg α] → Neg αˣ

Docstring: Each element of the group of units of a ring has an additive inverse. 

## BASE-LIBRARY REF NonUnitalNonAssocRing.toHasDistribNeg
{α : Type u} → [inst : NonUnitalNonAssocRing α] → HasDistribNeg α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF NonUnitalNormedCommRing.toNonUnitalCommRing
{α : Type u_5} → [self : NonUnitalNormedCommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF NormedCommRing.toNonUnitalNormedCommRing
{α : Type u_2} → [β : NormedCommRing α] → NonUnitalNormedCommRing α

Docstring: A normed commutative ring is a non-unital normed commutative ring. 

## BASE-LIBRARY REF Int.instNormedCommRing
NormedCommRing ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Units.instOne
{α : Type u} → [inst : Monoid α] → One αˣ

Docstring: Units of a monoid have a unit 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF Multiset.sum
{M : Type u_3} → [AddCommMonoid M] → Multiset M → M

Docstring: Sum of a multiset given a commutative additive monoid structure on `M`.
`sum {a, b, c} = a + b + c` 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Equiv.Perm.cycleType
{α : Type u_1} → [Fintype α] → [DecidableEq α] → Equiv.Perm α → Multiset ℕ

Docstring: The cycle type of a permutation 

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## INFORMAL STATEMENT
lem.sign_eq_neg_one_pow_sum_cycle_lengths_minus_one

\leanhelper  Let $\sigma \in S_n$. Let $m_1, m_2, \ldots , m_j$ be the lengths of the nontrivial cycles (of length $\geq 2$) of $\sigma $. Then $(-1)^{\sigma } = (-1)^{(m_1 - 1) + (m_2 - 1) + \cdots + (m_j - 1)}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cyclelengths
def.cycleLengths

\leanhelper  The \emph{cycle lengths} of $\sigma $ is the multiset of lengths of the nontrivial cycles (length $\geq 2$) in the cycle decomposition of $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.dcdlisttoperm
def.dcdListToPerm

\leanhelper  Given a list of lists (each representing a cycle), the corresponding permutation is obtained by composing the cycle permutations $\operatorname {cyc}_{a_1, a_2, \ldots , a_m}$ for each list $(a_1, a_2, \ldots , a_m)$ in the input.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs
def.perm.cycs

Let $X$ be a set. Let $i_1, i_2, \ldots , i_k$ be $k$ distinct elements of $X$. Then, 

\[  \operatorname {cyc}_{i_1, i_2, \ldots , i_k}  \]

 means the permutation of $X$ that sends 

\begin{align*} & i_1 \text{ to } i_2, \\ & i_2 \text{ to } i_3, \\ & \ldots , \\ & i_{k-1} \text{ to } i_k, \\ & i_k \text{ to } i_1 \end{align*}

 and leaves all other elements of $X$ unchanged. In other words, $\operatorname {cyc}_{i_1, i_2, \ldots , i_k}$ means the permutation of $X$ that satisfies 

\[  \operatorname {cyc}_{i_1, \ldots , i_k}(p) = \begin{cases}  i_{j+1}, &  \text{if } p = i_j \text{ for some } j \in \{ 1, 2, \ldots , k\} ;\\ p, &  \text{otherwise} \end{cases}  \]

 for every $p \in X$, where $i_{k+1}$ means $i_1$. 

This permutation is called a $k$\emph{-cycle}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs.cycs
def.perm.cycs.cycs

Let $X$ be a finite set. Let $\sigma $ be a permutation of $X$. \medskip 

\textbf{(a)} The \emph{cycles} of $\sigma $ are defined to be the cycles in the DCD of $\sigma $ (as defined in Theorem \ref{thm.perm.dcd.main} \textbf{(a)}). (This includes $1$-cycles, if there are any in the DCD of $\sigma $.) 

We shall equate a cycle of $\sigma $ with any of its cyclic rotations; thus, for example, $\left( 3,1,4\right) $ and $\left( 1,4,3\right) $ shall be regarded as being the same cycle (but $\left( 3,1,4\right) $ and $\left( 3,4,1\right) $ shall not). \medskip 

\textbf{(b)} The \emph{cycle lengths partition} of $\sigma $ shall denote the partition of $\left\vert X\right\vert $ obtained by writing down the lengths of the cycles of $\sigma $ in weakly decreasing order.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invs
def.perm.invs

Let $n\in \mathbb {N}$ and $\sigma \in S_{n}$. \medskip 

\textbf{(a)} An \emph{inversion} of $\sigma $ means a pair $\left(i,j\right)$ of elements of $\left[n\right]$ such that $i<j$ and $\sigma \left(i\right) >\sigma \left(j\right)$. \medskip 

\textbf{(b)} The \emph{length} (also known as the \emph{Coxeter length}) of $\sigma $ is the \#  of inversions of $\sigma $. It is called $\ell \left( \sigma \right)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sign
def.perm.sign

Let $n \in \mathbb {N}$. The \emph{sign} of a permutation $\sigma \in S_n$ is defined to be the integer $(-1)^{\ell (\sigma )}$. 

It is denoted by $(-1)^{\sigma }$ or $\operatorname {sgn}(\sigma )$ or $\operatorname {sign}(\sigma )$ or $\varepsilon (\sigma )$. It is also known as the \emph{signature} of $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifies over \u201c\u03c3 \u2208 S_n\u201d and asserts \u201c(-1)^\u03c3 = (-1)^((m\u2081-1)+\u22ef+(m\u2c7c-1))\u201d for the nontrivial cycle lengths. The formal binders `\u2200 {n : \u2115} (\u03c3 : Equiv.Perm (Fin n))` faithfully encode a permutation of an `n`-element set. By the supplied docstring, `Equiv.Perm.sign \u03c3` is precisely the permutation\u2019s signature, represented in `\u2124\u02e3` rather than as an integer; this is an encoding difference, since its values are the units `1` and `-1`. The exponent `\u03c3.cycleType.sum - \u03c3.cycleType.card` is `\u03a3 m_i - j`, which equals `\u03a3 (m_i - 1)` for the positive cycle lengths. In particular, any included 1-cycles would contribute zero and would not alter the exponent. Thus the formal equality states the same sign formula without adding hypotheses or narrowing the quantification."
}
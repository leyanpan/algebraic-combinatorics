## TARGET Equiv.Perm.IsOdd (def) — ELABORATED SIGNATURE
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Prop

Body:
fun {α} [DecidableEq α] [Fintype α] σ => Equiv.Perm.sign σ = -1

Docstring: A permutation is **odd** if its sign is -1 (equivalently, if its length is odd).
**Definition (def.perm.even-odd)** 

## TARGET Equiv.Perm.IsEven (def) — ELABORATED SIGNATURE
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Prop

Body:
fun {α} [DecidableEq α] [Fintype α] σ => Equiv.Perm.sign σ = 1

Docstring: A permutation is **even** if its sign is 1 (equivalently, if its length is even).
**Definition (def.perm.even-odd)** 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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

## INFORMAL STATEMENT
def.perm.even-odd

Let $n \in \mathbb {N}$. A permutation $\sigma \in S_n$ is said to be 

\begin{itemize} \item \emph{even} if $(-1)^{\sigma } = 1$ (that is, if $\ell (\sigma )$ is even); 

\item \emph{odd} if $(-1)^{\sigma } = -1$ (that is, if $\ell (\sigma )$ is odd). 

\end{itemize}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The bodies exactly match the blueprint\u2019s defining conditions: `Equiv.Perm.IsEven \u03c3` is `Equiv.Perm.sign \u03c3 = 1`, corresponding to \u201ceven if $(-1)^\u03c3 = 1$,\u201d and `Equiv.Perm.IsOdd \u03c3` is `Equiv.Perm.sign \u03c3 = -1`, corresponding to \u201codd if $(-1)^\u03c3 = -1$.\u201d The library specifies that `Equiv.Perm.sign` returns `1` for even permutations and `-1` for odd permutations. The binders `{\u03b1 : Type} [Fintype \u03b1] ... \u03c3 : Equiv.Perm \u03b1` are more general than the blueprint\u2019s `n \u2208 \u2115` and `\u03c3 \u2208 S_n`: taking `\u03b1 = Fin n` recovers `S_n`, while arbitrary finite `\u03b1` merely allows any finite underlying set. `[DecidableEq \u03b1]` is computational evidence needed by this sign construction, not a mathematically substantive restriction on finite sets."
}
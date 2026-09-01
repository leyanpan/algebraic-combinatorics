## TARGET AlgebraicCombinatorics.SubtractiveMethods.signProduct_flipSign (theorem) — ELABORATED SIGNATURE
∀ {n d : ℕ} (e : Fin d → ZMod 2) (x : Fin n → Fin d) (k : Fin d),
  Odd (AlgebraicCombinatorics.SubtractiveMethods.multiplicity x k) →
    AlgebraicCombinatorics.SubtractiveMethods.signProduct (AlgebraicCombinatorics.SubtractiveMethods.flipSign k e) x =
      -AlgebraicCombinatorics.SubtractiveMethods.signProduct e x

Docstring: Key lemma: flipping sign k negates the sign product when k has odd multiplicity 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.multiplicity (def)
{n d : ℕ} → (Fin n → Fin d) → Fin d → ℕ

Body:
fun {n d} x k => {i | x i = k}.card

Docstring: The multiplicity of element `k` in tuple `x` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.signProduct (def)
{n d : ℕ} → (Fin d → ZMod 2) → (Fin n → Fin d) → ℤ

Body:
fun {n d} e x => ∏ i, AlgebraicCombinatorics.SubtractiveMethods.toSign (e (x i))

Docstring: The product `e_{x_1} * e_{x_2} * ... * e_{x_n}` for a sign tuple `e` and
index tuple `x` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.flipSign (def)
{d : ℕ} → Fin d → (Fin d → ZMod 2) → Fin d → ZMod 2

Body:
fun {d} k e => Function.update e k (e k + 1)

Docstring: The involution that flips the k-th sign: if `e_k = +1`, make it `-1`, and vice versa 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.toSign (def)
ZMod 2 → ℤ

Body:
fun b => if b = 0 then 1 else -1

Docstring: Convert a ZMod 2 value to a sign: 0 ↦ 1, 1 ↦ -1 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF ZMod
ℕ → Type

Docstring: The integers modulo `n : ℕ`. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Odd
{α : Type u_2} → [Semiring α] → α → Prop

Docstring: An element `a` of a semiring is odd if there exists `k` such `a = 2*k + 1`. 

## BASE-LIBRARY REF Nat.instSemiring
Semiring ℕ

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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

## BASE-LIBRARY REF Function.update
{α : Sort u} → {β : α → Sort v} → [DecidableEq α] → ((a : α) → β a) → (a' : α) → β a' → (a : α) → β a

Docstring: Replacing the value of a function at a given point by a given value. 

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

## BASE-LIBRARY REF ZMod.commRing
(n : ℕ) → CommRing (ZMod n)

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF DivisionRing.toRing
{K : Type u_2} → [self : DivisionRing K] → Ring K

## BASE-LIBRARY REF Field.toDivisionRing
{K : Type u} → [self : Field K] → DivisionRing K

## BASE-LIBRARY REF ZMod.instField
(p : ℕ) → [hp : Fact (Nat.Prime p)] → Field (ZMod p)

Docstring: Field structure on `ZMod p` if `p` is prime. 

## BASE-LIBRARY REF Nat.fact_prime_two
Fact (Nat.Prime 2)

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF ZMod.decidableEq
(n : ℕ) → DecidableEq (ZMod n)

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## INFORMAL STATEMENT
lem.cancel.signProduct-flipSign

\leanhelper  Let $e \in \{ 1,-1\} ^d$, $x \in [d]^n$, and $k \in [d]$ such that the multiplicity $m_k$ of $k$ in $x$ is odd. Then 

\[  \operatorname {signProduct}(\operatorname {flipSign}_k(e), x) = -\operatorname {signProduct}(e, x).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.flipsign
def.cancel.flipSign

\leanhelper  For $k \in [d]$, the map $\operatorname {flipSign}_k : \{ 1,-1\} ^d \to \{ 1,-1\} ^d$ sends a $d$-tuple $(e_1, \ldots , e_d)$ to the tuple obtained by flipping the sign of the $k$-th entry: i.e., replacing $e_k$ by $-e_k$ and leaving all other entries unchanged.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.multiplicity
def.cancel.multiplicity

\leanhelper  For an $n$-tuple $x : \operatorname {Fin} n \to \operatorname {Fin} d$ and $k \in \operatorname {Fin} d$, the \emph{multiplicity} of $k$ in $x$ is the number of all $i \in \operatorname {Fin} n$ satisfying $x(i) = k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.signproduct
Sign product

\leanhelper  For a sign tuple $e : \operatorname {Fin} d \to \mathbb {Z}/2\mathbb {Z}$ and an index tuple $x : \operatorname {Fin} n \to \operatorname {Fin} d$, the \emph{sign product} is 

\[  \operatorname {signProduct}(e, x) := \prod _{i=1}^{n} \operatorname {toSign}(e_{x_i}).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.tosign
Sign conversion

\leanhelper  The function $\operatorname {toSign} : \mathbb {Z}/2\mathbb {Z} \to \mathbb {Z}$ converts elements of $\mathbb {Z}/2\mathbb {Z}$ to signs: $\operatorname {toSign}(0) = 1$ and $\operatorname {toSign}(1) = -1$.

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
  "justification": "The formal binders exactly match the blueprint\u2019s data: `e : Fin d \u2192 ZMod 2`, `x : Fin n \u2192 Fin d`, and `k : Fin d`, using the stated `Fin` indexing convention and the informal sign-tuple encoding. The hypothesis `Odd (multiplicity x k)` matches \u201cthe multiplicity `m_k` of `k` in `x` is odd,\u201d since `multiplicity x k` is `{i | x i = k}.card`. The conclusion is exactly `signProduct (flipSign k e) x = -signProduct e x`. Moreover, `signProduct` is the product of `toSign (e (x i))`, as defined informally, and `flipSign k e = Function.update e k (e k + 1)` toggles the two elements of `ZMod 2`, hence flips the corresponding sign under `toSign`. There are no added hypotheses or narrowed quantifiers."
}
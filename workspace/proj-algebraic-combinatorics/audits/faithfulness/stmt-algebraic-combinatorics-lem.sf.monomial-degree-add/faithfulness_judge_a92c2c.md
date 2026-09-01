## TARGET AlgebraicCombinatorics.SymmetricPolynomials.Monomial.degree_add (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} (m₁ m₂ : AlgebraicCombinatorics.SymmetricPolynomials.Monomial N), (m₁ + m₂).degree = m₁.degree + m₂.degree

Docstring: The degree of a product of monomials is the sum of degrees.
Label: def.sf.monomial 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.Monomial (def)
ℕ → Type

Body:
fun N => Fin N →₀ ℕ

Docstring: A monomial represented by its exponent vector.
In the textbook, a monomial is x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N}.
We represent it by the exponent vector (a₁, a₂, ..., a_N) ∈ ℕ^N.
Label: def.sf.monomial 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.Monomial.degree (def)
{N : ℕ} → AlgebraicCombinatorics.SymmetricPolynomials.Monomial N → ℕ

Body:
fun {N} m => Finsupp.sum m fun x a => a

Docstring: The degree of a monomial is the sum of its exponents.
Label: def.sf.monomial 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Finsupp.instAdd
{ι : Type u_1} → {M : Type u_3} → [inst : AddZeroClass M] → Add (ι →₀ M)

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Finsupp.sum
{α : Type u_1} → {M : Type u_8} → {N : Type u_10} → [inst : Zero M] → [AddCommMonoid N] → (α →₀ M) → (α → M → N) → N

Docstring: `sum f g` is the sum of `g a (f a)` over the support of `f`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## INFORMAL STATEMENT
lem.sf.monomial-degree-add

\leanhelper  The degree of the product of two monomials is the sum of their degrees: $\deg (\mathfrak {m}_1 \cdot \mathfrak {m}_2) = \deg \mathfrak {m}_1 + \deg \mathfrak {m}_2$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.monomial
def.sf.monomial

\textbf{(a)} A \emph{monomial} is an expression of the form $x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ with $a_1, a_2, \ldots , a_N \in \mathbb {N}$. \medskip 

\textbf{(b)} The \emph{degree} $\deg \mathfrak {m}$ of a monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is defined to be $a_1 + a_2 + \cdots + a_N \in \mathbb {N}$. \medskip 

\textbf{(c)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{squarefree} if $a_1, a_2, \ldots , a_N \in \{ 0,1\} $. (This is saying that no square or higher power of an indeterminate appears in $\mathfrak {m}$; thus the name “squarefree”.) \medskip 

\textbf{(d)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{primal} if there is at most one $i \in [N]$ satisfying $a_i > 0$. (This is saying that the monomial $\mathfrak {m}$ contains no two distinct indeterminates. Thus, a primal monomial is just $1$ or a power of an indeterminate.)

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint states \u201cthe degree of the product of two monomials is the sum of their degrees.\u201d The formal declaration quantifies over arbitrary `{N : \u2115}` and `m\u2081 m\u2082 : Monomial N` and concludes `(m\u2081 + m\u2082).degree = m\u2081.degree + m\u2082.degree`. Here `Monomial N` is `Fin N \u2192\u2080 \u2115`, so its inherited addition is pointwise addition of exponent vectors, exactly representing multiplication of monomials. Moreover, `Monomial.degree` is `Finsupp.sum m (fun x a => a)`, matching the informal definition as the sum of exponents. There are no additional hypotheses or restricted quantifiers."
}
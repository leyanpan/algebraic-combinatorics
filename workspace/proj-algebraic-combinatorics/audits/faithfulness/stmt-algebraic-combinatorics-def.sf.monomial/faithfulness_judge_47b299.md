## TARGET AlgebraicCombinatorics.SymmetricPolynomials.Monomial.IsPrimal (def) — ELABORATED SIGNATURE
{N : ℕ} → AlgebraicCombinatorics.SymmetricPolynomials.Monomial N → Prop

Body:
fun {N} m => m.support.card ≤ 1

Docstring: A monomial is primal if at most one exponent is positive.
This means the monomial is either 1 or a power of a single variable.
Label: def.sf.monomial 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.Monomial.IsSquarefree (def) — ELABORATED SIGNATURE
{N : ℕ} → AlgebraicCombinatorics.SymmetricPolynomials.Monomial N → Prop

Body:
fun {N} m => ∀ (i : Fin N), m i ≤ 1

Docstring: A monomial is squarefree if all exponents are 0 or 1.
Label: def.sf.monomial 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.Monomial (def) — ELABORATED SIGNATURE
ℕ → Type

Body:
fun N => Fin N →₀ ℕ

Docstring: A monomial represented by its exponent vector.
In the textbook, a monomial is x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N}.
We represent it by the exponent vector (a₁, a₂, ..., a_N) ∈ ℕ^N.
Label: def.sf.monomial 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.Monomial.degree (def) — ELABORATED SIGNATURE
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


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finsupp.support
{α : Type u_9} → {M : Type u_10} → [inst : Zero M] → (α →₀ M) → Finset α

Docstring: The support of a finitely supported function (aka `Finsupp`). 

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Finsupp.sum
{α : Type u_1} → {M : Type u_8} → {N : Type u_10} → [inst : Zero M] → [AddCommMonoid N] → (α →₀ M) → (α → M → N) → N

Docstring: `sum f g` is the sum of `g a (f a)` over the support of `f`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## INFORMAL STATEMENT
def.sf.monomial

\textbf{(a)} A \emph{monomial} is an expression of the form $x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ with $a_1, a_2, \ldots , a_N \in \mathbb {N}$. \medskip 

\textbf{(b)} The \emph{degree} $\deg \mathfrak {m}$ of a monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is defined to be $a_1 + a_2 + \cdots + a_N \in \mathbb {N}$. \medskip 

\textbf{(c)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{squarefree} if $a_1, a_2, \ldots , a_N \in \{ 0,1\} $. (This is saying that no square or higher power of an indeterminate appears in $\mathfrak {m}$; thus the name “squarefree”.) \medskip 

\textbf{(d)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{primal} if there is at most one $i \in [N]$ satisfying $a_i > 0$. (This is saying that the monomial $\mathfrak {m}$ contains no two distinct indeterminates. Thus, a primal monomial is just $1$ or a power of an indeterminate.)

## VERDICT
{
  "verdict": "faithful",
  "justification": "All four Lean definitions match the corresponding blueprint clauses. For (a), `Monomial N := Fin N \u2192\u2080 \u2115` represents the exponent vector `(a\u2081,\u2026,a_N) \u2208 \u2115^N`; because `Fin N` is finite, the finite-support representation does not restrict such vectors. For (b), `degree m := Finsupp.sum m (fun x a => a)` sums all nonzero exponents, which equals `a\u2081 + \u22ef + a_N` since omitted terms are zero. For (c), `IsSquarefree m := \u2200 (i : Fin N), m i \u2264 1` is equivalent over `\u2115` to every exponent belonging to `{0,1}`. For (d), `IsPrimal m := m.support.card \u2264 1` says that at most one exponent is nonzero; for natural exponents, nonzero is equivalent to positive, exactly matching \u201cat most one `i \u2208 [N]` satisfying `a_i > 0`.\u201d There are no additional hypotheses or mathematically substantive restrictions."
}
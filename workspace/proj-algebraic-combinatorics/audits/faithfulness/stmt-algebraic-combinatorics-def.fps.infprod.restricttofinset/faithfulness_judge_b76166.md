## TARGET PowerSeries.restrictToFinset (def) — ELABORATED SIGNATURE
{I : Type u_2} → (In : Finset I) → (I → ℕ) → ↥In → ℕ

Body:
fun {I} In k i => k ↑i

Docstring: Restrict a function to a finite subset. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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


## INFORMAL STATEMENT
def.fps.infprod.restrictToFinset

\leanhelper  Given a finite subset $I_n \subseteq I$ and a function $k : I \to \mathbb {N}$, \emph{restrict to finset} produces the restriction $k|_{I_n} : I_n \to \mathbb {N}$. This is the inverse direction of the bijection used in Claim~ 8.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.essfinite
def.fps.infprod.essFinite

\leanhelper  A family $(k_i)_{i \in I}$ of natural numbers is \emph{essentially finite} if all but finitely many entries equal $0$, i.e., the set $\{ i \in I : k_i \neq 0\} $ is finite. This corresponds to $S^I_{\mathrm{fin}}$ in the source.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.extendfromfinset
def.fps.infprod.extendFromFinset

\leanhelper  Given a finite subset $I_n \subseteq I$ and a function $f : I_n \to \mathbb {N}$, \emph{extend from finset} produces a function $I \to \mathbb {N}$ by setting $f(i)$ for $i \in I_n$ and $0$ otherwise. This is used in the bijection between essentially finite families supported on $I_n$ and functions $I_n \to S$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.sfini
def.fps.infprod.SfinI

\leanhelper  The set $S^I_{\mathrm{fin}}$ of \emph{essentially finite families} in $\prod _{i \in I} S_i$ is the set of all families $(k_i)_{i \in I}$ such that $k_i \in S_i$ for all $i$ and the family $(k_i)$ is essentially finite.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint asks for, \u201cGiven a finite subset $I_n \\subseteq I$ and a function $k : I \\to \\mathbb N$, \u2026 the restriction $k|_{I_n} : I_n \\to \\mathbb N$.\u201d The elaborated signature has exactly these data and result: `{I : Type u_2} \u2192 (In : Finset I) \u2192 (I \u2192 \u2115) \u2192 \u21a5In \u2192 \u2115`. Here `\u21a5In` is the subtype of elements belonging to the finset `In`, hence formalizes $I_n$. The body `fun {I} In k i => k \u2191i` evaluates `k` at the underlying element of `i : \u21a5In`, exactly giving the restriction. There are no added hypotheses or narrowed quantifiers."
}
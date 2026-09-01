## TARGET AlgebraicCombinatorics.FPS.exampleRecurrence (def) — ELABORATED SIGNATURE
ℕ → ℕ

Body:
fun x =>
  Nat.brecOn x fun x f =>
    (match (motive := (x : ℕ) → Nat.below x → ℕ) x with
      | 0 => fun x => 1
      | n.succ => fun x => 2 * x.1 + n)
      f

Docstring: The sequence defined by $a_0 = 1$ and $a_{n+1} = 2a_n + n$. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.brecOn
{motive : ℕ → Sort u} → (t : ℕ) → ((t : ℕ) → Nat.below t → motive t) → motive t

## BASE-LIBRARY REF Nat.below
{motive : ℕ → Sort u} → ℕ → Sort (max 1 u)

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Nat.succ
ℕ → ℕ

Docstring: The successor of a natural number `n`.

Using `Nat.succ n` should usually be avoided in favor of `n + 1`, which is the [simp normal
form](https://lean-lang.org/doc/reference/4.28.0/find/?domain=Verso.Genre.Manual.section&name=simp-normal-forms).


## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## INFORMAL STATEMENT
def.recurrence.seq

\leanhelper  The sequence $(a_n)$ defined by $a_0 = 1$ and $a_{n+1} = 2a_n + n$ for all $n\geq 0$.

## VERDICT
{
  "verdict": "unclear",
  "justification": "The successor branch is syntactically `| n.succ => fun x => 2 * x.1 + n`, matching the desired `a_{n+1} = 2a_n + n` only if `x.1` is the value of the recursively defined function at `n`. However, the definition is mediated by `Nat.brecOn x ...` and `Nat.below x`, while the package supplies only their signatures and no bodies, docstrings, or computation rules. Thus it does not establish that the first component of `Nat.below (n+1)` is exactly `a_n`, nor how `Nat.brecOn` supplies it. The zero branch `| 0 => ... => 1` is clear, and quantification over `\u2115` covers all `n \u2265 0`, but the recurrence cannot be verified from the available information. The package would need the definitions or computation rules for `Nat.brecOn` and `Nat.below`."
}
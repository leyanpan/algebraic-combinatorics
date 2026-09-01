## TARGET IversonBracket.iverson_true (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : Zero α] [inst_1 : One α] {P : Prop} [inst_2 : Decidable P], P → IversonBracket.iverson P = 1

Docstring: The Iverson bracket of a true proposition is 1. 

## TARGET IversonBracket.iverson_false (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : Zero α] [inst_1 : One α] {P : Prop} [inst_2 : Decidable P], ¬P → IversonBracket.iverson P = 0

Docstring: The Iverson bracket of a false proposition is 0. 

## TARGET IversonBracket.kronecker_eq_iverson (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] {R : Type u_2} [inst_1 : Zero R] [inst_2 : One R] (i j : α),
  (if i = j then 1 else 0) = IversonBracket.iverson (i = j)

Docstring: The Kronecker delta is a special case of the Iverson bracket: δ_{i,j} = [i = j].

In Mathlib, this is represented by `Pi.single i 1 j` for dependent functions,
or `if i = j then 1 else 0` directly. 

## TARGET IversonBracket.iverson (def) — ELABORATED SIGNATURE
(P : Prop) → [Decidable P] → {α : Type u_1} → [Zero α] → [One α] → α

Body:
fun P [Decidable P] {α} [Zero α] [One α] => if P then 1 else 0

Docstring: The Iverson bracket converts a proposition to its truth value (0 or 1).
(Definition \ref{def.pars.iverson})

This is the standard way to embed boolean values into a semiring:
- 1 if `P` is true
- 0 if `P` is false

In Mathlib, this is `if P then 1 else 0` or `(decide P).toNat` for naturals. 

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


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

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## INFORMAL STATEMENT
def.pars.iverson

We will use the \emph{Iverson bracket notation}: If $\mathcal{A}$ is a logical statement, then $\left[ \mathcal{A} \right]$ means the \emph{truth value} of $\mathcal{A}$; this is the integer $\begin{cases}  1, &  \text{if }\mathcal{A}\text{ is true};\\ 0, &  \text{if }\mathcal{A}\text{ is false}. \end{cases} $ 

Note that the Kronecker delta notation is a particular case of the Iverson bracket: We have 

\[  \delta _{i,j}=\left[ i=j \right]\  \  \  \  \  \  \  \  \  \  \text{for any objects }i\text{ and }j.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The definition body `fun P ... => if P then 1 else 0` exactly implements the blueprint\u2019s cases \u201c1, if A is true; 0, if A is false.\u201d The accompanying theorems state these two branches explicitly: `P \u2192 IversonBracket.iverson P = 1` and `\u00acP \u2192 IversonBracket.iverson P = 0`. Although the blueprint calls the result an integer, the formal binders `{\u03b1 : Type u_1} [Zero \u03b1] [One \u03b1]` are a strictly more general codomain supporting designated `0` and `1`; they include the intended integer-valued interpretation rather than weakening it. The `[Decidable P]` binder is the formal computational setting required by `if P then 1 else 0`, not a substantive change to the truth-value cases. Finally, `\u2200 ... (i j : \u03b1), (if i = j then 1 else 0) = IversonBracket.iverson (i = j)` is precisely the stated identity `\u03b4_{i,j} = [i=j]`, with the conditional representing the Kronecker delta. `[DecidableEq \u03b1]` supplies the decidability needed to evaluate that conditional and is an encoding requirement."
}
## TARGET Seq.stabilizesTo_neg (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : Neg K] {a : ℕ → K} {la : K}, Seq.StabilizesTo a la → Seq.StabilizesTo (fun i => -a i) (-la)

Docstring: Negation preserves stabilization. 

## PROJECT DEPENDENCY Seq.StabilizesTo (def)
{K : Type u_1} → (ℕ → K) → K → Prop

Body:
fun {K} a lim => ∃ N, ∀ i ≥ N, a i = lim

Docstring: A sequence `(a_i)_{i ∈ ℕ}` stabilizes to `a` if there exists `N` such that
for all `i ≥ N`, we have `a_i = a`.

This is the notion of convergence in the discrete topology.
(Definition 7.5.1, label: def.fps.lim.stab) 

## BASE-LIBRARY REF Neg
Type u → Type u

Docstring: The notation typeclass for negation.
This enables the notation `-a : α` where `a : α`.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Exists
{α : Sort u} → (α → Prop) → Prop

Docstring: Existential quantification. If `p : α → Prop` is a predicate, then `∃ x : α, p x`
asserts that there is some `x` of type `α` such that `p x` holds.
To create an existential proof, use the `exists` tactic,
or the anonymous constructor notation `⟨x, h⟩`.
To unpack an existential, use `cases h` where `h` is a proof of `∃ x : α, p x`,
or `let ⟨x, hx⟩ := h` where `.

Because Lean has proof irrelevance, any two proofs of an existential are
definitionally equal. One consequence of this is that it is impossible to recover the
witness of an existential from the mere fact of its existence.
For example, the following does not compile:
```
example (h : ∃ x : Nat, x = x) : Nat :=
  let ⟨x, _⟩ := h  -- fail, because the goal is `Nat : Type`
  x
```
The error message `recursor 'Exists.casesOn' can only eliminate into Prop` means
that this only works when the current goal is another proposition:
```
example (h : ∃ x : Nat, x = x) : True :=
  let ⟨x, _⟩ := h  -- ok, because the goal is `True : Prop`
  trivial
```


## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

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

## INFORMAL STATEMENT
lem.fps.lim.stab-neg

\leanhelper  If $(a_i)$ stabilizes to $\ell $, then $(-a_i)$ stabilizes to $-\ell $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.stab
def.fps.lim.stab

Let $\left( a_{i}\right) _{i\in \mathbb {N}}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K^{\mathbb {N}}$ be a sequence of elements of $K$. Let $a\in K$. 

We say that the sequence $\left( a_{i}\right) _{i\in \mathbb {N}}$ \emph{stabilizes to }$a$ if there exists some $N\in \mathbb {N}$ such that

\[  \text{all integers }i\geq N\text{ satisfy }a_{i}=a.  \]

If $a_{i}$ stabilizes to $a$ as $i\rightarrow \infty $, then we write $\lim \limits _{i\rightarrow \infty }a_{i}=a$ and say that $a$ is the \emph{limit} (or \emph{eventual value}) of $\left( a_{i}\right) _{i\in \mathbb {N}}$. This is legitimate, since $a$ is uniquely determined by the sequence $\left( a_{i}\right) _{i\in \mathbb {N}}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states `Seq.StabilizesTo a la \u2192 Seq.StabilizesTo (fun i => -a i) (-la)`, exactly matching \u201cIf `(a_i)` stabilizes to `\u2113`, then `(-a_i)` stabilizes to `-\u2113`.\u201d By the dependency body, stabilization means `\u2203 N, \u2200 i \u2265 N, a i = lim`, matching the informal definition. Applying the same unary negation to an eventual equality gives `-a i = -la`. The sole binder `[inst : Neg K]` merely supplies the negation operation used by the blueprint; no additional algebraic hypothesis or restricted quantifier is imposed."
}
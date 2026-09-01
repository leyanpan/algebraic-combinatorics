## TARGET finite_funcs_with_graph_in_finite_set (theorem) — ELABORATED SIGNATURE
∀ {I : Type u_2} {S : I → Type u_3} [inst : (i : I) → Zero (S i)] [(i : I) → DecidableEq (S i)]
  (T : Set ((i : I) × { k // k ≠ 0 })), T.Finite → {f | ∀ (i : I) (hi : ↑f i ≠ 0), ⟨i, ⟨↑f i, hi⟩⟩ ∈ T}.Finite

Docstring: Essentially finite functions whose graph is contained in a finite set form a finite set.
This is the key combinatorial lemma for proving summability of the RHS. 

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


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

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Filter.Eventually
{α : Type u_1} → (α → Prop) → Filter α → Prop

Docstring: `f.Eventually p` or `∀ᶠ x in f, p x` mean that `{x | p x} ∈ f`. E.g., `∀ᶠ x in atTop, p x`
means that `p` holds true for sufficiently large `x`. 

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

## BASE-LIBRARY REF Filter.cofinite
{α : Type u_2} → Filter α

Docstring: The cofinite filter is the filter of subsets whose complements are finite. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Sigma.mk
{α : Type u} → {β : α → Type v} → (fst : α) → β fst → Sigma β

Docstring: Constructs a dependent pair.

Using this constructor in a context in which the type is not known usually requires a type
ascription to determine `β`. This is because the desired relationship between the two values can't
generally be determined automatically.


## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## INFORMAL STATEMENT
lem.fps.finite-funcs-graph-in-finite-set

\leanhelper  Let $T$ be a finite set of pairs $(i,k)$ with $k\ne 0$. Then the set of essentially finite functions $f : I\to \prod _i S_i$ whose “graph” $\{ (i,f(i)) : f(i)\ne 0\} $ is contained in $T$ is finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.essfinite
def.fps.infprod.essFinite

\leanhelper  A family $(k_i)_{i \in I}$ of natural numbers is \emph{essentially finite} if all but finitely many entries equal $0$, i.e., the set $\{ i \in I : k_i \neq 0\} $ is finite. This corresponds to $S^I_{\mathrm{fin}}$ in the source.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.sfini
def.fps.infprod.SfinI

\leanhelper  The set $S^I_{\mathrm{fin}}$ of \emph{essentially finite families} in $\prod _{i \in I} S_i$ is the set of all families $(k_i)_{i \in I}$ such that $k_i \in S_i$ for all $i$ and the family $(k_i)$ is essentially finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.prodrule.ess-fin
def.fps.prodrule.ess-fin

\textbf{(a)} A sequence $\left( k_{1},k_{2},k_{3},\ldots \right) $ is said to be \emph{essentially finite} if all but finitely many $i\in \left\{  1,2,3,\ldots \right\}  $ satisfy $k_{i}=0$. \medskip 

\textbf{(b)} A family $\left( k_{i}\right) _{i\in I}$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $k_{i}=0$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal conclusion `T.Finite \u2192 {f | \u2200 (i : I) (hi : \u2191f i \u2260 0), \u27e8i, \u27e8\u2191f i, hi\u27e9\u27e9 \u2208 T}.Finite` exactly expresses that, for finite `T`, the set of functions whose nonzero graph is contained in `T` is finite. The pair type `(i : I) \u00d7 { k // k \u2260 0 }` faithfully represents the informal \u201cpairs `(i,k)` with `k \u2260 0`,\u201d including the dependence `k : S i`. The coercion `\u2191f` indicates that `f` ranges over the essentially finite-family subtype, matching \u201cessentially finite functions.\u201d The assumptions `(i : I) \u2192 Zero (S i)` supply the zeros used by the statement. The additional `[(i : I) \u2192 DecidableEq (S i)]` is a decidability instance used to encode/prove the finiteness assertion, rather than a mathematically contentful restriction on the claimed set."
}
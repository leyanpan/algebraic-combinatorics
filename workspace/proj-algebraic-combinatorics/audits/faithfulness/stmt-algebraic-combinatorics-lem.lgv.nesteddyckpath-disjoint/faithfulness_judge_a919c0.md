## TARGET LGV.nestedDyckPath_disjoint (theorem) — ELABORATED SIGNATURE
∀ (n m : ℕ), n ≠ m → ¬LGV.pathsIntersect (LGV.nestedDyckPath n) (LGV.nestedDyckPath m)

Docstring: Different nested Dyck paths don't share any vertices 

## PROJECT DEPENDENCY LGV.pathsIntersect (def)
{V : Type u_3} → [DecidableEq V] → {D : LGV.SimpleDigraph V} → D.Path → D.Path → Prop

Body:
fun {V} [DecidableEq V] {D} p q => ∃ v ∈ p.vertices, v ∈ q.vertices

Docstring: Two paths have a vertex in common 

## PROJECT DEPENDENCY LGV.dyckDigraph (def)
LGV.SimpleDigraph (ℤ × ℕ)

Body:
{ arc := fun u v => v.1 = u.1 + 1 ∧ v.2 = u.2 + 1 ∨ v.1 = u.1 + 1 ∧ v.2 + 1 = u.2 ∧ 0 < u.2,
  arc_irrefl := LGV.dyckDigraph._proof_1 }

Docstring: The Dyck path digraph: vertices are ℤ × ℕ, arcs go (i,j) → (i+1, j+1) and (i,j) → (i+1, j-1).
Used for counting Catalan numbers via Dyck paths.

A Dyck path from (0,0) to (2n,0) corresponds to a balanced sequence of n up-steps
and n down-steps that never goes below the x-axis. A Dyck path is a lattice path
that stays on or above the x-axis, where each step goes either up-right or down-right. 

## PROJECT DEPENDENCY LGV.nestedDyckPath (def)
ℕ → LGV.dyckDigraph.Path

Body:
fun n => { vertices := LGV.nestedDyckVertices n, nonempty := ⋯, arcs_valid := ⋯ }

Docstring: The nested Dyck path from (-2n, 0) to (2n, 0) 

## PROJECT DEPENDENCY LGV.SimpleDigraph (inductive)
Type u_1 → Type u_1

Body:
LGV.SimpleDigraph.mk : {V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

Docstring: A simple digraph with vertex set V.
Convention conv.lgv.digraph(d): A simple digraph has arcs as pairs of distinct vertices. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path (inductive)
{V : Type u_1} → LGV.SimpleDigraph V → Type u_1

Body:
LGV.SimpleDigraph.Path.mk : {V : Type u_1} →
  {D : LGV.SimpleDigraph V} →
    (vertices : List V) →
      vertices ≠ [] →
        (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → D.Path

Docstring: A path in a digraph is a list of vertices where consecutive vertices are connected by arcs.
A path may contain 0 arcs (in which case start and end are identical). 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.vertices (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → List V

Body:
fun V D self => self.1

Docstring: The vertices of the path, in order 

## PROJECT DEPENDENCY LGV.SimpleDigraph.mk (constructor)
{V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.mk (constructor)
{V : Type u_1} →
  {D : LGV.SimpleDigraph V} →
    (vertices : List V) →
      vertices ≠ [] →
        (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → D.Path

## PROJECT DEPENDENCY LGV.nestedDyckVertices (def)
ℕ → List (ℤ × ℕ)

Body:
fun n =>
  List.map
    (fun x =>
      match x with
      | ⟨i, isLt⟩ => (↑i - 2 * ↑n, min i (4 * n - i)))
    (List.finRange (4 * n + 1))

Docstring: The vertices of the nested Dyck path from (-2n, 0) to (2n, 0) 

## PROJECT DEPENDENCY LGV.nestedDyckVertices_nonempty (theorem)
∀ (n : ℕ), LGV.nestedDyckVertices n ≠ []

## PROJECT DEPENDENCY LGV.nestedDyckVertices_arcs_valid (theorem)
∀ (n i : ℕ) (hi : i + 1 < (LGV.nestedDyckVertices n).length),
  LGV.dyckDigraph.arc ((LGV.nestedDyckVertices n).get ⟨i, ⋯⟩) ((LGV.nestedDyckVertices n).get ⟨i + 1, hi⟩)

## PROJECT DEPENDENCY LGV.SimpleDigraph.arc (def)
{V : Type u_1} → LGV.SimpleDigraph V → V → V → Prop

Body:
fun V self => self.1

Docstring: The arc relation: `arc u v` means there is an arc from `u` to `v` 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF instDecidableEqProd
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → DecidableEq (α × β)

## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


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


## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF List
Type u → Type u

Docstring: Linked lists: ordered lists, in which each element has a reference to the next element.

Most operations on linked lists take time proportional to the length of the list, because each
element must be traversed to find the next element.

`List α` is isomorphic to `Array α`, but they are useful for different things:
* `List α` is easier for reasoning, and `Array α` is modeled as a wrapper around `List α`.
* `List α` works well as a persistent data structure, when many copies of the tail are shared. When
  the value is not shared, `Array α` will have better performance because it can do destructive
  updates.


## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

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

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Int.instAdd
Add ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF List.nil
{α : Type u} → List α

Docstring: The empty list, usually written `[]`. 

Conventions for notations in identifiers:

 * The recommended spelling of `[]` in identifiers is `nil`.

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF List.get
{α : Type u} → (as : List α) → Fin as.length → α

Docstring: Returns the element at the provided index, counting from `0`.

In other words, for `i : Fin as.length`, `as.get i` returns the `i`'th element of the list `as`.
Because the index is a `Fin` bounded by the list's length, the index will never be out of bounds.

Examples:
 * `["spring", "summer", "fall", "winter"].get (2 : Fin 4) = "fall"`
 * `["spring", "summer", "fall", "winter"].get (0 : Fin 4) = "spring"`


## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF Nat.lt_of_succ_lt
∀ {n m : ℕ}, n.succ < m → n < m

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF Int.instSub
Sub ℤ

## BASE-LIBRARY REF Nat.cast
{R : Type u} → [NatCast R] → ℕ → R

Docstring: The canonical homomorphism `Nat → R`. In most use cases, the target type will have a (semi)ring
structure, and this homomorphism should be a (semi)ring homomorphism.

`NatCast` and `IntCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`NatCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus a
`NatCast R` instance) whenever `R` is an additive monoid with a `1`.

The prototypical example is `Int.ofNat`.


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Int.instMul
Mul ℤ

## BASE-LIBRARY REF Min.min
{α : Type u} → [self : Min α] → α → α → α

Docstring: Returns the lesser of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `min` in identifiers is `min`.

 * The recommended spelling of `⊓` in identifiers is `inf` (`⊓` is the preferred notation for `min` when the type is not linearly ordered.).

## BASE-LIBRARY REF instMinNat
Min ℕ

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF List.finRange
(n : ℕ) → List (Fin n)

Docstring: Lists all elements of `Fin n` in order, starting at `0`.

Examples:
* `List.finRange 0 = ([] : List (Fin 0))`
* `List.finRange 2 = ([0, 1] : List (Fin 2))`


## INFORMAL STATEMENT
Nested Dyck paths are disjoint

\leanhelper  For $i \ne j$, the nested Dyck paths $\gamma _i$ and $\gamma _j$ share no vertices.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.lgv.crowded
def.lgv.crowded

\leanhelper  Let $\mathbf{p} = (p_1, \ldots , p_k)$ be a path tuple. 

\textbf{(a)} A vertex $v$ is \emph{crowded} in $\mathbf{p}$ if $v$ lies on at least two distinct paths $p_i, p_j$ with $i \ne j$. 

\textbf{(b)} The \emph{crowded path indices} of $\mathbf{p}$ is the set of indices $i$ such that $p_i$ contains a vertex shared with some other path $p_j$. 

\textbf{(c)} For an ipat $\mathbf{p}$, the \emph{minimum crowded path index} is the smallest $i$ in the crowded path indices. 

\textbf{(d)} The \emph{crowded vertices on path $i$} is the set of vertices on $p_i$ that also appear on some other path.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.lgv.lattice
def.lgv.lattice

We consider the infinite simple digraph with vertex set $\mathbb {Z}^{2}$ (so the vertices are pairs of integers) and arcs 

\[  \left( i,j\right) \rightarrow \left( i+1,j\right) \  \  \  \  \  \  \  \  \  \  \text{for all }\left( i,j\right) \in \mathbb {Z}^{2}  \]

 and 

\[  \left( i,j\right) \rightarrow \left( i,j+1\right) \  \  \  \  \  \  \  \  \  \  \text{for all }\left( i,j\right) \in \mathbb {Z}^{2}.  \]

 The arcs of the first form are called \emph{east-steps} or \emph{right-steps}; the arcs of the second form are called \emph{north-steps} or \emph{up-steps}. 

The vertices of this digraph will be called \emph{lattice points} or \emph{grid points} or simply \emph{points}. 

The entire digraph will be denoted by $\mathbb {Z}^{2}$ and called the \emph{integer lattice} or \emph{integer grid}. 

Any path is uniquely determined by its starting point and its step sequence.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.lgv.path-tups
def.lgv.path-tups

Let $k\in \mathbb {N}$. 

\textbf{(a)} A $k$\emph{-vertex} means a $k$-tuple of lattice points. 

\textbf{(b)} If $\mathbf{A}=\left( A_{1},A_{2},\ldots ,A_{k}\right) $ is a $k$-vertex, and if $\sigma \in S_{k}$ is a permutation, then $\sigma \left( \mathbf{A}\right) $ shall denote the $k$-vertex $\left( A_{\sigma \left( 1\right) },A_{\sigma \left( 2\right) },\ldots ,A_{\sigma \left( k\right) }\right) $. 

\textbf{(c)} If $\mathbf{A}=\left( A_{1},A_{2},\ldots ,A_{k}\right) $ and $\mathbf{B}=\left( B_{1},B_{2},\ldots ,B_{k}\right) $ are two $k$-vertices, then a \emph{path tuple} from $\mathbf{A}$ to $\mathbf{B}$ means a $k$-tuple $\left( p_{1},p_{2},\ldots ,p_{k}\right) $, where each $p_{i}$ is a path from $A_{i}$ to $B_{i}$. 

\textbf{(d)} A path tuple $\left( p_{1},p_{2},\ldots ,p_{k}\right) $ is said to be \emph{non-intersecting} if no two of the paths $p_{1},p_{2},\ldots ,p_{k}$ have any vertex in common. We abbreviate “non-intersecting path tuple” as \emph{nipat}. 

\textbf{(e)} A path tuple $\left( p_{1},p_{2},\ldots ,p_{k}\right) $ is said to be \emph{intersecting} if it is not non-intersecting (i.e., if two of its paths have a vertex in common). We abbreviate “intersecting path tuple” as \emph{ipat}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.jt-arc-weight
def.sf.jt-arc-weight

\leanhelper  The arc weight function for the Jacobi–Trudi proof on the integer lattice $\mathbb {Z}^2$: east-steps at height $y$ (with $1 \leq y \leq N$) are weighted by $x_{y-1}$; north-steps are weighted by $1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.jt-source-target
def.sf.jt-source-target

\leanhelper  Define two $N$-vertices $\mathbf{A} = (A_1, \ldots , A_N)$ and $\mathbf{B} = (B_1, \ldots , B_N)$ by 

\[  A_i := (\mu _i - i,\;  1) \quad \text{and} \quad B_i := (\lambda _i - i,\;  N) \quad \text{for each } i \in [N].  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.nipat
def.sf.nipat

\leanhelper  A \emph{non-intersecting path tuple} (nipat) from $\mathbf{A} = (A_1, \ldots , A_N)$ to $\mathbf{B} = (B_1, \ldots , B_N)$ is an $N$-tuple of lattice paths $(p_1, \ldots , p_N)$ where $p_i$ goes from $(\mu _i - i, 1)$ to $(\lambda _i - i, N)$, subject to a column-strictness condition: for $i < j$, if east steps $k$ (in path~ $i$) and $k'$ (in path~ $j$) correspond to the same tableau column ($\mu _i + k = \mu _j + k'$), then the height of path~ $i$ at step~ $k$ is strictly less than the height of path~ $j$ at step~ $k'$. 

The \emph{weight} of a nipat is $\prod _{i} w(p_i)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cFor i \u2260 j, the nested Dyck paths \u03b3_i and \u03b3_j share no vertices.\u201d The target quantifies exactly over distinct natural-number indices, `\u2200 (n m : \u2115), n \u2260 m \u2192`, and concludes `\u00ac LGV.pathsIntersect (LGV.nestedDyckPath n) (LGV.nestedDyckPath m)`. By the body of `LGV.pathsIntersect`, intersection means `\u2203 v \u2208 p.vertices, v \u2208 q.vertices`, so its negation is precisely that the two paths share no vertex. `LGV.nestedDyckPath n` has exactly the vertex list `LGV.nestedDyckVertices n`, matching the indexed nested Dyck paths. The concrete `DecidableEq (\u2124 \u00d7 \u2115)` instance required by `pathsIntersect` is only an encoding requirement, not an additional mathematical hypothesis."
}
## TARGET SymmetricFunctions.latticePathSymEquiv (def) — ELABORATED SIGNATURE
{N : ℕ} → {a c : ℤ} → SymmetricFunctions.LatticePath a c ≃ Sym (Fin N) (c - a).toNat

Body:
fun {N} {a c} =>
  { toFun := SymmetricFunctions.LatticePath.toSym, invFun := SymmetricFunctions.symToLatticePath, left_inv := ⋯,
    right_inv := ⋯ }

Docstring: The equivalence between lattice paths and Sym (multisets). 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath (inductive)
{N : ℕ} → ℤ → ℤ → Type

Body:
SymmetricFunctions.LatticePath.mk : {N : ℕ} →
  {a c : ℤ} →
    (eastStepHeights : List (Fin N)) →
      List.IsChain (fun x1 x2 => x1 ≤ x2) eastStepHeights →
        eastStepHeights.length = (c - a).toNat → SymmetricFunctions.LatticePath a c

Docstring: A lattice path in ℤ² from (a, 1) to (c, N) using north and east steps.
This is the type of paths relevant for the Jacobi-Trudi proof. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.toSym (def)
{N : ℕ} → {a c : ℤ} → SymmetricFunctions.LatticePath a c → Sym (Fin N) (c - a).toNat

Body:
fun {N} {a c} p => ⟨↑p.eastStepHeights, ⋯⟩

Docstring: Convert a lattice path to a Sym element (multiset of heights). 

## PROJECT DEPENDENCY SymmetricFunctions.symToLatticePath (def)
{N : ℕ} → {a c : ℤ} → Sym (Fin N) (c - a).toNat → SymmetricFunctions.LatticePath a c

Body:
fun {N} {a c} s => { eastStepHeights := (↑s).sort fun x1 x2 => x1 ≤ x2, weaklyIncreasing := ⋯, length_eq := ⋯ }

Docstring: Convert a Sym element (multiset) to a lattice path by sorting. 

## PROJECT DEPENDENCY SymmetricFunctions.symToLatticePath_toSym (theorem)
∀ {N : ℕ} {a c : ℤ} (p : SymmetricFunctions.LatticePath a c), SymmetricFunctions.symToLatticePath p.toSym = p

Docstring: Converting a path to Sym and back gives the original path. 

## PROJECT DEPENDENCY SymmetricFunctions.toSym_symToLatticePath (theorem)
∀ {N : ℕ} {a c : ℤ} (s : Sym (Fin N) (c - a).toNat), (SymmetricFunctions.symToLatticePath s).toSym = s

Docstring: Converting a Sym to a path and back gives the original Sym. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.eastStepHeights (def)
{N : ℕ} → {a c : ℤ} → SymmetricFunctions.LatticePath a c → List (Fin N)

Body:
fun N a c self => self.1

Docstring: The sequence of heights at which east-steps are taken.
A path from (a, 1) to (c, N) has exactly (c - a) east-steps
(when c ≥ a), and each east-step occurs at some height in [1, N]. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.mk (constructor)
{N : ℕ} →
  {a c : ℤ} →
    (eastStepHeights : List (Fin N)) →
      List.IsChain (fun x1 x2 => x1 ≤ x2) eastStepHeights →
        eastStepHeights.length = (c - a).toNat → SymmetricFunctions.LatticePath a c

## PROJECT DEPENDENCY SymmetricFunctions.symToWeaklyIncreasing (def)
{N : ℕ} → (n : ℕ) → Sym (Fin N) n → { f // ∀ (i j : Fin n), i ≤ j → f i ≤ f j }

Body:
fun {N} n s =>
  have hlen := ⋯;
  ⟨fun i => ((↑s).sort fun x1 x2 => x1 ≤ x2).get ⟨↑i, ⋯⟩, ⋯⟩

Docstring: Convert a Sym to a weakly increasing function.
The sorted list of a multiset gives a canonical weakly increasing sequence. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Sym
Type u_1 → ℕ → Type (max 0 u_1)

Docstring: The nth symmetric power is n-tuples up to permutation.  We define it
as a subtype of `Multiset` since these are well developed in the
library.  We also give a definition `Sym.sym'` in terms of vectors, and we
show these are equivalent in `Sym.symEquivSym'`.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


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

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

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


## BASE-LIBRARY REF List.IsChain
{α : Type u_1} → (α → α → Prop) → List α → Prop

Docstring: `IsChain R l` means that `R` holds between adjacent elements of `l`. Example:
```
IsChain R [a, b, c, d] ↔ R a b ∧ R b c ∧ R c d
```


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

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

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Multiset.ofList
{α : Type u_1} → List α → Multiset α

Docstring: The quotient map from `List α` to `Multiset α`. 

## BASE-LIBRARY REF Multiset.sort
{α : Type u_1} →
  Multiset α →
    (r : autoParam (α → α → Prop) Multiset.sort._auto_1) →
      [DecidableRel r] → [IsTrans α r] → [Std.Antisymm r] → [Std.Total r] → List α

Docstring: `sort s` constructs a sorted list from the multiset `s`.
(Uses merge sort algorithm.) 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

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

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## INFORMAL STATEMENT
lem.sf.lattice-path-sym-equiv

\leanhelper  There is a canonical equivalence 

\[  \mathrm{LatticePath}(a, c) \simeq \mathrm{Sym}(\mathrm{Fin}\, N, (c-a)^+)  \]

 between lattice paths from $(a, 1)$ to $(c, N)$ and multisets of size $(c - a)^+$ from $\mathrm{Fin}\, N$. The forward map extracts the multiset of east-step heights; the inverse sorts a multiset into a weakly increasing list.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.lgv-path-to-lattice-path
def.sf.lgv-path-to-lattice-path

\leanhelper  Convert an LGV path (in the integer lattice digraph) from $(a, 1)$ to $(c, N)$ into a lattice path by extracting the $y$-coordinates at which east-steps occur and converting them to $\mathrm{Fin}\, N$ values (by subtracting $1$).

## VERDICT
{
  "verdict": "drift",
  "justification": "The target quantifies without restrictions, `{N : \u2115} \u2192 {a c : \u2124} \u2192 ...`, while the blueprint describes genuine north/east paths \u201cfrom `(a, 1)` to `(c, N)`.\u201d The mismatch enters through `SymmetricFunctions.LatticePath.mk`, whose only endpoint-related condition is `eastStepHeights.length = (c - a).toNat`. Since `Int.toNat` sends negative differences to `0`, when `c < a` this type contains the empty list, although no north/east lattice path can move from x-coordinate `a` to the smaller x-coordinate `c`. Similarly, for `N = 0` and `c \u2264 a`, the formal type can contain an empty encoding although no north/east path goes from height `1` to height `0`. Thus the formal equivalence is correctly an equivalence between its list encoding and `Sym (Fin N) (c-a).toNat`, and its forward and inverse maps match the stated extraction/sorting operations, but that encoding is not the blueprint\u2019s endpoint-based path notion for all quantified parameters. On the usual valid range `a \u2264 c` and `1 \u2264 N`, the encoding agrees with the described paths. To repair the discrepancy, the setting and declaration would need those bounds, or `LatticePath` would need to encode genuine paths and endpoint feasibility; in the latter case the unrestricted right-hand side would also need adjustment, since `Sym (Fin N) 0` is inhabited in cases where the genuine path type is empty."
}
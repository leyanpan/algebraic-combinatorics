## TARGET SymmetricFunctions.Nipat (inductive) — ELABORATED SIGNATURE
{N : ℕ} →
  (lam mu : Fin N → ℕ) →
    (∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) →
      (∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) → (∀ (i : Fin N), mu i ≤ lam i) → Type

Body:
SymmetricFunctions.Nipat.mk : {N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          (paths : (i : Fin N) → SymmetricFunctions.LatticePath (↑(mu i) - ↑↑i) (↑(lam i) - ↑↑i)) →
            (∀ (i j : Fin N),
                i < j →
                  ∀ (k : ℕ) (hk : k < (paths i).eastStepHeights.length) (k' : ℕ)
                    (hk' : k' < (paths j).eastStepHeights.length),
                    mu i + k = mu j + k' → (paths i).eastStepHeights[k] < (paths j).eastStepHeights[k']) →
              SymmetricFunctions.Nipat lam mu hlam hmu hcontained

Docstring: A non-intersecting path tuple (nipat) from sources A to targets B.
For Jacobi-Trudi, A_i = (μᵢ - i, 1) and B_i = (λᵢ - i, N). 

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

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.eastStepHeights (def)
{N : ℕ} → {a c : ℤ} → SymmetricFunctions.LatticePath a c → List (Fin N)

Body:
fun N a c self => self.1

Docstring: The sequence of heights at which east-steps are taken.
A path from (a, 1) to (c, N) has exactly (c - a) east-steps
(when c ≥ a), and each east-step occurs at some height in [1, N]. 

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


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


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

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF GetElem.getElem
{coll : Type u} →
  {idx : Type v} →
    {elem : outParam (Type w)} →
      {valid : outParam (coll → idx → Prop)} →
        [self : GetElem coll idx elem valid] → (xs : coll) → (i : idx) → valid xs i → elem

Docstring: The syntax `arr[i]` gets the `i`'th element of the collection `arr`. If there
are proof side conditions to the application, they will be automatically
inferred by the `get_elem_tactic` tactic.


Conventions for notations in identifiers:

 * The recommended spelling of `xs[i]` in identifiers is `getElem`.

 * The recommended spelling of `xs[i]'h` in identifiers is `getElem`.

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


## BASE-LIBRARY REF List.instGetElemNatLtLength
{α : Type u_1} → GetElem (List α) ℕ α fun as i => i < as.length

## BASE-LIBRARY REF List.IsChain
{α : Type u_1} → (α → α → Prop) → List α → Prop

Docstring: `IsChain R l` means that `R` holds between adjacent elements of `l`. Example:
```
IsChain R [a, b, c, d] ↔ R a b ∧ R b c ∧ R c d
```


## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


## INFORMAL STATEMENT
def.sf.nipat

\leanhelper  A \emph{non-intersecting path tuple} (nipat) from $\mathbf{A} = (A_1, \ldots , A_N)$ to $\mathbf{B} = (B_1, \ldots , B_N)$ is an $N$-tuple of lattice paths $(p_1, \ldots , p_N)$ where $p_i$ goes from $(\mu _i - i, 1)$ to $(\lambda _i - i, N)$, subject to a column-strictness condition: for $i < j$, if east steps $k$ (in path~ $i$) and $k'$ (in path~ $j$) correspond to the same tableau column ($\mu _i + k = \mu _j + k'$), then the height of path~ $i$ at step~ $k$ is strictly less than the height of path~ $j$ at step~ $k'$. 

The \emph{weight} of a nipat is $\prod _{i} w(p_i)$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The formal declaration adds mathematically substantive restrictions not present in the blueprint. Its signature requires `hlam : \u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i`, `hmu : \u2200 i j, i \u2264 j \u2192 mu j \u2264 mu i`, and `hcontained : \u2200 i, mu i \u2264 lam i`. The informal statement merely defines the tuples of paths from `(\u03bc_i-i,1)` to `(\u03bb_i-i,N)` with the stated column-strictness condition; it does not say that `\u03bb` and `\u03bc` are N-partitions or that `\u03bc_i \u2264 \u03bb_i`. The supplied definition of \u201cN-partition\u201d only explains that term, which the statement does not apply to `\u03bb` or `\u03bc`. These binders therefore narrow the definition. They should be removed, or the blueprint must explicitly assume that `\u03bb, \u03bc` are N-partitions with `\u03bc \u2286 \u03bb` (and `LatticePath` should itself rule out impossible east-only displacements if unrestricted endpoints are intended).\n\nThere is also an indexing shift. The blueprint uses indices `i \u2208 [N]` and endpoints `\u03bc_i-i` and `\u03bb_i-i`, while the formal paths use `Fin N`\u2014whose values are `0,\u2026,N-1`\u2014and endpoints `(\u2191(mu i) - \u2191\u2191i)` and `(\u2191(lam i) - \u2191\u2191i)`. Under the usual correspondence between `Fin N` value `r` and the blueprint coordinate `i=r+1`, these endpoints should subtract `r+1`, not `r`. The current declaration translates all endpoints one unit east. This should be corrected by subtracting `\u2191i + 1`, or by explicitly defining a different indexing convention in the blueprint/formal dependencies.\n\nFinally, the blueprint also states, \u201cThe weight of a nipat is `\u220f_i w(p_i)`,\u201d but the inductive body contains only `paths` and the column-strictness proof and provides no weight definition. A corresponding weight declaration (and formal path-weight dependency) is needed to cover that clause. The core column condition itself is represented faithfully by `i < j`, `mu i + k = mu j + k'`, and `(paths i).eastStepHeights[k] < (paths j).eastStepHeights[k']`."
}
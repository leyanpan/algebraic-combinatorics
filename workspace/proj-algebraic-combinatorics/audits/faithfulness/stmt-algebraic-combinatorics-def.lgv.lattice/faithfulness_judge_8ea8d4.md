## TARGET LGV1.IntegerLatticeAdj (def) — ELABORATED SIGNATURE
LGV1.LatticePoint → LGV1.LatticePoint → Prop

Body:
fun p q => q = (p.1 + 1, p.2) ∨ q = (p.1, p.2 + 1)

Docstring: The adjacency relation for the integer lattice digraph.
There is an arc from p to q iff q is one step east or north of p.
Label: eq.def.lgv.lattice.east, eq.def.lgv.lattice.north 

## TARGET LGV1.LatticePoint (def) — ELABORATED SIGNATURE
Type

Body:
ℤ × ℤ

Docstring: A point on the integer lattice ℤ².
The vertices of the integer lattice are pairs of integers.
Label: def.lgv.lattice 

## TARGET LGV1.LatticeStep (inductive) — ELABORATED SIGNATURE
Type

Body:
LGV1.LatticeStep.east : LGV1.LatticeStep
LGV1.LatticeStep.north : LGV1.LatticeStep

Docstring: A step on the integer lattice: either east (right) or north (up).
- east: (i,j) → (i+1,j)
- north: (i,j) → (i,j+1)

This type is equivalent to `LGV.LatticeStep'` defined in LGV2.lean.
The equivalence is provided by `latticeStepEquiv : LatticeStep ≃ LGV.LatticeStep'`.

Label: eq.def.lgv.lattice.east, eq.def.lgv.lattice.north 

## TARGET LGV1.integerLattice (def) — ELABORATED SIGNATURE
Digraph LGV1.LatticePoint

Body:
{ Adj := LGV1.IntegerLatticeAdj }

Docstring: The integer lattice as a digraph.
This is the digraph with vertex set ℤ² and arcs (i,j) → (i+1,j) and (i,j) → (i,j+1).
Label: def.lgv.lattice 

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

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

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

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Digraph
Type u_1 → Type u_1

Docstring: A digraph is a relation `Adj` on a vertex type `V`.
The relation describes which pairs of vertices are adjacent.

In this treatment, a digraph may have self-loops.


## BASE-LIBRARY REF Digraph.mk
{V : Type u_1} → (V → V → Prop) → Digraph V

## INFORMAL STATEMENT
def.lgv.lattice

We consider the infinite simple digraph with vertex set $\mathbb {Z}^{2}$ (so the vertices are pairs of integers) and arcs 

\[  \left( i,j\right) \rightarrow \left( i+1,j\right) \  \  \  \  \  \  \  \  \  \  \text{for all }\left( i,j\right) \in \mathbb {Z}^{2}  \]

 and 

\[  \left( i,j\right) \rightarrow \left( i,j+1\right) \  \  \  \  \  \  \  \  \  \  \text{for all }\left( i,j\right) \in \mathbb {Z}^{2}.  \]

 The arcs of the first form are called \emph{east-steps} or \emph{right-steps}; the arcs of the second form are called \emph{north-steps} or \emph{up-steps}. 

The vertices of this digraph will be called \emph{lattice points} or \emph{grid points} or simply \emph{points}. 

The entire digraph will be denoted by $\mathbb {Z}^{2}$ and called the \emph{integer lattice} or \emph{integer grid}. 

Any path is uniquely determined by its starting point and its step sequence.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal definitions exactly specify the blueprint\u2019s graph. `LatticePoint` has body `\u2124 \u00d7 \u2124`, matching \u201cvertex set \u2124\u00b2,\u201d and `IntegerLatticeAdj` has body `q = (p.1 + 1, p.2) \u2228 q = (p.1, p.2 + 1)`, matching exactly the two stated arc forms and excluding all others. `integerLattice` installs precisely this relation as the `Digraph` adjacency. The two constructors `LatticeStep.east` and `LatticeStep.north` match the two kinds of steps. The graph is simple: adjacency is relational, so there are no parallel arcs, and neither listed successor equals its source over \u2124. The final path-determinacy observation follows from each east or north step having a uniquely determined successor from any starting point. There are no added hypotheses or narrowed quantifiers."
}
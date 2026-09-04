## TARGET AlgebraicCombinatorics.CycleDecomposition.dcdListToPerm (def) — ELABORATED SIGNATURE
{α : Type u_1} → [DecidableEq α] → List (List α) → Equiv.Perm α

Body:
fun {α} [DecidableEq α] cycleReps => (List.map List.formPerm cycleReps).prod

Docstring: Convert a list of lists representing cycles to a permutation by taking the product
of the cycle permutations. Each list `[a₁, a₂, ..., aₖ]` represents the k-cycle
`cyc_{a₁, a₂, ..., aₖ}` that sends a₁ → a₂ → ... → aₖ → a₁. 

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


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Body:
fun α => α ≃ α

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF List.prod
{α : Type u_1} → [Mul α] → [One α] → List α → α

Body:
fun {α} [Mul α] [One α] xs => List.foldr (fun x1 x2 => x1 * x2) 1 xs

Docstring: Computes the product of the elements of a list.

Examples:

[a, b, c].prod = a * (b * (c * 1))
[2, 3, 5].prod = 30


## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

Body:
fun {α} => { mul := fun f g => Equiv.trans g f }

Characterization: `(σ * τ) x = σ (τ x)`: multiplication is composition, right factor first (`Equiv.Perm.coe_mul`).

## BASE-LIBRARY REF Equiv.trans
{α : Sort u} → {β : Sort v} → {γ : Sort w} → α ≃ β → β ≃ γ → α ≃ γ

Body:
fun {α} {β} {γ} e₁ e₂ => { toFun := ⇑e₂ ∘ ⇑e₁, invFun := ⇑e₁.symm ∘ ⇑e₂.symm, left_inv := ⋯, right_inv := ⋯ }

Docstring: Composition of equivalences `e₁ : α ≃ β` and `e₂ : β ≃ γ`. 

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

Body:
fun {α} => { one := Equiv.refl α }

Characterization: `(1 : Perm α)` is the identity permutation (`Equiv.Perm.coe_one`).

## BASE-LIBRARY REF Equiv.refl
(α : Sort u_1) → α ≃ α

Body:
fun α => { toFun := id, invFun := id, left_inv := ⋯, right_inv := ⋯ }

Docstring: Any type is equivalent to itself. 

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Body:
fun {α} {β} f x =>
  List.brecOn x fun x f_1 =>
    (match (motive := (x : List α) → List.below x → List β) x with
      | [] => fun x => []
      | a :: as => fun x => f a :: x.1)
      f_1

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


## BASE-LIBRARY REF List.formPerm
{α : Type u_1} → [DecidableEq α] → List α → Equiv.Perm α

Body:
fun {α} [DecidableEq α] l => (List.zipWith Equiv.swap l l.tail).prod

Docstring: A list `l : List α` can be interpreted as an `Equiv.Perm α` where each element in the list
is permuted to the next one, defined as `formPerm`. When we have that `Nodup l`,
we prove that `Equiv.Perm.support (formPerm l) = l.toFinset`, and that
`formPerm l` is rotationally invariant, in `formPerm_rotate`.


## INFORMAL STATEMENT
def.dcdListToPerm

\leanhelper  Given a list of lists (each representing a cycle), the corresponding permutation is obtained by composing the cycle permutations $\operatorname {cyc}_{a_1, a_2, \ldots , a_m}$ for each list $(a_1, a_2, \ldots , a_m)$ in the input.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs
def.perm.cycs

Let $X$ be a set. Let $i_1, i_2, \ldots , i_k$ be $k$ distinct elements of $X$. Then, 

\[  \operatorname {cyc}_{i_1, i_2, \ldots , i_k}  \]

 means the permutation of $X$ that sends 

\begin{align*} & i_1 \text{ to } i_2, \\ & i_2 \text{ to } i_3, \\ & \ldots , \\ & i_{k-1} \text{ to } i_k, \\ & i_k \text{ to } i_1 \end{align*}

 and leaves all other elements of $X$ unchanged. In other words, $\operatorname {cyc}_{i_1, i_2, \ldots , i_k}$ means the permutation of $X$ that satisfies 

\[  \operatorname {cyc}_{i_1, \ldots , i_k}(p) = \begin{cases}  i_{j+1}, &  \text{if } p = i_j \text{ for some } j \in \{ 1, 2, \ldots , k\} ;\\ p, &  \text{otherwise} \end{cases}  \]

 for every $p \in X$, where $i_{k+1}$ means $i_1$. 

This permutation is called a $k$\emph{-cycle}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The body `(List.map List.formPerm cycleReps).prod` maps every input list to its cycle permutation and composes the resulting permutations. For a list of distinct entries `[a\u2081, \u2026, a\u2096]`, `List.formPerm`, defined as `(List.zipWith Equiv.swap l l.tail).prod`, sends `a\u2081 \u2192 a\u2082 \u2192 \u2026 \u2192 a\u2096 \u2192 a\u2081` and fixes all other elements, matching the informal definition of `cyc_{a\u2081,\u2026,a\u2096}`. The outer `List.prod` uses permutation multiplication characterized by `(\u03c3 * \u03c4) x = \u03c3 (\u03c4 x)`, exactly matching the blueprint convention that `\u03b1\u03b2 = \u03b1 \u2218 \u03b2`. The binder `[DecidableEq \u03b1]` is only the computational encoding needed to construct swaps, while `Equiv.Perm \u03b1 = \u03b1 \u2243 \u03b1` correctly represents permutations as bijections."
}
## TARGET AlgebraicCombinatorics.symmetricGroup_iso_of_equiv (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} {Y : Type u_2} (f : X ≃ Y), Nonempty (Equiv.Perm X ≃* Equiv.Perm Y)

Docstring: Symmetric groups of bijective sets are isomorphic. (Conclusion of prop.perm.Sf) 

## TARGET AlgebraicCombinatorics.symmetricGroup_conj_iso (def) — ELABORATED SIGNATURE
{X : Type u_1} → {Y : Type u_2} → X ≃ Y → Equiv.Perm X ≃* Equiv.Perm Y

Body:
fun {X} {Y} f => f.permCongrHom

Docstring: Given a bijection `f : X ≃ Y`, conjugation by `f` gives a group isomorphism
from `Perm X` to `Perm Y`. (prop.perm.Sf)

For each permutation `σ` of `X`, the map `f ∘ σ ∘ f⁻¹ : Y → Y` is a permutation of `Y`.
Furthermore, the map `S_f : S_X → S_Y, σ ↦ f ∘ σ ∘ f⁻¹` is a group isomorphism. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Nonempty
Sort u → Prop

Docstring: `Nonempty α` is a typeclass that says that `α` is not an empty type,
that is, there exists an element in the type. It differs from `Inhabited α`
in that `Nonempty α` is a `Prop`, which means that it does not actually carry
an element of `α`, only a proof that *there exists* such an element.
Given `Nonempty α`, you can construct an element of `α` *nonconstructively*
using `Classical.choice`.


## BASE-LIBRARY REF MulEquiv
(M : Type u_9) → (N : Type u_10) → [Mul M] → [Mul N] → Type (max u_10 u_9)

Docstring: `MulEquiv α β` is the type of an equiv `α ≃ β` which preserves multiplication. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Body:
fun α => α ≃ α

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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

## BASE-LIBRARY REF Equiv.permCongrHom
{α : Type u_4} → {β : Type u_5} → α ≃ β → Equiv.Perm α ≃* Equiv.Perm β

Body:
fun {α} {β} e =>
  let __Equiv := e.permCongr;
  { toEquiv := __Equiv, map_mul' := ⋯ }

Docstring: If `α` is equivalent to `β`, then `Perm α` is equivalent to `Perm β`. 

## INFORMAL STATEMENT
prop.perm.Sf

Let $X$ and $Y$ be two sets, and let $f : X \to Y$ be a bijection. Then, for each permutation $\sigma $ of $X$, the map $f \circ \sigma \circ f^{-1} : Y \to Y$ is a permutation of $Y$. Furthermore, the map 

\begin{align*}  S_f : S_X & \to S_Y, \\ \sigma & \mapsto f \circ \sigma \circ f^{-1} \end{align*}

 is a group isomorphism; thus, we obtain $S_X \cong S_Y$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "unclear",
  "discrepancies": [],
  "justification": "The blueprint requires the specific action \u201c\u03c3 \u21a6 f \u2218 \u03c3 \u2218 f\u207b\u00b9\u201d to be a group isomorphism. The theorem alone only asserts \u201cNonempty (Equiv.Perm X \u2243* Equiv.Perm Y)\u201d, which does not identify the isomorphism. The companion definition returns \u201cf.permCongrHom\u201d, but the supplied body of `Equiv.permCongrHom` delegates its underlying equivalence to the unavailable `e.permCongr`: \u201clet __Equiv := e.permCongr\u201d. Its docstring only says that `Perm \u03b1` and `Perm \u03b2` are equivalent and does not specify the pointwise formula. Therefore the package does not determine whether `symmetricGroup_conj_iso f` actually sends each `\u03c3` to `f \u2218 \u03c3 \u2218 f\u207b\u00b9`. The body or a pointwise characterization of `Equiv.permCongr` is needed."
}
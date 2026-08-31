Declaration: AlgebraicCombinatorics.CauchyBinet.det_const_add_diagonal
Module: AlgebraicCombinatorics.CauchyBinet

Statement id: stmt-algebraic-combinatorics-prop.det.x-ai

## INFORMAL STATEMENT
prop.det.x+ai

Let $n\in \mathbb {N}$. Let $d_1,d_2,\ldots ,d_n\in K$ and $x\in K$. Let $F$ be the $n\times n$-matrix 

\[  \begin{pmatrix}  x+d_1 

&  x 

&  \cdots 

&  x

\\ x 

&  x+d_2 

&  \cdots 

&  x

\\ \vdots 

&  \vdots 

&  \ddots 

&  \vdots 

\\ x 

&  x 

&  \cdots 

&  x+d_n 

\end{pmatrix}\in K^{n\times n}.  \]

 Then, 

\[  \det F = d_1 d_2 \cdots d_n + x \sum _{i=1}^n d_1 d_2 \cdots \widehat{d_i} \cdots d_n,  \]

 where the hat over “$d_i$” means “omit the $d_i$ factor.”

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signature is `theorem det_const_add_diagonal {R : Type u} [CommRing R] {n : \u2115} (x : R) (d : Fin n \u2192 R) : (constPlusDiagMatrix x d).det = (\u220f i, d i) + x * \u2211 i, \u220f j \u2208 Finset.univ.erase i, d j`. This matches the informal binders \u201cLet n\u2208\u2115. Let d\u2081,\u2026,d\u2099\u2208K and x\u2208K\u201d via `n : \u2115`, `x : R`, and the indexed family `d : Fin n \u2192 R`. The referenced definition has body `constPlusDiagMatrix x d := fun i j => x + if i = j then d i else 0`, so its diagonal entry is `x + d i` and every off-diagonal entry is `x`, exactly the displayed matrix `F`. On the right, `\u220f i : Fin n, d i` is `d\u2081\u22efd\u2099`, while for each `i`, `\u220f j \u2208 Finset.univ.erase i, d j` is precisely the product with the `d_i` factor omitted; summing over `Fin n` gives the informal `\u2211_{i=1}^n`. The determinant is Mathlib's determinant over the finite index type `Fin n`, agreeing with the blueprint determinant definition. The `[CommRing R]` binder supplies the formal algebraic setting required by that determinant definition and adds no restriction beyond the blueprint's commutative-ring setting; if `K` is intended to be a field, the Lean result is strictly more general and specializes to it."
}
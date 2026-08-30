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
  "justification": "The elaborated signature is `\u2200 {R : Type u} [CommRing R] {n : \u2115} (x : R) (d : Fin n \u2192 R), (constPlusDiagMatrix x d).det = (\u220f i, d i) + x * \u2211 i, \u220f j \u2208 Finset.univ.erase i, d j`. Its `{n : \u2115}`, `(x : R)`, and `(d : Fin n \u2192 R)` exactly encode the informal binders \u201cLet n\u2208\u2115. Let d\u2081,\u2026,d\u2099\u2208K and x\u2208K.\u201d The hidden `[CommRing R]` matches the blueprint definition of a commutative ring `K`, including commutative multiplication, addition, zero, and one; it is not an added substantive hypothesis. The referenced definition is `constPlusDiagMatrix x d := fun i j => x + if i = j then d i else 0`, so its diagonal entries are `x + d i` and its off-diagonal entries are `x`, exactly the displayed matrix `F`. Finally, `(\u220f i : Fin n, d i)` is `d\u2081\u22efd\u2099`, while `\u220f j \u2208 Finset.univ.erase i, d j` is precisely the product with the `d_i` factor omitted; summing this over `i : Fin n` gives the informal `\u2211_{i=1}^n`. Replacing the uniquely specified `F` directly by `constPlusDiagMatrix x d` and using zero-based `Fin n` indexing do not change the assertion."
}
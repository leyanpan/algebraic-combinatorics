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
  "justification": "The elaborated signature is `\u2200 {R : Type u} [CommRing R] {n : \u2115} (x : R) (d : Fin n \u2192 R), (constPlusDiagMatrix x d).det = (\u220f i, d i) + x * \u2211 i, \u220f j \u2208 Finset.univ.erase i, d j`. This matches the informal binders \u201cLet n\u2208\u2115. Let d\u2081,\u2026,d\u2099\u2208K and x\u2208K\u201d: `d : Fin n \u2192 R` is precisely an n-indexed family, and the determinant definition node likewise uses a commutative-ring coefficient type (`{K : Type u} [CommRing K]`). The referenced definition unfolds to `constPlusDiagMatrix x d i j = x + if i = j then d i else 0`, giving diagonal entries `x + d i` and off-diagonal entries `x`, exactly as in the displayed matrix. On the right, `\u220f i : Fin n, d i` formalizes `d\u2081\u22efd\u2099`, while `\u220f j \u2208 Finset.univ.erase i, d j` is the product over every index except `i`, exactly the hatted factor in \u201cx \u2211_{i=1}^n d\u2081\u22efd\u0302\u1d62\u22efd\u2099\u201d. The finite sums and products also give the standard empty-index interpretation when `n = 0`, which is included by the informal quantifier `n\u2208\u2115`. There are no added hypotheses or narrowed index ranges."
}
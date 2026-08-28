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
  "justification": "Q1: yes. Q2: yes. The source context fixes exactly the same coefficient structure: \u201cFor the rest of Section \u2026 we fix a commutative ring K,\u201d while the elaborated declaration quantifies `{R : Type u} [CommRing R] {n : \u2115}`. The formal definition `constPlusDiagMatrix x d := fun i j => x + if i = j then d i else 0` gives `x + d i` on the diagonal and `x` off the diagonal, exactly matching the informal matrix. Its conclusion, `(constPlusDiagMatrix x d).det = (\u220f i : Fin n, d i) + x * \u2211 i : Fin n, \u220f j \u2208 Finset.univ.erase i, d j`, is precisely the indexed form of \u201cdet F = d\u2081d\u2082\u22efd\u2099 + x \u2211\u1d62 d\u2081d\u2082\u22efd\u0302\u1d62\u22efd\u2099\u201d: `Fin n` represents the n indices and `univ.erase i` omits exactly the i-th factor. No additional hypothesis, restricted range, or differing definition changes either implication."
}
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
  "justification": "The source context fixes the coefficient type exactly as required: \u201cFor the rest of Section ... we fix a commutative ring K.\u201d The elaborated Lean signature likewise quantifies over `{R : Type*} [CommRing R]`, with `{n : \u2115}`, `x : R`, and `d : Fin n \u2192 R`. The referenced definition is `constPlusDiagMatrix x d := fun i j => x + if i = j then d i else 0`, which is exactly the informal matrix having diagonal entries `x+d_i` and off-diagonal entries `x`. The conclusion `(constPlusDiagMatrix x d).det = (\u220f i : Fin n, d i) + x * \u2211 i : Fin n, \u220f j \u2208 Finset.univ.erase i, d j` exactly represents \u201cdet F = d_1...d_n + x sum_i d_1...hat(d_i)...d_n\u201d: `Fin n` indexes the n entries, and `univ.erase i` omits precisely the i-th factor. Thus Q1 is yes: every Lean instance supplies the informal identity over the fixed commutative ring. Q2 is also yes: the informal data translate directly to `d : Fin n \u2192 R` and the defined matrix, yielding exactly the Lean equality. There are no additional hypotheses or restricted index ranges."
}
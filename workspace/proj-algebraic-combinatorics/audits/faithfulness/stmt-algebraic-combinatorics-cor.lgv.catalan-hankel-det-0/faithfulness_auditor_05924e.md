Declaration: LGV.catalan_hankel_det
Module: AlgebraicCombinatorics.Determinants.LGV2

Statement id: stmt-algebraic-combinatorics-cor.lgv.catalan-hankel-det-0

## INFORMAL STATEMENT
cor.lgv.catalan-hankel-det-0

Let $k \in \mathbb {N}$. Recall the Catalan numbers $c_n = \frac{1}{n+1}\binom {2n}{n}$ for all $n \in \mathbb {N}$. Then, 

\[  \det \! \left(\left(c_{i+j-2}\right)_{1 \le i \le k,\;  1 \le j \le k}\right) = \det \! \begin{pmatrix}  c_0 

&  c_1 

&  \cdots 

&  c_{k-1} 

\\ c_1 

&  c_2 

&  \cdots 

&  c_k 

\\ \vdots 

&  \vdots 

&  \ddots 

&  \vdots 

\\ c_{k-1}

&  c_k 

&  \cdots 

&  c_{2k-2} 

\end{pmatrix} = 1.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signature is exactly `LGV.catalan_hankel_det (k : \u2115) : (LGV.catalanHankelMatrix k).det = 1`, matching the blueprint binder \u201cLet k \u2208 \u2115\u201d with no additional hypotheses or restricted range. The referenced definition elaborates to `LGV.catalanHankelMatrix (k : \u2115) : Matrix (Fin k) (Fin k) \u2124 := fun k => Matrix.of fun i j => \u2191(catalan (\u2191i + \u2191j))`. Thus its rows and columns range over `Fin k`, namely indices 0 through k\u22121, and entry `(i,j)` is `catalan (i+j)`. Under the reindexing I=i+1 and J=j+1, this is precisely the blueprint entry `c_{I+J-2}` for `1 \u2264 I,J \u2264 k`, including the displayed rows from `c_0` through `c_{2k-2}`. Although this definition uses Mathlib\u2019s recursively defined `catalan`, Mathlib proves `catalan_eq_centralBinom_div (n : \u2115) : catalan n = n.centralBinom / (n + 1)`, while `Nat.centralBinom` unfolds to `(2 * n).choose n`; hence these are exactly the blueprint numbers `c_n = 1/(n+1) binom(2n,n)`. The determinant is taken over \u2124 after coercing these natural numbers, which faithfully encodes the same integer-valued determinant equality. For `k=0`, `Fin 0` gives the empty matrix and its determinant is 1, consistent with quantifying over all natural k."
}
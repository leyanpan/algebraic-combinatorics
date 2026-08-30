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
  "justification": "The elaborated signature is `LGV.catalan_hankel_det (k : \u2115) : (LGV.catalanHankelMatrix k).det = 1`, matching the blueprint binder \u201cLet $k \\in \\mathbb N$\u201d and conclusion that the determinant \u201c$=1$\u201d; it adds no hypotheses or restrictions. The referenced definition elaborates as `LGV.catalanHankelMatrix k = Matrix.of fun i j => \u2191(catalan (\u2191i + \u2191j))`, with indices `i j : Fin k` and entries in `\u2124`. Thus its zero-based entry at `(i,j)` is $c_{i+j}$, exactly the blueprint's one-based entry $c_{i+j-2}$ after replacing the blueprint indices by `i+1` and `j+1`. Although this definition uses Mathlib's recursive root declaration `catalan : \u2115 \u2192 \u2115` rather than the blueprint definition node `AlgebraicCombinatorics.FPS.catalan n := (2*n).choose n / (n+1)`, the project theorem `AlgebraicCombinatorics.FPS.catalan_eq_mathlib_catalan (n : \u2115) : AlgebraicCombinatorics.FPS.catalan n = catalan n` identifies them, and Mathlib's `catalan_eq_centralBinom_div` together with `Nat.centralBinom n = (2*n).choose n` gives precisely $c_n=\\binom{2n}{n}/(n+1)$. Consequently the defined matrix is exactly the displayed Catalan Hankel matrix, and the formal determinant equality implies the full blueprint equality."
}
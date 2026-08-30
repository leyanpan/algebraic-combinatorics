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
  "justification": "The elaborated signature is `LGV.catalan_hankel_det : \u2200 (k : \u2115), (LGV.catalanHankelMatrix k).det = 1`, matching the blueprint binder \u201cLet $k \\in \\mathbb N$\u201d with no added hypotheses or restricted range. The referenced definition elaborates to `LGV.catalanHankelMatrix : (k : \u2115) \u2192 Matrix (Fin k) (Fin k) \u2124 := fun k => Matrix.of fun i j => \u2191(catalan (\u2191i + \u2191j))`. Thus its indices satisfy `0 \u2264 i,j < k`, and entry `catalan (i+j)` is exactly the zero-based reindexing of the blueprint entry `$c_{i+j-2}$` for `$1 \\le i,j \\le k$`. The unqualified `catalan` resolves to Mathlib's root `catalan : \u2115 \u2192 \u2115`; Mathlib proves `catalan_eq_centralBinom_div (n : \u2115) : catalan n = n.centralBinom / (n + 1)` and `Nat.centralBinom_eq_two_mul_choose (n : \u2115) : n.centralBinom = (2 * n).choose n`, so it has precisely the blueprint meaning `$c_n=\\frac1{n+1}\\binom{2n}{n}$`. Coercing these natural entries to `\u2124` merely supplies the determinant's ring and does not change their values. The blueprint's equality between the indexed matrix and the displayed matrix is an expansion of the same matrix, not an additional mathematical condition omitted by Lean."
}
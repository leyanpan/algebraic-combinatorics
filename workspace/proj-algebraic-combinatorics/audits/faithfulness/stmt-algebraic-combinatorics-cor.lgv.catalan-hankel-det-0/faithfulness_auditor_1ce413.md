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
  "justification": "Q1: yes. The elaborated signature is `LGV.catalan_hankel_det (k : \u2115) : (catalanHankelMatrix k).det = 1`, with no hidden hypotheses or restricted range. The referenced definition is `def catalanHankelMatrix (k : \u2115) : Matrix (Fin k) (Fin k) \u2124 := Matrix.of fun i j => (catalan ((i : \u2115) + (j : \u2115)) : \u2124)`. Thus its zero-based entry `(i,j)` is `catalan (i+j)`. Under the reindexing `i = I-1`, `j = J-1`, this is exactly the informal entry `c_{I+J-2}` for `1 \u2264 I,J \u2264 k`. Mathlib's recursively defined `catalan` denotes the source's sequence because `catalan_eq_centralBinom_div` states `catalan n = n.centralBinom / (n + 1)`, while `Nat.centralBinom_eq_two_mul_choose` states `n.centralBinom = (2 * n).choose n`; together these give the quoted informal definition `c_n = 1/(n+1) binom(2n,n)`. The coercion of these natural-number entries to `\u2124` is the standard determinant coefficient ring and does not alter the claimed equality. Q2: yes. The informal statement quantifies over the same `k \u2208 \u2115` and says the determinant of precisely this finite matrix is `1`, which directly gives the Lean equality after zero-based reindexing and integer coercion. The informal equality between the indexed notation and the displayed matrix is only an expansion of the same matrix, not an additional independent assertion. The `k = 0` case is also compatible: `Fin 0` gives the empty matrix, whose determinant is `1`."
}
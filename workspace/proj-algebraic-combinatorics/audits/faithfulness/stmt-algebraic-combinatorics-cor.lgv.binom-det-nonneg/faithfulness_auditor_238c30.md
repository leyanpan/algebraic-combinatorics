Declaration: LGV.binom_det_nonneg
Module: AlgebraicCombinatorics.Determinants.LGV2

Statement id: stmt-algebraic-combinatorics-cor.lgv.binom-det-nonneg

## INFORMAL STATEMENT
cor.lgv.binom-det-nonneg

Let $k \in \mathbb {N}$. Let $a_1, a_2, \ldots , a_k$ and $b_1, b_2, \ldots , b_k$ be nonnegative integers such that 

\[  a_1 \ge a_2 \ge \cdots \ge a_k \qquad \text{and} \qquad b_1 \ge b_2 \ge \cdots \ge b_k.  \]

 Then, 

\[  \det \! \left(\left(\binom {a_i}{b_j}\right)_{1 \le i \le k,\;  1 \le j \le k}\right) \ge 0.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signature quantifies over exactly the required data: `\u2200 {k : \u2115} (a b : Fin k \u2192 \u2115)`, matching \u201cLet k \u2208 \u2115\u201d and the two k-tuples of nonnegative integers. Its hypotheses `(\u2200 (i j : Fin k), i \u2264 j \u2192 a j \u2264 a i)` and `(\u2200 (i j : Fin k), i \u2264 j \u2192 b j \u2264 b i)` exactly encode \u201ca\u2081 \u2265 a\u2082 \u2265 \u22ef \u2265 a_k\u201d and \u201cb\u2081 \u2265 b\u2082 \u2265 \u22ef \u2265 b_k\u201d under the zero-based indexing of `Fin k`. The conclusion is `0 \u2264 (Matrix.of fun i j => \u2191((a i).choose (b j))).det`: `Nat.choose` is the natural-number binomial coefficient, each entry is cast to `\u2124`, and `Matrix.det` computes the determinant over that commutative ring. Thus this is precisely the asserted nonnegativity of the determinant of the k-by-k matrix `(binom(a_i, b_j))`. The implicit treatment of `k` does not narrow its quantification, and the use of `\u2124` merely supplies the natural codomain in which this integer-valued determinant can be compared with zero."
}
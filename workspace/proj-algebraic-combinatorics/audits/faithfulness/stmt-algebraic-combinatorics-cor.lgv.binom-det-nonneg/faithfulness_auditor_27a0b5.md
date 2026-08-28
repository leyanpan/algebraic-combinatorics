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
  "justification": "Q1: yes. The elaborated signature quantifies over \"{k : \u2115} (a b : Fin k \u2192 \u2115)\", exactly representing two length-k sequences of nonnegative integers. Its hypotheses \"\u2200 i j : Fin k, i \u2264 j \u2192 a j \u2264 a i\" and the analogous condition for b express the informal descending chains \"a\u2081 \u2265 a\u2082 \u2265 \u22ef \u2265 a_k\" and \"b\u2081 \u2265 b\u2082 \u2265 \u22ef \u2265 b_k\". Its conclusion is \"0 \u2264 (Matrix.of fun i j => (a i).choose (b j) : Matrix (Fin k) (Fin k) \u2124).det\". `Matrix.of` merely casts the displayed entry function into a matrix, so this is precisely the determinant of the k-by-k matrix whose (i,j)-entry is the binomial coefficient choose(a_i,b_j), coerced to \u2124. Thus the Lean conclusion implies the informal nonnegativity claim. Q2: yes. Any informal length-k sequences correspond to functions `Fin k \u2192 \u2115`; each displayed descending chain implies the formal all-pairs antitonicity hypothesis by transitivity. Conversely, the formal all-pairs conditions include each adjacent inequality, so they impose no extra restriction. Integer coercion preserves the determinant entries and order, and the shift between informal indices 1,\u2026,k and `Fin k` indices 0,\u2026,k\u22121 is only encoding. Therefore neither direction adds or loses mathematical content."
}
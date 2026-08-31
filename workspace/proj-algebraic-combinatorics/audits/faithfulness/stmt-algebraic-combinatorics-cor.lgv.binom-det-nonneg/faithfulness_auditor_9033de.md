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
  "justification": "The elaborated signature quantifies exactly the required data: \u201c{k : \u2115} (a b : Fin k \u2192 \u2115)\u201d. Thus every entry of both sequences is a nonnegative integer, and `Fin k` is the zero-based formal indexing of the informal positions \u201c1 \u2264 i,j \u2264 k\u201d. The formal hypotheses \u201cha : \u2200 i j : Fin k, i \u2264 j \u2192 a j \u2264 a i\u201d and \u201chb : \u2200 i j : Fin k, i \u2264 j \u2192 b j \u2264 b i\u201d are precisely the informal assumptions \u201ca\u2081 \u2265 a\u2082 \u2265 \u22ef \u2265 a_k\u201d and \u201cb\u2081 \u2265 b\u2082 \u2265 \u22ef \u2265 b_k\u201d. The conclusion is \u201c0 \u2264 (Matrix.of fun i j => \u2191((a i).choose (b j))).det\u201d. `Matrix.of` is definitionally the matrix-valued form of the displayed function, `Nat.choose` is the natural-number binomial coefficient, and its coercion to \u2124 places the matrix in the commutative ring where its determinant and order comparison are stated. Consequently this is exactly \u201cdet ((binom(a_i,b_j))_{1\u2264i,j\u2264k}) \u2265 0\u201d, with no additional hypothesis, restricted quantifier, or altered conclusion."
}
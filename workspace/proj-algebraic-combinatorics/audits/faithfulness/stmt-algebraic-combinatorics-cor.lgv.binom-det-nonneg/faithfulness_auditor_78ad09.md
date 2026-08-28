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
  "justification": "Q1: yes. The elaborated signature is `\u2200 {k : \u2115} (a b : Fin k \u2192 \u2115), (\u2200 i j : Fin k, i \u2264 j \u2192 a j \u2264 a i) \u2192 (\u2200 i j : Fin k, i \u2264 j \u2192 b j \u2264 b i) \u2192 0 \u2264 (Matrix.of fun i j => \u2191((a i).choose (b j))).det`. Thus `a` and `b` are precisely length-`k` sequences of nonnegative integers, and the hypotheses encode exactly the informal chains `a\u2081 \u2265 a\u2082 \u2265 \u22ef \u2265 a\u2096` and `b\u2081 \u2265 b\u2082 \u2265 \u22ef \u2265 b\u2096` after the standard shift from `Fin k` indices `0,\u2026,k-1` to indices `1,\u2026,k`. The conclusion is the determinant over `\u2124` of the matrix whose `(i,j)` entry is `(a i).choose (b j)`, cast from `\u2115`, and asserts it is nonnegative. The library docstring confirms that `Nat.choose n r` is \u201cthe number of `r`-element subsets in an `n`-element set. Also known as binomial coefficients,\u201d while `Matrix.of` merely \u201cCast[s] a function into a matrix.\u201d Hence the formal conclusion implies the displayed informal inequality. Q2: yes. Given any informal `k`, sequences, and the two decreasing chains, representing the sequences as functions `Fin k \u2192 \u2115` supplies exactly `ha` and `hb`, and the informal determinant is exactly the formal `Matrix.det`. There are no hidden section binders or additional hypotheses in the elaborated declaration. The `k = 0` case is also consistent with Lean\u2019s standard meaning of `\u2115` and the empty determinant convention."
}
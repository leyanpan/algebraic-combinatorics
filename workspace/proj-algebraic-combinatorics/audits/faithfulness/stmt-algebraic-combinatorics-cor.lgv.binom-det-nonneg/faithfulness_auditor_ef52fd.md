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
  "justification": "The elaborated signature quantifies `{k : \u2115}` and `(a b : Fin k \u2192 \u2115)`, faithfully encoding \u201cLet k \u2208 \u2115\u201d and the two k-tuples of \u201cnonnegative integers.\u201d Its hypotheses `(ha : \u2200 i j : Fin k, i \u2264 j \u2192 a j \u2264 a i)` and `(hb : \u2200 i j : Fin k, i \u2264 j \u2192 b j \u2264 b i)` exactly express the informal conditions \u201ca\u2081 \u2265 a\u2082 \u2265 \u22ef \u2265 a\u2096\u201d and \u201cb\u2081 \u2265 b\u2082 \u2265 \u22ef \u2265 b\u2096\u201d under the order-preserving identification of `Fin k` with indices 1 through k. The conclusion `0 \u2264 (Matrix.of fun i j => (a i).choose (b j) : Matrix (Fin k) (Fin k) \u2124).det` is precisely the nonnegativity of the determinant whose `(i,j)` entry is `binom(a_i,b_j)`. Mathlib documents `Nat.choose n r` as the binomial coefficient counting r-element subsets of an n-element set; the blueprint dependency `def.binom.binom`, together with its natural-argument specialization, agrees with this operation. `Matrix.of` merely casts the entry function to a matrix, and `Matrix.det` is the Leibniz determinant, matching the blueprint determinant definition. The cast of the natural entries to `\u2124` does not change their values or the asserted nonnegativity. There are no additional section binders or hypotheses. Lean also permits `k = 0`; if the blueprint convention intended only positive k, this is a harmless stronger, more general statement rather than drift."
}
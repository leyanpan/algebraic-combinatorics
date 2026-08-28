Declaration: SymmetricFunctions.pieri_horizontal, SymmetricFunctions.pieri_vertical
Module: AlgebraicCombinatorics.SymmetricFunctions.PieriJacobiTrudi

Statement id: stmt-algebraic-combinatorics-thm.sf.pieri

## INFORMAL STATEMENT
Pieri rules

Let $n\in \mathbb {N}$. Let $\mu $ be an $N$-partition. Then: 

\textbf{(a)} We have

\[  h_{n}s_{\mu }=\sum _{\substack {\lambda \text{ is an }N\text{-partition;}\\ \lambda /\mu \text{ is a horizontal }n\text{-strip}}}s_{\lambda }.  \]

\textbf{(b)} We have

\[  e_{n}s_{\mu }=\sum _{\substack {\lambda \text{ is an }N\text{-partition;}\\ \lambda /\mu \text{ is a vertical }n\text{-strip}}}s_{\lambda }.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: Yes. The elaborated signatures quantify over exactly the source's ambient data: `{N : \u2115} {R : Type u} [CommRing R] (n : \u2115) (mu : NPartition N)`. This matches the source convention, \"Fix a commutative ring K. Fix an N \u2208 \u2115,\" and the target, \"Let n \u2208 \u2115. Let \u03bc be an N-partition.\" The formal left sides are respectively `hsymm (Fin N) R n * schur mu` and `esymm (Fin N) R n * schur mu`. Mathlib documents `hsymm` as \"the sum over all the degree n monomials\" and `esymm` as \"the sum over all the degree n squarefree monomials,\" exactly matching the source definitions of h_n and e_n. The project defines `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial`, matching the source's `s_\u03bb := \u2211_{T \u2208 SSYT(\u03bb)} x_T`. The right-side index sets also have the intended meaning: `horizontalNStripPartitions` filters for containment, `isHorizontalStripFun f mu.parts`, and `hasSizeDiff mu.parts f n`, where the bodies state `mu i \u2265 lam \u27e8i.val + 1, hi\u27e9` and `\u2211 i, lam i = \u2211 i, mu i + n`; `verticalNStripPartitions` similarly requires containment, `lam i \u2264 mu i + 1`, and the same exact size equation. These are precisely the source conditions \"\u03bc \u2286 \u03bb,\" no two added boxes in one column or row, and `|Y(\u03bb/\u03bc)| = n`. Thus each Lean equality implies the corresponding informal Pieri equality. Q2: Yes. Conversely, for arbitrary fixed N and commutative coefficient ring R, the informal sums range over exactly the `NPartition N` values represented by these two finsets, with no additional theorem hypotheses or restricted index ranges. Hence the informal horizontal and vertical Pieri rules instantiate to the two Lean equalities. The hidden `CommRing R` binder is the source's ambient coefficient-ring convention, not an added hypothesis, and the two separate declarations jointly represent parts (a) and (b)."
}
Declaration: SymmetricFunctions.pieri_horizontal
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
  "verdict": "drift",
  "justification": "Q1: No. The elaborated conclusion of `SymmetricFunctions.pieri_horizontal` is only `hsymm (Fin N) R n * schur mu = \u2211 lam \u2208 horizontalNStripPartitions mu n, schur lam`, corresponding to informal part (a), `h_n s_\u03bc = ... horizontal n-strip`. It does not assert informal part (b), `e_n s_\u03bc = ... vertical n-strip`, so this declaration alone cannot imply the full informal statement. The separately declared `SymmetricFunctions.pieri_vertical` is attached to the same market statement, but it is not part of `pieri_horizontal`'s meaning. Q2: Yes, the informal conjunction of (a) and (b) implies part (a). The formal definitions otherwise match that part: `NPartition` has `parts : Fin N \u2192 \u2115` with weak decrease; `horizontalNStripPartitions` filters for containment, `isHorizontalStripFun`, and size equation `|\u03bb| = |\u03bc| + n`; `hsymm` is documented as the sum of all degree-n monomials; and `schur` is defined as `\u2211 T \u2208 ssytFinset lam, T.toMonomial`. Thus the difference enters in the result proposition of `SymmetricFunctions.pieri_horizontal`, not in a binder or referenced definition. To make it faithful to the entire informal statement, use one declaration whose conclusion conjoins both the horizontal and vertical equations, or split the informal statement into separate (a) and (b) statement IDs and associate `pieri_horizontal` only with (a) and `pieri_vertical` only with (b)."
}
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
  "justification": "The elaborated declarations quantify exactly over the stated data: `\u2200 {N : \u2115} {R : Type u} [CommRing R] (n : \u2115) (mu : SymmetricFunctions.NPartition N)`, and conclude respectively `MvPolynomial.hsymm (Fin N) R n * SymmetricFunctions.schur mu = \u2211 lam \u2208 SymmetricFunctions.horizontalNStripPartitions mu n, SymmetricFunctions.schur lam` and `MvPolynomial.esymm (Fin N) R n * SymmetricFunctions.schur mu = \u2211 lam \u2208 SymmetricFunctions.verticalNStripPartitions mu n, SymmetricFunctions.schur lam`. These directly answer the blueprint's binders \u201cLet n \u2208 \u2115. Let \u03bc be an N-partition\u201d and its two equations `h_n s_\u03bc = \u2211 ... s_\u03bb` and `e_n s_\u03bc = \u2211 ... s_\u03bb`. The implicit `R` and `[CommRing R]` encode the blueprint's ambient polynomial ring `K[x\u2081,\u2026,x_N]`, whose definition node likewise assumes `[CommRing K]`; they add no mathematical restriction. `SymmetricFunctions.NPartition` has fields `parts : Fin N \u2192 \u2115` and `weaklyDecreasing : \u2200 i j, i \u2264 j \u2192 parts j \u2264 parts i`, exactly the blueprint definition \u201ca weakly decreasing N-tuple of nonnegative integers.\u201d The referenced polynomial definitions also agree: Mathlib documents `hsymm` as the sum of all degree-`n` monomials and `esymm` as the sum of all degree-`n` squarefree monomials, while `schur lam` unfolds to `\u2211 T \u2208 ssytFinset lam, T.toMonomial`; `ssytFinset` enumerates all fillings with weak rows, strict columns, and entries in `Fin N`, matching the blueprint's Schur-polynomial definition. Finally, the summation finsets have the intended membership conditions. Their filters require containment `\u03bc_i \u2264 \u03bb_i`, the horizontal condition `\u03bc_i \u2265 \u03bb_{i+1}` or vertical condition `\u03bb_i \u2264 \u03bc_i+1`, and `\u2211 \u03bb_i = \u2211 \u03bc_i+n`. These are precisely the definition node's requirements that `\u03bb/\u03bc` be a horizontal or vertical strip with `n` boxes. The additional computational upper bound in `horizontalNStripPartitions` does not narrow the sum: for the first part it follows from containment plus total size difference, and for every later part it is exactly the horizontal-strip inequality. Thus both declarations state the two Pieri rules without added hypotheses or restricted summation ranges."
}
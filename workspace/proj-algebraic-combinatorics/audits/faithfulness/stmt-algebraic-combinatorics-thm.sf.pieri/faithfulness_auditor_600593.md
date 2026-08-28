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
  "justification": "Q1: yes. Q2: yes. The elaborated signatures quantify over `{N : \u2115} {R : Type} [CommRing R]` and state `hsymm (Fin N) R n * schur mu = \u2211 lam \u2208 horizontalNStripPartitions mu n, schur lam` and, respectively, `esymm (Fin N) R n * schur mu = \u2211 lam \u2208 verticalNStripPartitions mu n, schur lam`. These hidden binders match the source's standing convention, quoted as \u201cFix a commutative ring K. Fix an N \u2208 \u2115\u201d and its polynomial ring `K[x\u2081,\u2026,x_N]`; `Fin N` is merely the zero-based indexing equivalent of the source's `[N]`. Mathlib defines `hsymm` as \u201cthe sum over all the degree n monomials\u201d and `esymm` as \u201cthe sum over all the degree n squarefree monomials,\u201d matching `h_n` and `e_n`. The project definition `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial` matches the source definition `s_\u03bb := \u2211_{T\u2208SSYT(\u03bb)} x_T`; its tableaux have entries in `Fin N`, are row-weak, and column-strict, exactly as the source requires. Finally, the formal summation domains match \u201c\u03bb/\u03bc is a horizontal [or vertical] n-strip\u201d: `horizontalNStripPartitions` and `verticalNStripPartitions` require containment, respectively `\u03bc_i \u2265 \u03bb_{i+1}` or `\u03bb_i \u2264 \u03bc_i + 1`, and size equation `|\u03bb| = |\u03bc| + n`. The horizontal enumerator's explicit finite upper bounds do not narrow the intended domain: the bounds for later rows follow from the horizontal-strip condition, while the first-row bound follows from containment and the size equation. Thus both formal declarations express precisely the two informal Pieri identities."
}
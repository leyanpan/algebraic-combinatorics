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
  "justification": "The elaborated signatures quantify exactly as required: `pieri_horizontal {N : \u2115} {R : Type u} [CommRing R] (n : \u2115) (mu : NPartition N)` concludes `hsymm (Fin N) R n * schur mu = \u2211 lam \u2208 horizontalNStripPartitions mu n, schur lam`, and `pieri_vertical` has the corresponding conclusion with `esymm` and `verticalNStripPartitions`. This directly matches the blueprint binders \u201cLet n \u2208 \u2115. Let \u03bc be an N-partition\u201d and conclusions `h_n s_\u03bc = \u2211 ... s_\u03bb` and `e_n s_\u03bc = \u2211 ... s_\u03bb`. The implicit `[CommRing R]` is the coefficient-ring setting supplied by the blueprint definitions of the polynomial ring over K, not an added mathematical hypothesis on n or \u03bc. The local `NPartition N` contains `parts : Fin N \u2192 \u2115` and `weaklyDecreasing : \u2200 i j, i \u2264 j \u2192 parts j \u2264 parts i`, exactly the blueprint definition \u201ca weakly decreasing N-tuple of nonnegative integers.\u201d The local `schur` is `\u2211 T \u2208 ssytFinset lam, T.toMonomial`, with tableaux having entries in `Fin N`, weak rows, and strict columns, matching `s_\u03bb := \u2211_{T \u2208 SSYT(\u03bb)} x_T`. Mathlib documents `hsymm` as the sum of all degree-n monomials and `esymm` as the sum of all degree-n squarefree monomials, matching the blueprint meanings of h_n and e_n. Finally, membership in `verticalNStripPartitions mu n` is equivalent to containment `\u2200 i, mu.parts i \u2264 lam.parts i`, the vertical condition `\u2200 i, lam.parts i \u2264 mu.parts i + 1`, and `\u2211 i, lam.parts i = \u2211 i, mu.parts i + n`. Horizontal membership uses containment, `\u2200 i < N-1, mu_i \u2265 lam_{i+1}`, the same size equality, and an apparent upper-bound condition; that bound is redundant, since for positive indices it is exactly the horizontal-strip inequality and at index zero it follows from containment plus the total size difference. Thus both finite sums range over exactly the N-partitions whose skew differences are the respective horizontal or vertical n-strips."
}
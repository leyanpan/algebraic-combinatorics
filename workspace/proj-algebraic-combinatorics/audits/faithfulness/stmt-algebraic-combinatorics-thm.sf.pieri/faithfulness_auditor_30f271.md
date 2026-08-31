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
  "justification": "The elaborated signatures are `\u2200 {N : Nat} {R : Type u} [CommRing R] (n : Nat) (mu : SymmetricFunctions.NPartition N), hsymm (Fin N) R n * schur mu = \u2211 lam \u2208 horizontalNStripPartitions mu n, schur lam` and the analogous equality with `esymm` and `verticalNStripPartitions`. These directly match the blueprint binders \u201cLet n \u2208 \u2115. Let \u03bc be an N-partition\u201d and conclusions \u201ch_n s_\u03bc = \u2211 ... s_\u03bb\u201d and \u201ce_n s_\u03bc = \u2211 ... s_\u03bb.\u201d The implicit quantification over `N` and `R` makes the result uniform in the formal polynomial-ring setting; `[CommRing R]` is the coefficient-ring setting used by the project definition of the polynomial ring, not an added mathematical hypothesis on `n` or `\u03bc`. The local `SymmetricFunctions.NPartition N` has fields `parts : Fin N \u2192 \u2115` and `weaklyDecreasing : \u2200 i j, i \u2264 j \u2192 parts j \u2264 parts i`, exactly the blueprint definition of a weakly decreasing N-tuple of nonnegative integers. `schur lam` is definitionally `\u2211 T \u2208 ssytFinset lam, T.toMonomial`, with tableaux taking entries in `Fin N`, matching `s_\u03bb`. Mathlib defines `hsymm` as the sum of all degree-`n` monomials and `esymm` as the sum of all degree-`n` squarefree monomials, matching the blueprint definitions of `h_n` and `e_n`. Finally, `horizontalNStripPartitions mu n` filters for componentwise containment, `isHorizontalStripFun lam mu` (`mu_i \u2265 lam_{i+1}`), and `\u2211 lam_i = \u2211 mu_i + n`; `verticalNStripPartitions mu n` similarly filters for containment, `lam_i \u2264 mu_i + 1`, and the same size equality. These are precisely the blueprint conditions that `\u03bb/\u03bc` have no two new boxes in one column or row and have exactly `n` boxes. The horizontal enumeration also contains an explicit upper bound, but it is redundant: for positive indices it follows from the horizontal-strip inequality, and at index zero it follows from containment and total size difference. Thus it does not narrow the indexed set. Both declarations therefore express exactly the two Pieri rules."
}
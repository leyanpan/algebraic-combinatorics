Declaration: AlgebraicCombinatorics.littlewoodRichardson
Module: AlgebraicCombinatorics.SymmetricFunctions.LittlewoodRichardson

Statement id: stmt-algebraic-combinatorics-thm.sf.lr-zy

## INFORMAL STATEMENT
Zelevinsky’s generalized Littlewood–Richardson rule, in Yamanouchi form

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\begin{equation}  s_{\nu }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}s_{\nu +\operatorname *{cont}T}. \end{equation}

## VERDICT
{
  "verdict": "drift",
  "justification": "The elaborated signature contains the unsupported stronger typeclass binder `{R : Type u} [CommRing R] ... [IsDomain R]`, whereas the blueprint states only \u201cLet \u03bb, \u03bc, \u03bd be three N-partitions\u201d and its polynomial-ring definition is `K[x\u2081, ..., x_N]` over a commutative ring, formalized with `[CommRing K]`. Thus `littlewoodRichardson` proves the rule only when the coefficient ring is an integral domain, not for the blueprint\u2019s arbitrary commutative ring. There is also drift in the tableau dependency. The blueprint definition says, \u201cIf we don\u2019t have \u03bc \u2286 \u03bb, then we agree that there are no Young tableaux of shape \u03bb/\u03bc.\u201d But this declaration uses `Tableau lam mu := {c // c \u2208 skewYoungDiagram lam mu} \u2192 Fin N`, where `skewYoungDiagram lam mu := {c | mu c.1 < c.2 \u2227 c.2 \u2264 lam c.1}`. This merely omits rows where \u03bc exceeds \u03bb; it does not make the tableau type empty when `\u03bc \u2288 \u03bb`. Consequently the sums in `skewSchurPoly` and in `\u2211 T : {T : Tableau lam mu // IsYamanouchi nu T}, ...` have the wrong indexing set for such N-partitions. The partition binders themselves are faithful: `(lam mu nu : Fin N \u2192 \u2115)` together with `(hlam : IsNPartition lam) (hmu : IsNPartition mu) (hnu : IsNPartition nu)`, and `IsNPartition lam := \u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i`, exactly encode the blueprint\u2019s weakly decreasing nonnegative N-tuples. To make the formalization faithful, remove the `[IsDomain R]` restriction from `littlewoodRichardson` and arrange its proof for every `[CommRing R]`; additionally, change `Tableau` (or its underlying shape representation) so that it is empty when `\u03bc \u2288 \u03bb`, with `skewSchurPoly` and the Yamanouchi indexing type using that corrected definition. Adding a `\u03bc \u2286 \u03bb` hypothesis to the theorem would instead narrow the blueprint\u2019s stated quantification and would not be faithful to its explicit empty-tableau convention."
}
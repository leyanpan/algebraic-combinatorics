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
  "justification": "The elaborated declaration is `\u2200 {R : Type u} [CommRing R] {N : \u2115} [IsDomain R] (lam mu nu : Fin N \u2192 \u2115), IsNPartition lam \u2192 IsNPartition mu \u2192 IsNPartition nu \u2192 ...`. Its partition binders correctly answer the blueprint's \u201cLet \u03bb, \u03bc, \u03bd be three N-partitions\u201d: `IsNPartition lam := \u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`, exactly weak decrease. Its summation index also expands appropriately to semistandard \u03bd-Yamanouchi tableaux: `IsYamanouchi nu T := IsSemistandard T \u2227 \u2200 j > 0, IsNPartition (nu + contentColGeq T j)`, matching the blueprint definition. However, there are two decisive restrictions/mismatches. First, `[IsDomain R]` is an added hypothesis. The blueprint polynomial ring is `P K N = MvPolynomial (Fin N) K` under only `[CommRing K]`; neither the theorem text nor that definition requires K to be a domain. Thus the formal theorem is weaker than the stated rule over the fixed commutative coefficient ring. This enters directly through the binder `[IsDomain R]` of `AlgebraicCombinatorics.littlewoodRichardson`; it should be removed, with the proof obtained without domain cancellation (for example over integer coefficients followed by coefficient base change). Second, the blueprint tableau definition says: \u201cIf we don\u2019t have \u03bc \u2286 \u03bb, then we agree that there are no Young tableaux of shape \u03bb/\u03bc.\u201d The dependency used here instead defines `skewYoungDiagram lam mu := {c | mu c.1 < c.2 \u2227 c.2 \u2264 lam c.1}` and `Tableau lam mu := {c // c \u2208 skewYoungDiagram lam mu} \u2192 Fin N` without a global `\u03bc \u2286 \u03bb` guard. If containment fails in one row but not another, this still produces a partially nonempty diagram and tableaux, whereas the blueprint prescribes none. Since the target quantifies over all three N-partitions and has no `\u03bc \u2286 \u03bb` hypothesis, this changes both `skewSchurPoly lam mu` and the RHS index set. To make the statement faithful, `Tableau`/`skewYoungDiagram` (and consequently `skewSchurPoly`) must enforce the blueprint\u2019s globally empty convention when `\u03bc \u2284 \u03bb`, or the target would need a containment hypothesis; the former preserves the stated unrestricted theorem, while the latter would itself narrow the blueprint quantifier."
}
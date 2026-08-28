Declaration: AlgebraicCombinatorics.littlewoodRichardson
Module: AlgebraicCombinatorics.SymmetricFunctions.LittlewoodRichardson

Statement id: stmt-algebraic-combinatorics-thm.sf.lr-zy

## INFORMAL STATEMENT
Zelevinsky’s generalized Littlewood–Richardson rule, in Yamanouchi form

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\begin{equation}  s_{\nu }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}s_{\nu +\operatorname *{cont}T}. \end{equation}

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: yes. The elaborated conclusion is exactly `schurPoly nu * skewSchurPoly lam mu = \u2211 T : {T : Tableau lam mu // IsYamanouchi nu T}, schurPoly (nu + contentTableau T.val)`, matching the informal `s_\u03bd \u00b7 s_{\u03bb/\u03bc} = \u2211 ... s_{\u03bd+cont T}`. Its hypotheses `hlam`, `hmu`, and `hnu` require precisely the stated three N-partitions: `IsNPartition lam`, `IsNPartition mu`, and `IsNPartition nu`, where `IsNPartition` is defined by `\u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`. The summation index also has the intended meaning. `Tableau lam mu` consists of fillings of cells satisfying `mu c.1 < c.2 \u2227 c.2 \u2264 lam c.1`; `IsYamanouchi nu T` is `IsSemistandard T \u2227 \u2200 j : \u2115, j > 0 \u2192 IsNPartition (nu + contentColGeq T j)`, so the subtype sums exactly over \u03bd-Yamanouchi semistandard tableaux of shape \u03bb/\u03bc. Finally, `contentTableau T i` counts cells whose entry is `i`, while `skewSchurPoly` is the tableau generating function and `schurPoly lam` is defined as `skewSchurPoly lam 0`, giving the intended Schur polynomials. Q2: yes. The hidden binders `{R : Type u} [CommRing R] [IsDomain R]` place the equality in `MvPolynomial (Fin N) R`. This is coefficient-ring generality rather than a change to the combinatorial assertion: specializing to the conventional integer coefficient ring recovers the informal identity, and the integer polynomial identity extends by coefficient base change to every integral-domain coefficient ring covered by the Lean theorem. Thus neither direction introduces a different tableau class, shape, content, partition condition, or polynomial identity."
}
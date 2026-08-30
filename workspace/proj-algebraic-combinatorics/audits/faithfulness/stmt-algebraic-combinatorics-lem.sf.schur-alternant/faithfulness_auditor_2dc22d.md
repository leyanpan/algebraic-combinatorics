Declaration: AlgebraicCombinatorics.schurPoly_eq_alternant_div
Module: AlgebraicCombinatorics.SymmetricFunctions.LittlewoodRichardson

Statement id: stmt-algebraic-combinatorics-lem.sf.schur-alternant

## INFORMAL STATEMENT
Schur–alternant relation

\leanhelper  Let $\lambda $ be an $N$-partition. Then, 

\[  a_{\lambda + \rho } = a_{\rho } \cdot s_{\lambda }.  \]

 (This is Theorem~ \ref{thm.sf.schur-symm}~ \textbf{(b)}.)

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signature is `\u2200 {R : Type u} [CommRing R] {N : \u2115} (lam : Fin N \u2192 \u2115), IsNPartition lam \u2192 alternant (lam + rho N) = alternant (rho N) * schurPoly lam`. This directly matches the blueprint binders and conclusion: \u201cLet \u03bb be an N-partition\u201d and `a_{\u03bb+\u03c1} = a_\u03c1 \u00b7 s_\u03bb`. The referenced definitions preserve the intended meanings: `IsNPartition lam` unfolds to `\u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`, exactly a weakly decreasing N-tuple of natural numbers; `rho N i = N - 1 - i.val`, giving `(N-1, N-2, ..., 0)`; function addition is entrywise; `alternant \u03b1` is the signed permutation sum equivalent to the defining determinant; and `schurPoly lam` is the sum of tableau monomials over semistandard tableaux of shape `lam/0`, hence the blueprint's `s_\u03bb`. The formal coefficient ring binder `[CommRing R]` is the blueprint's commutative base ring `K`, not an added mathematical hypothesis. No partition, index-range, or ring restriction beyond the blueprint setting is introduced."
}
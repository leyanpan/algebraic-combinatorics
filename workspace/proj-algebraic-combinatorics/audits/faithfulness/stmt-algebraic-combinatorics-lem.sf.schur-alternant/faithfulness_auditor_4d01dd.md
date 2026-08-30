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
  "justification": "The blueprint says, \u201cLet \u03bb be an N-partition\u201d and asserts \u201ca_{\u03bb+\u03c1} = a_\u03c1 \u00b7 s_\u03bb.\u201d The elaborated signature is `{R : Type u} [CommRing R] {N : \u2115} (lam : Fin N \u2192 \u2115) (hlam : IsNPartition lam) : alternant (lam + rho N) = alternant (rho N) * schurPoly lam`. The binder `hlam : IsNPartition lam` unfolds to `\u2200 i j : Fin N, i \u2264 j \u2192 lam j \u2264 lam i`, exactly the blueprint definition of a weakly decreasing N-tuple of natural numbers. Addition is pointwise, and `rho N i = N - 1 - i.val`, matching \u03c1 = (N-1, N-2, ..., 0). The referenced `alternant` is extensionally the blueprint alternant: `alternant_eq_det` identifies it with the determinant of the transpose of `(x_i^(\u03b1_j))`, which has the same determinant. The referenced `schurPoly lam` unfolds to the sum of `xPow (contentTableau T)` over tableaux satisfying `IsSemistandard`, whose body requires entries in `Fin N`, weak increase along rows, and strict increase down columns, matching the blueprint definition of `s_\u03bb`. Finally, `[CommRing R]` is the formal encoding of the blueprint polynomial ring `K[x_1, ..., x_N]` with commutative-ring coefficients, not an added hypothesis. Unlike the separate bundled Schur definition, this declaration does not require `NeZero N`; covering `N = 0` makes it slightly more general rather than weaker."
}
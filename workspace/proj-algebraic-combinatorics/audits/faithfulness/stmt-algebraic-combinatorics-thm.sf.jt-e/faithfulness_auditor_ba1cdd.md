Declaration: SymmetricFunctions.jacobiTrudi_e
Module: AlgebraicCombinatorics.SymmetricFunctions.PieriJacobiTrudi

Statement id: stmt-algebraic-combinatorics-thm.sf.jt-e

## INFORMAL STATEMENT
Second Jacobi–Trudi formula

Let $\lambda $ and $\mu $ be two partitions. Let $\lambda ^{t}$ and $\mu ^{t}$ be the transposes of $\lambda $ and $\mu $. Let $M\in \mathbb {N}$ be such that both $\lambda ^{t}$ and $\mu ^{t}$ have length $\leq M$. We extend the partitions $\lambda ^{t}$ and $\mu ^{t}$ to $M$-tuples (by inserting zeroes at the end). Write these $M$-tuples $\lambda ^{t}$ and $\mu ^{t}$ as $\lambda ^{t}=\left( \lambda _{1}^{t},\lambda _{2}^{t},\ldots ,\lambda _{M}^{t}\right) $ and $\mu ^{t}=\left( \mu _{1}^{t},\mu _{2}^{t},\ldots ,\mu _{M}^{t}\right) $. Then,

\[  s_{\lambda /\mu }=\det \left( \left( e_{\lambda _{i}^{t}-\mu _{j}^{t}-i+j}\right) _{1\leq i\leq M,\  1\leq j\leq M}\right) .  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The elaborated declaration quantifies a single dimension: \"\u2200 {N : \u2115} {R : Type} [CommRing R] (lam mu lamt muT : Fin N \u2192 \u2115)\" and forms both \"skewSchur ... : MvPolynomial (Fin N) R\" and a determinant indexed by \"Fin N\". Thus N simultaneously fixes the number of polynomial variables, the tuple length of \u03bb and \u03bc, and the determinant size. The blueprint instead independently quantifies \"M \u2208 \u2115 ... such that both \u03bb\u1d57 and \u03bc\u1d57 have length \u2264 M\" and asks for the determinant over \"1 \u2264 i \u2264 M, 1 \u2264 j \u2264 M\". Consequently, the Lean theorem only covers the special case in which that freely chosen M equals the number N of polynomial variables and the padded lengths of \u03bb, \u03bc. This is a narrowed quantifier, not merely an encoding requirement. The transpose relation itself is suitable: `NPartition.IsTranspose` is defined with independent dimensions `{N M : \u2115}` as `IsTranspose (lam : Fin N \u2192 \u2115) (lamt : Fin M \u2192 \u2115)`, so the blueprint is expressible in the project. The drift enters specifically in `SymmetricFunctions.jacobiTrudi_e` at the binders `(lamt muT : Fin N \u2192 \u2115)` and the resulting `Matrix (Fin N) (Fin N)`. To make it faithful, introduce an independent `{M : \u2115}`, bind `lamt muT : Fin M \u2192 \u2115` (and their monotonicity hypotheses over `Fin M`), retain `lam mu : Fin N \u2192 \u2115` and `esymm (Fin N) R` for the polynomial-variable setting, and index the matrix and determinant by `Fin M`."
}
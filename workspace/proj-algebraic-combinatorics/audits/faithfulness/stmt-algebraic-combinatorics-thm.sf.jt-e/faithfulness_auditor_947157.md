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
  "justification": "The elaborated signature conflates the blueprint's independent matrix size M with the number N of polynomial variables. Formally it binds `lam mu lamt muT : Fin N \u2192 \u2115`, uses `MvPolynomial.esymm (Fin N) R`, and takes the determinant of a `Matrix (Fin N) (Fin N)`. The blueprint instead says: \"Let M \u2208 \u2115 be such that both \u03bb\u1d57 and \u03bc\u1d57 have length \u2264 M\" and forms the M-by-M matrix, while the surrounding polynomial-ring definition fixes P = K[x\u2081,\u2026,x_N]. Thus the formal theorem only covers M = N and, through `NPartition.IsTranspose lam lamt` with both functions indexed by `Fin N`, only shapes whose partitions and transposes both fit in N entries. For example, an N-partition of width greater than N is covered by the blueprint after choosing a larger M but cannot satisfy this formal transpose hypothesis. There is also an added hypothesis `hcontained : \u2200 i : Fin N, mu i \u2264 lam i`. The blueprint only says \"Let \u03bb and \u03bc be two partitions\"; its skew-tableau definition handles the non-contained case by declaring that there are no tableaux, whereas the target uses `SymmetricFunctions.skewSchur` whose argument is a `SkewPartition N`, and that structure contains the field `contained : inner \u2264 outer`. The intended statement is expressible in the project: make M a separate binder, take `lam mu : Fin N \u2192 \u2115`, `lamt muT : Fin M \u2192 \u2115`, use `NPartition.IsTranspose` at these two different lengths, and form a `Matrix (Fin M) (Fin M)` whose entries remain `esymm (Fin N) R`; additionally use an unbundled skew-Schur definition supporting arbitrary \u03bb and \u03bc, or encode its stipulated zero value when \u03bc is not contained, rather than requiring `hcontained`."
}
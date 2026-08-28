Declaration: SymmetricFunctions.skewSchur_isSymmetric_jacobiTrudi
Module: AlgebraicCombinatorics.SymmetricFunctions.PieriJacobiTrudi

Statement id: stmt-algebraic-combinatorics-thm.sf.skew-schur-symm-jt

## INFORMAL STATEMENT
thm.sf.skew-schur-symm-jt

\leanhelper  Skew Schur polynomials are symmetric: for any partitions $\lambda \supseteq \mu $, $s_{\lambda /\mu }$ is a symmetric polynomial. 

This provides a proof of symmetry via the Jacobi–Trudi formula, without relying on the Bender–Knuth involution.

## VERDICT
{
  "verdict": "unstatable",
  "justification": "Q1: no. Q2: yes. The informal statement quantifies over \u201cany partitions \u03bb \u2287 \u03bc\u201d and asserts that \u201cs_{\u03bb/\u03bc} is a symmetric polynomial.\u201d In the intended finite-variable setting, the partition length and the number of polynomial variables are independent. The module itself confirms this: \u201cIn the source, M is the length of the partition tuples (for Jacobi-Trudi), while N is the number of variables,\u201d followed by \u201cWe use a single parameter N for simplicity in this formalization.\u201d The elaborated declaration instead has one implicit binder `{N : \u2115}` and takes `lam mu : Fin N \u2192 \u2115`, while its conclusion concerns `MvPolynomial (Fin N) R`. This forces the partitions to have exactly the same indexing dimension as the variable set. Consequently, for a fixed number N of variables, skew shapes represented using M-partitions with M > N cannot even be supplied to the theorem. Thus the Lean theorem proves only the dimension-diagonal cases M = N and does not imply the unrestricted informal claim; the informal claim does imply those cases. The mismatch enters through the definitions: `SkewPartition (N)` contains `NPartition N`, `SkewSSYT (s : SkewPartition N)` has entries in `Fin N`, and `skewSchur` returns `MvPolynomial (Fin N) R`, all using the same parameter. The intended independent-dimension theorem cannot be stated with this `skewSchur`, so the verdict is unstatable rather than ordinary drift. To make it faithful, generalize the tableau and polynomial definitions to separate parameters M and N, for example `SkewSSYT (s : SkewPartition M)` with entries in `Fin N` and `skewSchur : SkewPartition M \u2192 MvPolynomial (Fin N) R`, then state the theorem with `lam mu : Fin M \u2192 \u2115` and independent `{M N : \u2115}`."
}
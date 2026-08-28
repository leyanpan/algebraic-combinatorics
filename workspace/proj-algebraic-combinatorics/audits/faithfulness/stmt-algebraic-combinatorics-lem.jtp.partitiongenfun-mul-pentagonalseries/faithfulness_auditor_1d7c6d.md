Declaration: AlgebraicCombinatorics.partitionGenFun_mul_pentagonalSeries
Module: AlgebraicCombinatorics.PentagonalJacobi

Statement id: stmt-algebraic-combinatorics-lem.jtp.partitiongenfun-mul-pentagonalseries

## INFORMAL STATEMENT
lem.jtp.partitionGenFun-mul-pentagonalSeries

\leanhelper  We have $P\cdot Q = 1$, where $P=\sum _{n\geq 0}p(n)x^{n}$ is the partition generating function and $Q=\sum _{k\in \mathbb {Z}}(-1)^{k}x^{w_{k}}$ is the pentagonal series.

## VERDICT
{
  "verdict": "faithful",
  "justification": "Q1: yes. The elaborated signature is exactly \u201cpartitionGenFun * pentagonalSeries = 1\u201d in \u2124\u27e6X\u27e7, matching the informal \u201cP\u00b7Q = 1.\u201d The referenced definitions give \u201cpartitionGenFun := PowerSeries.mk fun n => partitionCount n,\u201d with partitionCount an alias for Nat.Partition.partitionCount, so it is precisely the informal \u201cP = \u2211_{n\u22650} p(n)x^n.\u201d Likewise, \u201cpentagonalSeries := PowerSeries.mk fun n => (pentagonalCoeff n : R),\u201d where pentagonalCoeff is (-1)^k.natAbs when n = pentagonalNumber k and zero otherwise, and \u201cpentagonalNumber (k : \u2124) := ((3 * k - 1) * k / 2).toNat.\u201d Since the pentagonal numbers are nonnegative and injective, this coefficientwise definition is exactly the locally finite formal series \u201cQ = \u2211_{k\u2208\u2124} (-1)^k x^{w_k}\u201d; using k.natAbs does not change the sign because (-1)^k = (-1)^|k|. Thus the Lean equality implies the stated generating-function identity. Q2: yes. Interpreting the informal P and Q as formal power series with integer coefficients gives exactly the two Lean definitions, so the informal identity implies the Lean equality. There are no additional binders, hypotheses, typeclass restrictions, or narrowed index ranges in the elaborated theorem."
}
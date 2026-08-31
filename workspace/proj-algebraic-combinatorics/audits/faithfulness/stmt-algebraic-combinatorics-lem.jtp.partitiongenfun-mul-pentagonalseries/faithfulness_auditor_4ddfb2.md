Declaration: AlgebraicCombinatorics.partitionGenFun_mul_pentagonalSeries
Module: AlgebraicCombinatorics.PentagonalJacobi

Statement id: stmt-algebraic-combinatorics-lem.jtp.partitiongenfun-mul-pentagonalseries

## INFORMAL STATEMENT
lem.jtp.partitionGenFun-mul-pentagonalSeries

\leanhelper  We have $P\cdot Q = 1$, where $P=\sum _{n\geq 0}p(n)x^{n}$ is the partition generating function and $Q=\sum _{k\in \mathbb {Z}}(-1)^{k}x^{w_{k}}$ is the pentagonal series.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated declaration has no binders or added hypotheses and states exactly `partitionGenFun * pentagonalSeries = 1` in `\u2124\u27e6X\u27e7`, matching the blueprint fragment \u201cWe have P\u00b7Q = 1.\u201d The referenced definitions also match the blueprint notation: `partitionGenFun : \u2124\u27e6X\u27e7 := PowerSeries.mk fun n => \u2191(partitionCount n)`, where `partitionCount n := Fintype.card (Partition n)`, realizes \u201cP = \u2211_{n\u22650} p(n)x^n\u201d; and `pentagonalSeries := PowerSeries.mk fun n => \u2191(pentagonalCoeff n)`, with `pentagonalCoeff (pentagonalNumber k) = (-1 : \u2124) ^ k.natAbs` and `pentagonalNumber k := ((3 * k - 1) * k / 2).toNat`, realizes \u201cQ = \u2211_{k\u2208\u2124} (-1)^k x^{w_k}.\u201d The use of `k.natAbs` does not change the sign because integer powers of `-1` depend only on parity. Thus the formal equality is the same formal-power-series identity as the informal statement, without a restriction or extra assumption."
}
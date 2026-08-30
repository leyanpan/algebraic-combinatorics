Declaration: AlgebraicCombinatorics.partitionGenFun_mul_pentagonalSeries
Module: AlgebraicCombinatorics.PentagonalJacobi

Statement id: stmt-algebraic-combinatorics-lem.jtp.partitiongenfun-mul-pentagonalseries

## INFORMAL STATEMENT
lem.jtp.partitionGenFun-mul-pentagonalSeries

\leanhelper  We have $P\cdot Q = 1$, where $P=\sum _{n\geq 0}p(n)x^{n}$ is the partition generating function and $Q=\sum _{k\in \mathbb {Z}}(-1)^{k}x^{w_{k}}$ is the pentagonal series.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated signature has no hidden binders or added hypotheses: `AlgebraicCombinatorics.partitionGenFun_mul_pentagonalSeries : partitionGenFun * pentagonalSeries = 1`, with `pentagonalSeries` instantiated at `\u2124\u27e6X\u27e7`. This exactly answers the blueprint fragment `We have P\u00b7Q = 1`. The referenced definitions also match the blueprint notation: `partitionGenFun : \u2124\u27e6X\u27e7 := PowerSeries.mk fun n => partitionCount n`, corresponding to `P = \u2211_{n\u22650} p(n)x^n`, and `pentagonalSeries : R\u27e6X\u27e7 := PowerSeries.mk fun n => (pentagonalCoeff n : R)`, instantiated here with `R = \u2124`. Its coefficient definition returns `(-1 : \u2124) ^ k.natAbs` when `n = pentagonalNumber k`, and `pentagonalNumber (k : \u2124) : \u2115 := ((3 * k - 1) * k / 2).toNat`; the proved nonnegativity makes this the blueprint's `w_k = ((3k-1)k)/2`. Thus this coefficient presentation is precisely the definition node's `Q = \u2211_{k\u2208\u2124} (-1)^k x^{w_k}` (with `(-1)^k = (-1)^{|k|}`), and the formal equality is the claimed generating-series identity over `\u2124[[x]]`."
}
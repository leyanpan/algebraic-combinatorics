Declaration: AlgebraicCombinatorics.partitionGenFun_mul_pentagonalSeries
Module: AlgebraicCombinatorics.PentagonalJacobi

Statement id: stmt-algebraic-combinatorics-lem.jtp.partitiongenfun-mul-pentagonalseries

## INFORMAL STATEMENT
lem.jtp.partitionGenFun-mul-pentagonalSeries

\leanhelper  We have $P\cdot Q = 1$, where $P=\sum _{n\geq 0}p(n)x^{n}$ is the partition generating function and $Q=\sum _{k\in \mathbb {Z}}(-1)^{k}x^{w_{k}}$ is the pentagonal series.

## VERDICT
{
  "verdict": "faithful",
  "justification": "Both implications hold. The informal claim is \u201cWe have P\u00b7Q = 1,\u201d with \u201cP=\u2211_{n\u22650} p(n)x^n\u201d and \u201cQ=\u2211_{k\u2208\u2124}(-1)^k x^{w_k}.\u201d The elaborated Lean signature has no hidden binders or added hypotheses: `partitionGenFun * (pentagonalSeries : \u2124\u27e6X\u27e7) = 1`. Its definitions match the named series. Lean defines `partitionGenFun` as `PowerSeries.mk fun n => \u2191(partitionCount n)`, while `Nat.Partition.partitionCount` is `fun n => Fintype.card n.Partition`, so its coefficient at n is exactly p(n). It defines `pentagonalNumber (k : \u2124)` as `((3 * k - 1) * k / 2).toNat`, the project\u2019s w_k, and `pentagonalSeries` as `PowerSeries.mk fun n => \u2191(pentagonalCoeff n)`, where `pentagonalCoeff n` is `(-1 : \u2124) ^ k.natAbs` when `pentagonalNumberInverse n = some k`, and zero otherwise. This coefficient representation is equivalent to the stated integer-indexed sum: `pentagonalNumber_injective` proves the exponents are distinct, and `pentagonalNumberInverse_of_pentagonalNumber` proves every w_k is recovered. Using `k.natAbs` does not alter the sign because integer powers of -1 satisfy `(-1)^k = (-1)^|k|`, including negative k. Thus the Lean equality is precisely the informal formal-power-series identity over integer coefficients, with neither narrowed quantification nor an additional hypothesis."
}
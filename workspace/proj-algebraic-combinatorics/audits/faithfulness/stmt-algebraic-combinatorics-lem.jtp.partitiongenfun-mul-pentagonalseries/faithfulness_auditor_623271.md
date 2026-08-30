Declaration: AlgebraicCombinatorics.partitionGenFun_mul_pentagonalSeries
Module: AlgebraicCombinatorics.PentagonalJacobi

Statement id: stmt-algebraic-combinatorics-lem.jtp.partitiongenfun-mul-pentagonalseries

## INFORMAL STATEMENT
lem.jtp.partitionGenFun-mul-pentagonalSeries

\leanhelper  We have $P\cdot Q = 1$, where $P=\sum _{n\geq 0}p(n)x^{n}$ is the partition generating function and $Q=\sum _{k\in \mathbb {Z}}(-1)^{k}x^{w_{k}}$ is the pentagonal series.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The elaborated declaration has no binders or hypotheses and states exactly `partitionGenFun * (pentagonalSeries : \u2124\u27e6X\u27e7) = 1`, matching the informal claim \u201cWe have $P\\cdot Q=1$.\u201d The referenced definitions also match the informal identifications: `partitionGenFun : \u2124\u27e6X\u27e7 := PowerSeries.mk fun n => partitionCount n`, where `partitionCount n := Fintype.card (Partition n)`, realizes \u201c$P=\\sum_{n\\geq0}p(n)x^n$\u201d; and `pentagonalSeries : R\u27e6X\u27e7 := PowerSeries.mk fun n => (pentagonalCoeff n : R)`, with `pentagonalCoeff` equal to `(-1 : \u2124) ^ k.natAbs` at `n = pentagonalNumber k` and zero otherwise, realizes \u201c$Q=\\sum_{k\\in\\mathbb Z}(-1)^k x^{w_k}$.\u201d Here `pentagonalNumber (k : \u2124) := ((3*k-1)*k/2).toNat` agrees with the blueprint definition $w_k=((3k-1)k)/2$, whose value is nonnegative, and using `k.natAbs` gives the same sign as the integer-exponent notation $(-1)^k$. Thus the formal equality is precisely the blueprint equality in `\u2124\u27e6X\u27e7`, with no added assumptions or restricted quantifiers."
}
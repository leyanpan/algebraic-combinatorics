Declaration: AlgebraicCombinatorics.partition_recursive
Module: AlgebraicCombinatorics.PentagonalJacobi

Statement id: stmt-algebraic-combinatorics-cor.pars.pn-rec

## INFORMAL STATEMENT
cor.pars.pn-rec

For each positive integer $n$, we have 

\begin{align*}  p\left( n\right) &  =\sum _{\substack {k\in \mathbb {Z};\\ \begin{bgroup} k\neq 0

\end{bgroup}}}\left( -1\right) ^{k-1}p\left( n-w_{k}\right) \\ &  =p\left( n-1\right) +p\left( n-2\right) -p\left( n-5\right) -p\left( n-7\right) \\ &  \  \  \  \  \  \  \  \  \  \  +p\left( n-12\right) +p\left( n-15\right) -p\left( n-22\right) -p\left( n-26\right) \pm \cdots . \end{align*}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifier, \"For each positive integer n\", is represented exactly by the formal binders `(n : \u2115) (hn : n > 0)`. Its main equality, `p(n) = \u2211_{k\u2208\u2124; k\u22600} (-1)^{k-1} p(n-w_k)`, is represented by `partitionCount n = \u2211' k : {k : \u2124 // k \u2260 0 \u2227 pentagonalNumber k \u2264 n}, (if k.val.natAbs % 2 = 1 then (1 : \u2124) else (-1 : \u2124)) * partitionCount (n - pentagonalNumber k.val)`. The extra-looking condition `pentagonalNumber k \u2264 n` is not a mathematical restriction: the blueprint definition makes `p(m)` the number of partitions of the integer `m`, hence `p(m)=0` for negative `m`; the formalization instead uses the natural-domain definition `Nat.Partition.partitionCount (n : \u2115) := Fintype.card (Partition n)` and omits exactly those zero summands rather than applying truncated natural subtraction to them. The dependency `pentagonalNumber` has body `((3 * k - 1) * k / 2).toNat`, matching the blueprint definition `w_k=((3k-1)k)/2`, whose value is nonnegative. Finally, the formal sign is equivalent to `(-1)^{k-1}` for nonzero integral `k`: it is `+1` when `|k|` is odd and `-1` when `|k|` is even. Together with the pentagonal values for `k=1,-1,2,-2,3,-3,\u2026`, this gives exactly the displayed expansion `p(n-1)+p(n-2)-p(n-5)-p(n-7)+p(n-12)+p(n-15)-\u22ef`."
}
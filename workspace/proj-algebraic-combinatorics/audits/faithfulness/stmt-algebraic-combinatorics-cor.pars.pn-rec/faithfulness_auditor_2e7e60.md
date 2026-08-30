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
  "justification": "The blueprint quantifies \"For each positive integer n\"; the elaborated Lean signature has exactly `(n : \u2115) (hn : n > 0)`. Its conclusion is `\u2191(partitionCount n) = \u2211' (k : {k // k \u2260 0 \u2227 pentagonalNumber k \u2264 n}), (if k.val.natAbs % 2 = 1 then 1 else -1) * \u2191(partitionCount (n - pentagonalNumber k.val))`, matching `p(n) = \u2211_{k\u2208\u2124; k\u22600} (-1)^{k-1} p(n-w_k)`. The apparent restriction `pentagonalNumber k \u2264 n` is a faithful finite-support encoding, not a narrowed theorem: the blueprint definition sets `p(m)` to the number of partitions of every integer `m`, and there are no partitions of a negative integer, so all omitted terms with `w_k > n` are zero. Within the subtype, natural subtraction `n - pentagonalNumber k` therefore agrees with integer subtraction. The referenced definitions also match: `partitionCount n := Fintype.card (Partition n)` counts partitions, while `pentagonalNumber k := ((3*k - 1)*k / 2).toNat`; the numerator is nonnegative and divisible by 2, so this is the blueprint's `w_k = ((3k-1)k)/2`. Finally, the formal sign is `+1` exactly when `|k|` is odd and `-1` when it is even, which equals `(-1)^{k-1}` for nonzero integer `k`. For `k = 1,-1,2,-2,3,-3,4,-4`, this gives respectively the displayed terms `+p(n-1)+p(n-2)-p(n-5)-p(n-7)+p(n-12)+p(n-15)-p(n-22)-p(n-26)`."
}